# Methodology — Processing Chain

> Detailed walkthrough of the production chain, from raw data to the final georeferenced 3D scene.
> Companion document to [`README.md`](../README.md).

---

## Overview

The workflow splits into two independent branches that converge only at the end:

| Branch | Input | Output | Environment |
|--------|-------|--------|-------------|
| **Territory** | Orthophoto + OSM | LoD1 urban context, GeoPackage | QGIS |
| **Building** | Mobile-mapping point cloud | LOD 500 as-built model, IFC | ReCap → Revit → Blender |

Convergence happens in **ArcGIS Pro**, in a single local 3D scene tied to EPSG:26191.

---

## Step 1 — Urban context in QGIS

### 1.1 Georeferencing the base

The orthophoto is georeferenced in **EPSG:26191 — Merchich / Nord Maroc**, the official Moroccan projection for the northern zone.

| Parameter | Value |
|-----------|-------|
| Projection type | Lambert conformal conic, 1 standard parallel |
| Reference ellipsoid | Clarke 1880 (IGN) |
| Latitude of origin | 33.3° N |
| Central meridian | −5.4° |
| Scale factor at origin | 0.999625769 |
| False easting (X₀) | 500,000 m |
| False northing (Y₀) | 300,000 m |

Every subsequent layer inherits this CRS. Consistency at this stage is what makes the rest of the chain possible.

### 1.2 Point-cloud merging

The LAZ tiles delivered by the mobile-mapping survey are merged using the **GeoRaster3D** plugin, producing a single working extract:

- **633,946 points**
- coverage **852 × 954 m — 81.3 ha**
- format **LAS 1.4 COPC**, produced by **PDAL 2.9.0**

### 1.3 OpenStreetMap extraction

Contextual layers are acquired through **Overpass API** queries issued from the **QuickOSM** plugin:

| Layer | OSM key/value | Post-processing |
|-------|---------------|-----------------|
| Road network | `highway=*` | Hierarchised by class (primary / secondary / residential / service) |
| Building footprints | `building=*` | Cleaned, tied to EPSG:26191 |
| Vegetation | `landuse=grass`, `natural=tree`, `leisure=park` | Merged into a single vegetation layer |
| Public transport | `highway=bus_stop`, `public_transport=*` | Point layer |

All layers are reprojected to EPSG:26191 and exported to a **single GeoPackage container** — one file, one CRS, one deliverable.

> **Why GeoPackage rather than Shapefile?** No 10-character field-name limit, no multi-file fragility, native CRS storage, OGC standard, and direct compatibility with both QGIS and ArcGIS Pro.

---

## Step 2 — Scan-to-BIM of the R+4 building

### 2.1 Point-cloud preparation (Autodesk ReCap)

The cloud acquired by the mobile-mapping system is imported into **Autodesk ReCap**, where it is:

1. cleaned — removal of vegetation noise, passing vehicles and stray returns
2. cropped to the building's extent
3. exported to **`.rcp`**, the format Revit consumes natively

### 2.2 Modelling in Revit

| Sub-step | Operation |
|----------|-----------|
| Cloud insertion | `.rcp` linked into the Revit project |
| Level registration | Storey levels aligned on the cloud's floor slabs, in cutaway view |
| Envelope modelling | Walls, floors, roof modelled directly against the cloud |
| Openings | Windows and doors positioned from the surveyed geometry |
| Curtain walls | Modelled with real mullion and panel divisions |

The result is an **as-built** model — not a design model. Geometry follows what was measured, not what was drawn.

### 2.3 LOD 500 — what is claimed and what is not

**LOD 500** (AIA / BIM Forum) designates a *field-verified* level of development: the element is modelled as actually built, with verified size, shape, location, quantity and orientation.

In this project the LOD 500 claim covers **the building envelope only**. Structural, MEP and electrical packages were not modelled and are explicitly out of scope. Stating this boundary matters more than claiming a higher number.

---

## Step 3 — Georeferencing the BIM model

This is the critical step of the whole chain, and the one where the land surveyor's expertise is not optional.

### 3.1 The problem

A Revit model is born in **project-local coordinates** — an arbitrary origin, usually near the building. A territorial GIS lives in a **national projection**. Placing the first inside the second requires an explicit, controlled transformation.

### 3.2 The solution applied

| Setting | Configuration |
|---------|---------------|
| **Survey Point** | Set to the building's real coordinates in EPSG:26191 |
| **True north angle** | Declared, so the model's north matches geographic north |
| **Project Base Point** | Kept at the local origin for modelling comfort |
| **IFC export** | *Coordination View*, coordinate base = **Shared Coordinates** |

With this configuration, the exported IFC arrives in ArcGIS Pro **already positioned**. `Define Projection` in ArcGIS Pro does not move anything — it merely declares which CRS the incoming geometry is expressed in.

> **A common misconception.** Georeferencing is not done "in the GIS at the end". It is done **upstream, in Revit**. Anything else is fitting geometry by eye.

### 3.3 What the IFC file does *not* carry

Inspection of the delivered **IFC4X3_ADD2** file shows:

- ❌ no `IfcMapConversion` — the transformation to the map CRS is absent
- ❌ no `IfcProjectedCRS` — the target CRS is not declared
- ⚠️ `IfcSite` retains the exporter's **default geographic coordinates**, not the real site
- ✅ geometric context tolerance: **1 × 10⁻⁵ m**

The schema provides for these entities. The export chain simply does not write them. The consequence is significant: **the georeferencing works, but it does not travel with the file**. Any recipient who does not know the shared-coordinates convention receives a model whose position cannot be recovered from the file itself.

This is documented as the project's principal finding on openBIM interoperability, and it drives the first item of the future-work list.

---

## Step 4 — IFC → CityJSON conversion and detail loss

### 4.1 The conversion path tested

```
Revit  ──IFC (Coordination View, shared coords)──▶  Blender + Bonsai
                                                          │
                                              rewrite to IFC4X3_ADD2
                                                          │
                                                          ▼
                                                     CityJSON
                                                          │
                                             CityJSON Loader plugin
                                                          ▼
                                                        QGIS
```

**Blender with the Bonsai extension** was used to inspect the full IFC hierarchy and to rewrite the file to the IFC4X3_ADD2 schema before conversion.

### 4.2 Where the detail is lost

The initial hypothesis was that QGIS was degrading the model. Systematic testing of each link showed otherwise.

**The loss occurs during the IFC → CityJSON conversion.** The conversion merges the building envelope into a **single solid**:

| Preserved | Lost |
|-----------|------|
| Overall building volume | Openings (windows, doors) |
| Footprint | Curtain walls and mullions |
| Height | Wall/floor/roof distinction |
| Position | BIM semantic attributes (IfcWall, IfcWindow, property sets) |

Visualised through **Qgis2threejs**, the building is reduced to an extruded volume — visually indistinguishable from the LoD1 context blocks around it.

### 4.3 Consequence for the project

Since the CityJSON path could not carry LOD 500 into the GIS, the integration environment was changed: **ArcGIS Pro** was used instead, importing the IFC directly and preserving the model's detail alongside the LoD1 context.

This is not a workaround presented as a success — it is a characterised limit of the IFC/CityJSON pair, documented with the exact step responsible.

---

## Step 5 — Final integration in ArcGIS Pro

| Operation | Detail |
|-----------|--------|
| GIS layers | Exported from QGIS to GeoPackage, imported into ArcGIS Pro |
| CRS declaration | `Define Projection` → EPSG:26191 on incoming geometry |
| Context | Building footprints extruded to LoD1 |
| Building | LOD 500 IFC model imported, already positioned via shared coordinates |
| Scene | Local 3D scene assembled, both scales coexisting |
| Verification | Position checked on comparison points |

The final scene shows LoD1 context volumes in blue and the LOD 500 building in grey — the difference in detail is immediately legible, which is precisely the point the project set out to demonstrate.

---

## Reproducibility notes

| Requirement | Status |
|-------------|--------|
| Software list and versions | ✅ documented in [`README.md`](../README.md#technology-stack) |
| CRS parameters | ✅ documented above |
| OSM extraction queries | ✅ reproducible via QuickOSM presets |
| Revit georeferencing settings | ✅ documented above |
| Source point cloud | ❌ not redistributable — see [`DATA-SOURCES.md`](DATA-SOURCES.md) |
| Orthophoto | ❌ not redistributable |

Anyone with equivalent survey data over another sector can reproduce the full chain from this document.

---

## See also

- [`DATA-SOURCES.md`](DATA-SOURCES.md) — data provenance and licences
- [`GLOSSARY.md`](GLOSSARY.md) — GeoBIM terminology, EN–FR
- [`LESSONS-LEARNED.md`](LESSONS-LEARNED.md) — technical retrospective
