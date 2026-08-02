# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] — 2026-07-29

First public release: complete final-year project (PFE), defended at IFMBTP Fès.

### Added

**GIS baseline (O1)**
- Orthophoto georeferenced in EPSG:26191 (Merchich / Nord Maroc)
- LAZ point-cloud merging with GeoRaster3D
- OpenStreetMap extraction via Overpass queries (QuickOSM): hierarchised road
  network, building footprints, vegetation, bus stops
- Export of all vector layers to a single GeoPackage container

**As-built BIM model (O2)**
- Mobile-mapping point cloud cleaned in Autodesk ReCap, exported to `.rcp`
- Level registration on the point cloud in Revit
- R+4 building modelled to LOD 500 on the envelope: walls, floors, roof,
  curtain walls, openings

**Georeferencing (O3)**
- Revit *Survey Point* set to real EPSG:26191 coordinates
- True-north angle declared
- IFC export in shared coordinates (Coordination View)
- Georeferencing verified on comparison points in ArcGIS Pro

**Interoperability assessment (O4)**
- IFC → CityJSON conversion tested through Blender + Bonsai (rewrite to
  IFC4X3_ADD2) and CityJSON Loader for QGIS
- Detail loss formally localised at the IFC → CityJSON step
- 3D navigable preview generated with Qgis2threejs

**Unified 3D scene (O5)**
- Final ArcGIS Pro local scene combining LoD1 urban context and LOD 500 building
- Video walkthrough of the scene

**Deliverables**
- Standalone responsive HTML report (`index.html`), 12 sections, mobile-first,
  no framework, no build step
- Quality-control table read directly from production files
- Critical retrospective: limitations and perspectives

### Documented findings
- The IFC4X3_ADD2 file produced by the export chain contains neither
  `IfcMapConversion` nor `IfcProjectedCRS`, although the schema provides for them
- `IfcSite` retains the exporter's default geographic coordinates
- IFC → CityJSON conversion merges the building envelope into a single solid,
  dropping openings, curtain walls and semantic attributes

### Repository setup
- Bilingual documentation (English / French)
- MIT licence with third-party data notices
- `.gitignore` tuned for GIS, BIM and LaTeX workflows
- GitHub Pages deployment workflow

---

## [Unreleased] — planned

### Planned
- Quantify the four declared-but-unmeasured controls:
  - announced accuracy of the mobile-mapping system
  - method and number of control points used to register the point cloud
  - deviation between modelled surfaces and the source cloud
  - planimetric deviation of the building on comparison points
- Write `IfcMapConversion` and `IfcProjectedCRS` at IFC export, and populate
  `IfcSite` with real coordinates
- Convert to CityGML 3.0 / CityJSON at LoD2 or LoD3 to preserve façades and openings
- Automated LoD1 extrusion of the entire district from point-cloud heights
- Publish layers and 3D scene on a map server
- English version of the web report (`index.en.html`)
- Digital twin extension: utility networks, public lighting, asset management

---

[1.0.0]: https://github.com/benhassaneamine/geobim-tamansourt/releases/tag/v1.0.0
