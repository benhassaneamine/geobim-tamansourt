# Contributing

Thank you for your interest in this project.

This repository documents a **completed final-year academic project** (PFE, IFMBTP Fès, 2025–2026). It is published primarily as a portfolio piece and as a documented case study of GeoBIM integration in the Moroccan national reference system.

Contributions are nevertheless welcome — particularly from the GIS, surveying and openBIM communities.

---

## What is especially welcome

**Technical discussion**
- Feedback on the georeferencing approach (Revit shared coordinates vs. `IfcMapConversion`)
- Experience with IFC → CityGML/CityJSON conversion that **preserves** LoD2/LoD3 detail
- Alternative toolchains for GIS ↔ BIM integration
- Corrections on geodesy, projection parameters or CRS handling

**Documentation**
- Typos, grammar or clarity fixes in `README.md`, `README.fr.md` or `docs/`
- Translations into other languages
- Glossary additions in `docs/GLOSSARY.md`

**Web report**
- Accessibility improvements (ARIA, contrast, keyboard navigation)
- Responsive behaviour fixes on specific devices
- Performance optimisations

---

## What cannot be accepted

- **Source survey data.** The point cloud and orthophoto belong to ETAFAT and are not redistributable. Please do not submit them, or derivatives that would expose them.
- **Rewrites of the academic content.** Findings, results and the critical retrospective reflect work that was defended before a jury and must remain faithful to it.

---

## How to contribute

### Reporting an issue

Open an [issue](../../issues) and include:

- a clear title
- what you observed, and what you expected
- for the web report: browser, version, device and a screenshot if relevant
- for technical content: the source, standard or specification supporting your point

### Submitting a change

```bash
# 1. Fork, then clone your fork
git clone https://github.com/YOUR-GITHUB-USERNAME/geobim-tamansourt.git
cd geobim-tamansourt

# 2. Create a branch
git checkout -b fix/short-description

# 3. Make your changes, then commit
git commit -m "docs: fix EPSG parameter in accuracy table"

# 4. Push and open a pull request
git push origin fix/short-description
```

### Commit message convention

This project follows [Conventional Commits](https://www.conventionalcommits.org/):

| Prefix | Use for |
|--------|---------|
| `feat:` | New content or feature |
| `fix:` | Correction of an error |
| `docs:` | Documentation only |
| `style:` | Formatting, no content change |
| `refactor:` | Restructuring without behaviour change |
| `chore:` | Maintenance, tooling, configuration |

---

## Code style (web report)

- HTML5, semantic elements, `lang` attributes correctly set
- CSS custom properties for all colours and typography — no hard-coded hex values in rules
- Mobile-first media queries
- No JavaScript, no framework, no build step: the report must stay a single self-contained file
- Preserve the existing French code comments and section banners

---

## Code of conduct

Be respectful, constructive and precise. Technical disagreement is welcome; personal attacks are not. Contributors are expected to assume good faith.

---

## Contact

For questions that do not fit an issue:

**Amine Ben Elhassane** — [benhassaneamine48@gmail.com](mailto:benhassaneamine48@gmail.com)
