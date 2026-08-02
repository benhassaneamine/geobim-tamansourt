# Data Sources, Licences and Reference System

---

## Study area

| Item | Value |
|------|-------|
| Sector | Tamansourt (new town) |
| Province | Al Haouz |
| Region | Marrakech-Safi |
| Country | Morocco |
| Extent of working extract | 852 × 954 m — 81.3 ha |

---

## Coordinate reference system

**EPSG:26191 — Merchich / Nord Maroc**

| Parameter | Value |
|-----------|-------|
| Projection | Lambert conformal conic, 1 standard parallel |
| Geodetic datum | Merchich |
| Reference ellipsoid | Clarke 1880 (IGN) |
| Latitude of origin | 33.3° N |
| Central meridian | −5.4° |
| Scale factor at origin | 0.999625769 |
| False easting (X₀) | 500,000 m |
| False northing (Y₀) | 300,000 m |
| Unit | metre |

Reference: [epsg.io/26191](https://epsg.io/26191)

All layers, the point cloud and the BIM model are expressed in this system. No reprojection occurs anywhere in the chain after the initial georeferencing.

---

## Data inventory

### 1. Mobile-mapping point cloud

| Attribute | Value |
|-----------|-------|
| Source | **ETAFAT, Casablanca** — provided for the final-year internship |
| Acquisition | Mobile mapping system |
| Format | LAS 1.4 COPC |
| Production chain | PDAL 2.9.0 |
| Points (working extract) | 633,946 |
| Coverage | 852 × 954 m — 81.3 ha |
| CRS | EPSG:26191 |
| **Redistribution** | ❌ **Not included in this repository.** Reproduction and reuse subject to prior written authorisation from ETAFAT. |

**Not yet quantified:** the announced accuracy of the mobile-mapping system, and the method and number of control points used to register the cloud. These are declared as open rather than estimated.

### 2. Orthophoto

| Attribute | Value |
|-----------|-------|
| Source | **ETAFAT, Casablanca** |
| Use | Georeferenced base for the GIS layers |
| CRS | EPSG:26191 |
| **Redistribution** | ❌ **Not included in this repository.** |

### 3. OpenStreetMap layers

| Attribute | Value |
|-----------|-------|
| Source | [OpenStreetMap](https://www.openstreetmap.org) |
| Acquisition | Overpass API queries via the QuickOSM plugin for QGIS |
| Extraction period | 14 → 22 June 2026 |
| Layers | Road network (hierarchised), building footprints, vegetation, public transport stops |
| Delivery format | GeoPackage (OGC) |
| **Licence** | **ODbL** — Open Database License |
| **Attribution required** | © OpenStreetMap contributors |

> ⚠️ **Fitness for use.** OpenStreetMap layers have uneven completeness and are **not certified for regulatory, cadastral or land-registry purposes**. They are used here as contextual data only.

Licence text: [opendatacommons.org/licenses/odbl](https://opendatacommons.org/licenses/odbl/)
Attribution guidance: [osmfoundation.org/wiki/Licence](https://osmfoundation.org/wiki/Licence)

### 4. BIM model (produced by the author)

| Attribute | Value |
|-----------|-------|
| Author | Amine Ben Elhassane |
| Software | Autodesk Revit |
| Exchange format | IFC4X3_ADD2 |
| Level of development | LOD 500 on the envelope |
| Coordinate base | Shared coordinates |
| Geometric context tolerance | 1 × 10⁻⁵ m |
| **Redistribution** | ❌ Not included — derived from restricted survey data |

### 5. Images and cartographic plates

| Attribute | Value |
|-----------|-------|
| Author | Amine Ben Elhassane |
| Content | Screenshots, renderings, map layouts |
| Location | [`../images/`](../images/) |
| Licence | © 2026 Amine Ben Elhassane — reuse permitted with attribution |

---

## What is and is not in this repository

| Included ✅ | Excluded ❌ |
|-------------|-------------|
| Web report (`index.html`) | Point cloud (`.las` / `.laz` / `.rcp`) |
| Screenshots and map plates | Orthophoto (raster) |
| Full methodology documentation | Revit project file (`.rvt`) |
| CRS parameters and QC values | IFC model (`.ifc`) |
| Software list and versions | GeoPackage of GIS layers |

The exclusions are enforced by [`.gitignore`](../.gitignore) and reflect both file-size constraints and the confidentiality of the source data.

---

## Requesting access to the source data

The survey data belongs to **ETAFAT, Casablanca**. Requests must be addressed to ETAFAT directly. The author of this project cannot grant redistribution rights.

For questions about the methodology itself, contact:
**Amine Ben Elhassane** — [benhassaneamine48@gmail.com](mailto:benhassaneamine48@gmail.com)

---

## Standards and specifications referenced

| Standard | Body | Use in this project |
|----------|------|---------------------|
| **IFC 4.3 (IFC4X3_ADD2)** | buildingSMART / ISO 16739 | BIM exchange format |
| **CityGML 3.0 / CityJSON** | OGC | Urban 3D model, LoD1 |
| **GeoPackage** | OGC | Vector layer container |
| **LAS 1.4 / COPC** | ASPRS / COPC.io | Point-cloud format |
| **LOD specification** | AIA / BIM Forum | Level of development (LOD 500) |
| **EPSG registry** | IOGP | CRS definition (26191) |
