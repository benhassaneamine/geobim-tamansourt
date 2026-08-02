# Glossary — GeoBIM, GIS & Surveying (EN ↔ FR)

Bilingual reference for the terminology used throughout this project.

---

## Core concepts

| English | Français | Definition |
|---------|----------|------------|
| **GeoBIM** | GéoBIM | The convergence of GIS (territory scale) and BIM (building scale) into a single georeferenced information environment. |
| **BIM** — Building Information Modeling | Modélisation des informations du bâtiment | Digital representation of a building's physical and functional characteristics, carrying both geometry and semantics. |
| **GIS** — Geographic Information System | SIG — Système d'Information Géographique | System for capturing, storing, analysing and displaying spatially referenced data. |
| **Digital twin** | Jumeau numérique | A georeferenced model enriched with live or operational data (networks, lighting, asset management). |
| **Smart City** | Ville intelligente | Urban management approach built on integrated, up-to-date digital data infrastructure. |

---

## Levels of detail — two different scales

> These two acronyms look alike and mean different things. Confusing them is the most common error in GeoBIM discussions.

| Term | Standard | What it qualifies |
|------|----------|-------------------|
| **LOD 100–500** | AIA / BIM Forum | The **reliability of information** in a BIM element |
| **LoD0–LoD4** | CityGML / CityJSON | The **geometric granularity** of an urban object |

### BIM — LOD (Level of Development)

| Level | Meaning |
|-------|---------|
| LOD 100 | Symbolic representation, approximate |
| LOD 200 | Generic element, approximate size and location |
| LOD 300 | Specific element, accurate size, shape and location |
| LOD 350 | LOD 300 + interfaces with other systems |
| LOD 400 | Fabrication and assembly level detail |
| **LOD 500** | **Field-verified as-built** — verified size, shape, location, quantity, orientation |

### CityGML — LoD (Level of Detail)

| Level | Meaning |
|-------|---------|
| LoD0 | 2D footprint |
| **LoD1** | **Extruded block — flat roof, no façade detail** |
| LoD2 | Differentiated roof shapes, coarse façade elements |
| LoD3 | Detailed façades with openings (windows, doors) |
| LoD4 | LoD3 + interior spaces |

**In this project:** the building reaches LOD 500 in Revit; after IFC → CityJSON conversion it degrades to LoD1. This degradation is the project's central interoperability finding.

---

## Geodesy and surveying

| English | Français | Definition |
|---------|----------|------------|
| **CRS** — Coordinate Reference System | SCR — Système de coordonnées de référence | Framework defining how coordinates map to positions on Earth. |
| **Georeferencing** | Géoréférencement | Assigning real-world coordinates to a dataset or model. |
| **Geodetic datum** | Datum géodésique | Reference surface and origin from which coordinates are computed (here: Merchich). |
| **Reference ellipsoid** | Ellipsoïde de référence | Mathematical approximation of the Earth's shape (here: Clarke 1880 IGN). |
| **Lambert conformal conic** | Lambert conique conforme | Conic map projection preserving angles; the Moroccan national projection family. |
| **Scale factor** | Facteur d'échelle | Ratio between distance on the projection and distance on the ellipsoid. |
| **Central meridian** | Méridien central | Longitude of the projection's axis of symmetry. |
| **False easting / northing** | Constantes X₀ / Y₀ | Offsets added to coordinates to keep all values positive. |
| **Planimetric deviation** | Écart planimétrique | Horizontal difference between a modelled position and a control measurement. |
| **Control point** | Point d'appui | Known-coordinate point used to register or verify a dataset. |
| **Comparison point** | Point de comparaison | Point used to check agreement between two datasets. |
| **EPSG code** | Code EPSG | Numeric identifier of a CRS in the EPSG registry (here: 26191). |

---

## Point clouds and scanning

| English | Français | Definition |
|---------|----------|------------|
| **Point cloud** | Nuage de points | Set of 3D points measured by laser scanning or photogrammetry. |
| **Mobile mapping** | Cartographie mobile | Survey by vehicle-mounted sensors acquiring data while moving. |
| **Scan-to-BIM** | Scan-to-BIM | Workflow converting a point cloud into a structured BIM model. |
| **LAS / LAZ** | LAS / LAZ | Standard (LAS) and compressed (LAZ) point-cloud formats. |
| **COPC** — Cloud Optimized Point Cloud | COPC | LAS variant enabling efficient streaming and partial reads. |
| **PDAL** | PDAL | Point Data Abstraction Library — open-source point-cloud processing. |
| **Registration** | Recalage / rattachement | Aligning a point cloud to a known reference frame. |
| **Cutaway view** | Vue en écorché | Section view revealing internal structure. |

---

## openBIM and exchange formats

| English | Français | Definition |
|---------|----------|------------|
| **IFC** — Industry Foundation Classes | IFC | Open, vendor-neutral BIM exchange format (ISO 16739). |
| **IFC4X3_ADD2** | IFC4X3_ADD2 | IFC 4.3 schema version, extended for infrastructure. |
| **Coordination View** | Vue de coordination | IFC Model View Definition intended for multi-discipline coordination. |
| **Shared coordinates** | Coordonnées partagées | Revit mechanism placing a model in a common real-world reference. |
| **Survey Point** | Point topographique | Revit point defining the model's real-world coordinates. |
| **Project Base Point** | Point de base du projet | Revit local origin used for modelling. |
| **`IfcMapConversion`** | `IfcMapConversion` | IFC entity storing the transformation from local to map coordinates. |
| **`IfcProjectedCRS`** | `IfcProjectedCRS` | IFC entity declaring the target projected CRS. |
| **`IfcSite`** | `IfcSite` | IFC entity describing the site, including geographic coordinates. |
| **CityJSON** | CityJSON | JSON encoding of the CityGML data model. |
| **GeoPackage** | GeoPackage | OGC SQLite-based container for vector, raster and tile data. |
| **BCF** — BIM Collaboration Format | BCF | Format for exchanging issues and comments between BIM tools. |

---

## Urban and GIS data

| English | Français | Definition |
|---------|----------|------------|
| **Building footprint** | Emprise bâtie | 2D outline of a building at ground level. |
| **Extrusion** | Extrusion | Generating a 3D volume by raising a 2D footprint to a height. |
| **Road hierarchy** | Hiérarchie routière | Classification of roads by function (primary, secondary, residential…). |
| **Overpass API** | API Overpass | Query service for extracting OpenStreetMap data. |
| **ODbL** — Open Database License | Licence ODbL | Open licence governing OpenStreetMap data reuse. |
| **Vector layer** | Couche vecteur | Geographic layer made of points, lines or polygons. |
| **Cartographic layout** | Mise en page cartographique | Composed map with legend, scale, north arrow and metadata. |

---

## Software

| Tool | Type | Role here |
|------|------|-----------|
| **QGIS** | Open source | Desktop GIS, layer production, cartographic layout |
| **ArcGIS Pro** | Commercial (Esri) | Final georeferenced 3D scene |
| **QuickOSM** | QGIS plugin | OSM extraction via Overpass |
| **GeoRaster3D** | QGIS plugin | LAZ point-cloud merging |
| **Qgis2threejs** | QGIS plugin | Navigable 3D web view |
| **CityJSON Loader** | QGIS plugin | CityJSON import |
| **Autodesk ReCap** | Commercial | Point-cloud cleaning, `.rcp` export |
| **Autodesk Revit** | Commercial | BIM modelling, shared coordinates |
| **Blender + Bonsai** | Open source | IFC inspection and schema rewriting |
| **PDAL** | Open source | Point-cloud processing library |
| **LaTeX** | Open source | Dissertation typesetting |

---

## French academic terms

| Français | English |
|----------|---------|
| **PFE** — Projet de Fin d'Études | Final-year project / capstone project |
| **IFMBTP** | Institut de Formation aux Métiers du Bâtiment et des Travaux Publics |
| **Technicien Spécialisé Géomètre-Topographe** | Specialised Technician — Land Surveyor |
| **Encadrante pédagogique** | Academic supervisor |
| **Encadrante professionnelle** | Industrial supervisor |
| **Organisme d'accueil** | Host organisation |
| **Lotissement** | Housing development / subdivision district |
| **Tel que construit** | As-built |
| **Mémoire** | Dissertation / thesis |
