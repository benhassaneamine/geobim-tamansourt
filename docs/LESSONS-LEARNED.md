# Lessons Learned — Technical Retrospective

> What this project taught, beyond the deliverable itself.

---

## 1. Georeferencing is decided upstream, not at the end

The most common assumption in GeoBIM discussions is that the building "gets georeferenced in the GIS". It does not — or rather, it should not.

By the time a model reaches ArcGIS Pro, its position is already fixed. `Define Projection` only *declares* which CRS the geometry is expressed in; it moves nothing. If the Revit **Survey Point** and true-north angle were not configured before export, no GIS operation will recover the correct position. Fitting the model by eye afterwards produces something that looks right and is geodetically meaningless.

**Takeaway:** the surveyor's intervention point is at the start of the BIM workflow, not at the end of the GIS one.

---

## 2. The IFC schema provides for georeferencing — exporters do not write it

`IfcMapConversion` and `IfcProjectedCRS` exist in IFC 4 precisely to carry the local-to-map transformation and the target CRS. Both are absent from the file this chain produced, and `IfcSite` kept the exporter's default geographic coordinates.

The practical consequence: **the model is correctly positioned, but the file cannot prove it.** A recipient who does not know the shared-coordinates convention receives geometry whose absolute position is unrecoverable from the file itself.

**Takeaway:** "supports IFC" and "carries its georeferencing" are different claims. Verify the header, not the marketing.

---

## 3. Diagnose the chain link by link before blaming a tool

The working hypothesis was that QGIS was flattening the model. Testing each step separately showed the degradation happened one stage earlier, in the **IFC → CityJSON conversion**, which merges the envelope into a single solid.

Had the diagnosis stopped at "QGIS loses detail", the conclusion would have been wrong and the remedy (switching GIS) would have been the right action for the wrong reason — and would not have generalised.

**Takeaway:** isolating the failing link is worth more than working around it. The workaround is disposable; the diagnosis transfers to the next project.

---

## 4. A characterised limit is a result, not a failure

The project did not achieve LOD 500 preservation through the CityJSON path. Stating that plainly, with the exact responsible step identified, is more useful to a reader than a partial success dressed up as a complete one.

The same applies to the four quality controls that were not quantified. They are declared as open — the accuracy of the mobile-mapping system, the registration method and control-point count, the surface-to-cloud deviation, and the planimetric deviation on comparison points — rather than approximated with plausible-sounding numbers.

**Takeaway:** in surveying, an unquantified figure and an invented one are not equally honest. Only one of them can be corrected later.

---

## 5. Two "LOD" acronyms, two different questions

LOD 500 (AIA / BIM Forum) answers *how reliable is this information?*
LoD1 (CityGML) answers *how detailed is this geometry?*

Moving between them is not a resolution change — it is a change of semantic frame. A LOD 500 wall carries a type, a material, a fire rating and a verified position. The LoD1 volume that replaces it carries a footprint and a height. Nothing was "downsampled"; the object was replaced by a different kind of object.

**Takeaway:** interoperability failures in GeoBIM are usually semantic before they are geometric.

---

## 6. Open context data has a fitness-for-use boundary

OpenStreetMap made the urban context achievable in days rather than months. It is also of uneven completeness and is not certified for regulatory or cadastral use.

Both statements are true simultaneously, and a professional deliverable has to say so. Using OSM as context is sound; presenting it as survey-grade would not be.

**Takeaway:** state the fitness for use of every dataset. It is what separates a technical report from a demonstration.

---

## 7. Format choices compound

Choosing **GeoPackage** over Shapefile removed a whole class of downstream problems: no 10-character field-name truncation, no sidecar-file fragility, native CRS storage, and clean interchange between QGIS and ArcGIS Pro.

Small decisions early in a chain either accumulate friction or remove it. This one removed it.

**Takeaway:** prefer the format that carries its own metadata.

---

## 8. A single self-contained HTML file is a legitimate deliverable

The project report is one HTML file: no framework, no build step, no npm install, no JavaScript. It opens on any machine, any browser, offline, in five years' time.

For a portfolio piece meant to be opened by recruiters who will not clone a repository or run a dev server, this is a feature, not a limitation.

**Takeaway:** match the delivery format to how the artefact will actually be consumed.

---

## What I would do differently

| Area | Next time |
|------|-----------|
| Quality control | Plan the control-point campaign at the same time as the survey, not after modelling |
| IFC export | Verify `IfcMapConversion` / `IfcProjectedCRS` in the header *before* declaring the export complete, and script the fix if absent |
| Conversion path | Test the IFC → CityJSON path on a single test element in week one, not after the full model is built |
| Sample size | Model two buildings rather than one, to distinguish chain-level problems from building-specific ones |
| Automation | Script the OSM extraction and reprojection so the whole GIS baseline rebuilds in one command |

---

## Transferable skills

Beyond the software list, the project exercised:

- **framing a problem precisely** — the research question names both the constraint (national CRS) and the unknown (how far detail survives)
- **hypothesis testing under uncertainty** — testing each link rather than accepting the intuitive culprit
- **root-cause isolation** — separating symptom (LoD1 output) from cause (conversion step)
- **intellectual honesty in reporting** — declaring what was not measured
- **bilingual technical communication** — French dissertation, English documentation
