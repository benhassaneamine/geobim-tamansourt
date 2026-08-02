<div align="center">

# GeoBIM Integration for a Smart City — Tamansourt, Morocco

**From GIS territorial data to a LOD 500 as-built BIM model, unified in a single georeferenced 3D scene.**

Final-year engineering project (PFE) · 2025–2026 · IFMBTP Fès × ETAFAT Casablanca

[![Live Demo](https://img.shields.io/badge/Live_Demo-GitHub_Pages-00707f?style=for-the-badge&logo=github)](https://benhassaneamine.github.io/geobim-tamansourt/)
[![License: MIT](https://img.shields.io/badge/License-MIT-b3222a?style=for-the-badge)](LICENSE)
[![Français](https://img.shields.io/badge/Lire_en-Français-12a0b4?style=for-the-badge)](README.fr.md)

![CRS](https://img.shields.io/badge/CRS-EPSG:26191-informational)
![IFC](https://img.shields.io/badge/IFC-4X3__ADD2-blue)
![LOD](https://img.shields.io/badge/BIM-LOD_500-success)
![LoD](https://img.shields.io/badge/CityJSON-LoD1-orange)
![Status](https://img.shields.io/badge/status-completed-brightgreen)

![Final ArcGIS Pro 3D scene of the Tamansourt district](images/10-arcgis-final-scene.jpg)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Research Question](#research-question)
- [Objectives](#objectives)
- [Key Features](#key-features)
- [Screenshots](#screenshots)
- [Technology Stack](#technology-stack)
- [Project Architecture](#project-architecture)
- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Quality Control & Accuracy](#quality-control--accuracy)
- [Challenges Encountered](#challenges-encountered)
- [Limitations](#limitations)
- [Future Work](#future-work)
- [Skills Demonstrated](#skills-demonstrated)
- [Author](#author)
- [Acknowledgements](#acknowledgements)
- [License](#license)

---

## Overview

BIM describes a **building** with high fidelity. GIS describes a **territory** at scale. For a long time these two worlds evolved independently, with incompatible reference systems, data models and semantics. Their convergence is known as **GeoBIM**.

This project demonstrates the technical feasibility of that convergence on a real urbanised sector of **Tamansourt**, a new town near Marrakech, Morocco. The deliverable is a single georeferenced 3D scene that brings together:

- the **urban context** of the district — extruded building footprints, hierarchised road network, vegetation and public transport stops, all tied to the Moroccan national projection;
- a **five-storey (R+4) building** modelled *as-built* at **LOD 500** from a mobile-mapping point-cloud survey.

Both live in the same coordinate reference system: **Merchich / Nord Maroc — EPSG:26191**.

Beyond the 3D output, the project isolates and documents the single most critical bottleneck of the GeoBIM chain: **georeferencing the IFC model** — the exact point where the land surveyor's expertise becomes indispensable, and where standard export pipelines silently fail.

> **A note on two different "LOD" scales.** *LOD 500* comes from the AIA / BIM Forum specification and qualifies the **reliability of information** in a BIM model. *LoD1* comes from CityGML / CityJSON and qualifies the **geometric granularity** of an urban object. Moving from one to the other is not a simple loss of detail — it is a change of semantic frame of reference.

---

## Research Question

> How can geometric and geodetic consistency be guaranteed between a BIM building model — produced in project-local coordinates — and a GIS environment referenced in the Merchich / Nord Maroc national projection? And to what level of detail does that integration survive the exchange formats currently available?

---

## Objectives

| # | Objective | Outcome |
|---|-----------|---------|
| **O1** | Build the GIS baseline of the sector | Hierarchised road network, building footprints, vegetation and transport layers, all tied to EPSG:26191 in a single GeoPackage container |
| **O2** | Produce an *as-built* BIM model | R+4 building modelled through scan-to-BIM from a point cloud, up to LOD 500 on the building envelope |
| **O3** | Georeference and control | Anchor the model in the national system and quantify the quality of that anchoring — the core contribution of the land surveyor |
| **O4** | Evaluate the exchange chains | Test IFC → CityJSON → GIS, measure the loss of detail and pinpoint the responsible step |
| **O5** | Deliver a unified scene | Combine urban context and detailed building in one georeferenced 3D scene, usable as a Smart City foundation |

---

## Key Features

- **Full scan-to-BIM pipeline** — mobile-mapping LAZ/LAS point cloud → Autodesk ReCap cleaning → Revit modelling at LOD 500 (walls, floors, roof, curtain walls, openings, levels registered on the cloud).
- **Automated GIS data acquisition** — OpenStreetMap extraction through Overpass queries (QuickOSM), producing a hierarchised road network, building footprints, vegetation and bus-stop layers.
- **Rigorous national georeferencing** — Revit *Survey Point* set to real EPSG:26191 coordinates, true-north angle declared, IFC exported in **shared coordinates** so the model arrives already positioned.
- **openBIM interoperability testing** — IFC (Coordination View, IFC4X3_ADD2 via Blender/Bonsai) → CityJSON → QGIS, with the point of detail loss formally identified and documented.
- **Multi-scale 3D scene** — LoD1 extruded context and LOD 500 building coexisting in a single ArcGIS Pro local scene, verified on comparison points.
- **Documented quality control** — projection parameters, point-cloud metadata, IFC header and geometric tolerance read directly from production files, with unquantified controls explicitly declared rather than estimated.
- **Standalone responsive web report** — the whole project is presented as a single self-contained, mobile-first HTML page requiring no build step, no framework and no external dependency beyond web fonts.

---

## Screenshots

| GIS synthesis map | District zoom (LoD1) |
|---|---|
| ![GIS synthesis map](images/05-gis-synthesis-map.jpg) | ![District zoom](images/06-gis-zoom-district.jpg) |
| Complete vector layer set of the sector with full cartographic layout | Large-scale detail: footprints, vegetation, bus stops, LoD1 extent |

| Point cloud (ReCap) | OSM extraction (QGIS) |
|---|---|
| ![Point cloud](images/02-recap-point-cloud.jpg) | ![QGIS OSM extraction](images/01-qgis-osm-extraction.jpg) |
| R+4 building cloud in cutaway view, storeys visible | Overpass queries: roads in blue, footprints in grey |

| Revit LOD 500 model | IFC tree in Blender / Bonsai |
|---|---|
| ![Revit model](images/07-revit-lod500-model.jpg) | ![Blender Bonsai](images/03-blender-bonsai-ifc.jpg) |
| Curtain walls, openings and levels modelled from the survey | Full IFC hierarchy before conversion to CityJSON |

| Interoperability loss | Final ArcGIS Pro scene |
|---|---|
| ![LoD1 degradation](images/04-qgis2threejs-lod1-loss.jpg) | ![Final scene](images/08-lod500-in-context.jpg) |
| After IFC → CityJSON: extruded volumes only, no façades or openings | LOD 500 building among LoD1 volumes, same CRS |

📺 **[Watch the 3D scene walkthrough video](https://youtu.be/zoTWtQCNjIE)** *(link available in the web report)*

---

## Technology Stack

### GIS
| Tool | Role |
|------|------|
| **QGIS** | Desktop GIS, layer production and cartographic layout |
| **QuickOSM** | OpenStreetMap extraction via Overpass API queries |
| **GeoRaster3D** | LAZ point-cloud merging |
| **Qgis2threejs** | Navigable 3D web view |
| **CityJSON Loader** | CityJSON import into QGIS |
| **ArcGIS Pro** | Final georeferenced 3D scene assembly |
| **PDAL 2.9.0** | Point-cloud processing chain |

### BIM
| Tool | Role |
|------|------|
| **Autodesk ReCap** | Point-cloud cleaning and `.rcp` export |
| **Autodesk Revit** | LOD 500 as-built modelling, survey point, shared coordinates |
| **Blender + Bonsai** | IFC inspection and rewriting to IFC4X3_ADD2 |

### Formats & standards
`EPSG:26191 (Merchich / Nord Maroc)` · `LAS 1.4 COPC` · `IFC4X3_ADD2` · `CityJSON` · `GeoPackage (OGC)` · `LOD 500 (AIA / BIM Forum)` · `LoD1 (CityGML)`

### Web report
`HTML5` · `CSS3` (custom properties, Grid, Flexbox) · `Responsive / mobile-first design` · `Semantic markup & accessibility` · Zero JavaScript, zero framework, zero build step

### Documentation
`LaTeX` (dissertation) · `Markdown` (repository)

---

## Project Architecture

```
                        ┌─────────────────────────┐
                        │      RAW DATA           │
                        │  Orthophoto · LAZ/LAS   │
                        └───────────┬─────────────┘
              ┌─────────────────────┴─────────────────────┐
              ▼                                           ▼
   ╔══════════════════════╗                    ╔══════════════════════╗
   ║ PART 1 — TERRITORY   ║                    ║ PART 2 — BUILDING    ║
   ╚══════════════════════╝                    ╚══════════════════════╝
              │                                           │
   Orthophoto georeferenced                     Mobile-mapping LAZ/LAS
        EPSG:26191                                        │
              │                                           ▼
              ▼                                   Autodesk ReCap
            QGIS                                 (cleaning → .rcp)
   ┌──────────┴───────────┐                              │
   │ QuickOSM  GeoRaster3D│                              ▼
   │ Qgis2threejs         │                            Revit
   │ CityJSON Loader      │                    scan-to-BIM · LOD 500
   └──────────┬───────────┘                     R+4 building as-built
              │                                           │
              ▼                                           ▼
   ⚠ INTEROPERABILITY LIMIT                      Blender / Bonsai
   IFC → CityJSON degrades                    IFC · shared coordinates
   the building to LoD1                                   │
              │                                           │
              └─────────────────┬─────────────────────────┘
                                ▼
                    ╔═══════════════════════╗
                    ║      ArcGIS Pro       ║
                    ║ Georeferenced 3D scene║
                    ║   LoD1 + LOD 500      ║
                    ╚═══════════════════════╝
```

Full narrative walkthrough: **[docs/METHODOLOGY.md](docs/METHODOLOGY.md)**

---

## Repository Structure

```
geobim-tamansourt/
├── index.html              # Standalone web report (self-contained, GitHub Pages entry point)
├── README.md               # This file (English)
├── README.fr.md            # French version
├── LICENSE                 # MIT
├── CHANGELOG.md            # Version history
├── CONTRIBUTING.md         # Contribution guidelines
├── .gitignore
├── .github/
│   └── workflows/
│       └── pages.yml       # Automatic GitHub Pages deployment
├── assets/
│   └── social-preview.md   # Social preview & branding notes
├── docs/
│   ├── METHODOLOGY.md      # Detailed processing chain, step by step
│   ├── DATA-SOURCES.md     # Data provenance, licences, CRS parameters
│   ├── GLOSSARY.md         # GeoBIM / GIS / BIM terminology (EN–FR)
│   └── LESSONS-LEARNED.md  # Technical retrospective
└── images/
    ├── 00-cover.jpg
    ├── 01-qgis-osm-extraction.jpg
    ├── ...
    └── 11-author-portrait.jpg
```

---

## Installation

No build step, no dependency, no package manager. The web report is a single self-contained HTML file.

### Option 1 — View online
Open the live version on GitHub Pages:
```
https://benhassaneamine.github.io/geobim-tamansourt/
```

### Option 2 — Run locally
```bash
git clone https://github.com/benhassaneamine/geobim-tamansourt.git
cd geobim-tamansourt
```
Then simply open `index.html` in any modern browser.

Optionally, serve it over HTTP:
```bash
python3 -m http.server 8000
# then browse to http://localhost:8000
```

### Option 3 — Reproduce the GIS/BIM chain
| Software | Minimum version | Licence |
|----------|-----------------|---------|
| QGIS | 3.34 LTR | Open source |
| ArcGIS Pro | 3.x | Commercial / student |
| Autodesk Revit | 2024+ | Commercial / student |
| Autodesk ReCap | 2024+ | Commercial / student |
| Blender + Bonsai | 4.x | Open source |

QGIS plugins required: `QuickOSM`, `GeoRaster3D`, `Qgis2threejs`, `CityJSON Loader`.

> ⚠️ The source survey data (point cloud, orthophoto) was provided by **ETAFAT** in the context of the internship and is **not redistributed** in this repository. See [docs/DATA-SOURCES.md](docs/DATA-SOURCES.md).

---

## Usage

The web report is organised in twelve navigable sections:

1. **The project** — GeoBIM context and the two-LOD distinction
2. **Framing** — research question and operational objectives
3. **Workflow** — full production chain diagram
4. **Methodology** — the four processing steps
5. **GIS results** — cartographic plates
6. **BIM results** — Revit model plates
7. **Demonstration** — 3D scene video walkthrough
8. **Final integration** — ArcGIS Pro assembly
9. **Quality control** — accuracy and georeferencing table
10. **Limitations & perspectives** — critical retrospective
11. **Software environment** — toolchain
12. **Contact**

Navigation is sticky and fully keyboard-accessible; the layout adapts from 320 px mobile to desktop.

---

## Results

| Deliverable | Result |
|-------------|--------|
| GIS baseline | Roads, footprints, vegetation and transport layers extracted, hierarchised and exported to GeoPackage in EPSG:26191 |
| As-built BIM model | R+4 building modelled at **LOD 500** on the envelope from a 633,946-point cloud |
| Georeferencing | Model positioned through Revit shared coordinates + survey point in EPSG:26191, controlled on comparison points |
| Interoperability | Loss of detail **formally localised** at the IFC → CityJSON conversion — *not* in QGIS, contrary to the initial hypothesis |
| Final scene | LoD1 context and LOD 500 building coexisting in one ArcGIS Pro georeferenced 3D scene |
| Web deliverable | Single-file responsive HTML report, ~1 MB, no external dependency |

**The key finding:** the degradation of the building to LoD1 does not occur inside the GIS software. It occurs during the **IFC → CityJSON conversion**, which merges the envelope into a single solid — dropping openings, curtain walls and BIM semantic attributes. Identifying this precisely is what justified switching the integration environment from QGIS to ArcGIS Pro.

---

## Quality Control & Accuracy

Values read directly from production files (LAS header, IFC header, projection definition):

| Link | Characteristic | Measured value |
|------|----------------|----------------|
| Projection | Type | Lambert conformal conic, 1 parallel |
| Projection | Scale factor · origin latitude | 0.999625769 · 33.3° N |
| Projection | X₀ · Y₀ · central meridian | 500,000 · 300,000 m · −5.4° |
| Projection | Reference ellipsoid | Clarke 1880 (IGN) |
| Point cloud | Points in working extract | 633,946 |
| Point cloud | Coverage | 852 × 954 m — 81.3 ha |
| Point cloud | Format · production chain | LAS 1.4 COPC · PDAL 2.9.0 |
| IFC model | Schema of delivered file | IFC4X3_ADD2 |
| IFC model | Declared coordinate base | Shared coordinates |
| IFC model | Geometric context tolerance | 1 × 10⁻⁵ m |
| GIS layers | GeoPackage export of OSM layers | 14 → 22 June 2026 |

**Declared as not yet quantified** (stated openly rather than approximated): the announced accuracy of the mobile-mapping system, the method and number of control points used to register the cloud, the deviation between modelled surfaces and the source cloud, and the planimetric deviation of the building on comparison points.

---

## Challenges Encountered

1. **Reconciling two coordinate philosophies.** A BIM model is born in project-local coordinates; a territorial GIS lives in a national projection. Making both hold in the same space without losing what gives the model its value was the central difficulty of the whole project.

2. **IFC does not carry its own georeferencing.** The exported IFC4X3_ADD2 file contains neither `IfcMapConversion` nor `IfcProjectedCRS`, although the schema explicitly provides for them — the export chain simply does not write these entities. The anchoring therefore rests entirely on Revit shared coordinates: functional, but it does not travel with the file.

3. **Silent semantic loss in format conversion.** The IFC → CityJSON conversion merges the building envelope into a single solid. Openings, curtain walls and semantic attributes are not transposed. Diagnosing *where* the loss occurred — rather than assuming it was the GIS — required systematically testing each link of the chain.

4. **Changing integration environment mid-project.** Once the QGIS/CityJSON limit was characterised, the integration had to be rebuilt in ArcGIS Pro, which meant re-exporting all layers to GeoPackage and re-validating the georeferencing.

5. **Variable quality of open context data.** OpenStreetMap layers have uneven completeness and are not certified for regulatory or cadastral use — a constraint that had to be stated rather than hidden.

---

## Limitations

- **Georeferencing not carried by the exchange file** — no `IfcMapConversion` / `IfcProjectedCRS`; `IfcSite` keeps the exporter's default geographic coordinates.
- **IFC → CityJSON interoperability** — envelope merged into a single solid; openings, curtain walls and semantics lost.
- **Scope of LOD 500** — claimed on the surveyed envelope only; structural, MEP and electrical packages are not modelled.
- **Sample size** — a single building was processed; the chain has not yet been tested at full-district scale.
- **Context data** — OpenStreetMap layers are not certified for regulatory or land-registry use.

---

## Future Work

- **Write georeferencing into the file** — generate `IfcMapConversion` and `IfcProjectedCRS` at export and populate `IfcSite` with real coordinates, so the anchoring travels with the model.
- **Preserve level of detail** — convert to CityGML 3.0 / CityJSON at **LoD2 or LoD3** to retain façades and openings.
- **Generalise the context** — automated LoD1 extrusion of the whole district using heights derived from the point cloud.
- **Publish the layers** — serve the layers and the 3D scene from a map server for online consultation by technical departments.
- **Towards a digital twin** — associate operational data (utility networks, public lighting, asset management) with the georeferenced model.

---

## Skills Demonstrated

**Geomatics & surveying** — geodesy and projection systems (Lambert conformal conic, Clarke 1880 ellipsoid), georeferencing and datum transformation, point-cloud processing (LAS/LAZ/COPC), topographic quality control, cartographic design and layout.

**GIS** — QGIS and ArcGIS Pro, vector data modelling, OGC GeoPackage, Overpass/OpenStreetMap data acquisition, 3D scene construction, CityGML/CityJSON urban modelling.

**BIM** — scan-to-BIM workflow, Autodesk Revit modelling to LOD 500, shared coordinates and survey point configuration, IFC schema literacy (IFC4X3, Coordination View), openBIM interoperability diagnosis.

**GeoBIM & Smart City** — GIS ↔ BIM integration, multi-scale semantic reconciliation (LOD 500 ↔ LoD1), digital twin foundations, urban data infrastructure.

**Web & communication** — HTML5, CSS3 (custom properties, Grid, Flexbox), responsive mobile-first design, web accessibility, technical documentation in English and French, LaTeX.

**Method** — problem framing, systematic hypothesis testing, root-cause isolation, intellectual honesty in reporting unquantified controls.

---

## Author

<img src="images/11-author-portrait.jpg" width="120" align="left" style="margin-right:16px" alt="Amine Ben Elhassane" />

**Amine Ben Elhassane**
Specialised Technician — Land Surveyor / Geomatics Engineer
Georeferencing · Scan-to-BIM · 3D GIS

🎓 IFMBTP Fès — 2025/2026
🏢 Internship: ETAFAT, Casablanca
📍 Morocco — open to opportunities in Morocco and internationally

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/amine-ben-elhassane-644b3a328/)
[![Email](https://img.shields.io/badge/Email-benhassaneamine48@gmail.com-b3222a?style=flat-square&logo=gmail)](mailto:benhassaneamine48@gmail.com)

<br clear="left"/>

---

## Acknowledgements

- **Mme Nassira Bouissouden** — academic supervisor, IFMBTP Fès
- **Mme Fatine Choujae** — industrial supervisor, ETAFAT Casablanca
- **ETAFAT, Casablanca** — host organisation and provider of the source survey data
- **IFMBTP Fès** — Institut de Formation aux Métiers du Bâtiment et des Travaux Publics
- **OpenStreetMap contributors** — road, building, vegetation and transport data (ODbL licence)

---

## License

Source code and documentation of this repository are released under the [MIT License](LICENSE).

**Please note:**
- OpenStreetMap-derived data: © OpenStreetMap contributors, **ODbL** licence.
- Original survey data (point cloud, orthophoto) made available by **ETAFAT** for this final-year project — reproduction and reuse subject to prior authorisation, and **not included** in this repository.
- Photographs and renderings: © 2026 Amine Ben Elhassane.

---

<div align="center">

**If this project is useful or interesting to you, please consider giving it a ⭐**

`GeoBIM` · `GIS` · `BIM` · `Smart City` · `Scan-to-BIM` · `Digital Twin` · `Morocco`

</div>
