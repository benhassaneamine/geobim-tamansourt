# Social Preview & Branding Notes

---

## GitHub social preview image

GitHub shows a preview card when your repository link is shared on LinkedIn, X, Slack or WhatsApp. Setting it makes the difference between a bare grey card and a professional thumbnail.

**Specification**

| Property | Value |
|----------|-------|
| Recommended size | **1280 × 640 px** (2:1) |
| Maximum file size | 1 MB |
| Format | PNG or JPG |
| Safe zone | Keep text within the central 1100 × 500 px |

**How to set it**
`Repository → Settings → General → Social preview → Upload an image`

**Suggested composition**

```
┌──────────────────────────────────────────────────────────┐
│                                                          │
│   [ArcGIS final scene screenshot as background,          │
│    darkened ~40% with a #12181a overlay]                 │
│                                                          │
│   GeoBIM Integration for a Smart City                    │  ← Barlow Condensed 800, ~72px, #f3f5f0
│   Tamansourt, Morocco                                    │  ← Barlow Condensed 600, ~40px, #12a0b4
│                                                          │
│   GIS × BIM · LOD 500 · EPSG:26191                       │  ← IBM Plex Mono, ~28px, #e9ebe6
│                                                          │
│   Amine Ben Elhassane · IFMBTP Fès · 2026                │  ← Inter 500, ~24px, #c2c9c3
└──────────────────────────────────────────────────────────┘
```

Base image to use: `images/10-arcgis-final-scene.jpg`

**Tools:** Canva (1280 × 640 custom size), Figma, GIMP or PowerPoint (set slide size to 33.87 × 16.93 cm and export as PNG).

---

## Project colour palette

Taken directly from the web report's CSS custom properties — reuse them for slides, the social card and LinkedIn graphics so everything stays visually consistent.

| Role | Name | Hex | Use |
|------|------|-----|-----|
| Background | `--papier` | `#e9ebe6` | Page background (paper) |
| Background light | `--papier-clair` | `#f3f5f0` | Cards, panels |
| Text | `--encre` | `#12181a` | Body text (ink) |
| Text soft | `--encre-douce` | `#4b5551` | Secondary text |
| Accent | `--cyan` | `#00707f` | Links, primary accent |
| Accent bright | `--cyan-trait` | `#12a0b4` | Highlights, lines |
| Alert | `--rouge` | `#b3222a` | Emphasis, focus outline |
| Rule | `--trait` | `#c2c9c3` | Borders, separators |
| Rule strong | `--trait-fort` | `#8d9791` | Stronger borders |

---

## Typography

| Role | Family | Weights | Fallback |
|------|--------|---------|----------|
| Headings | **Barlow Condensed** | 600, 700, 800 | Arial Narrow, sans-serif |
| Body | **Inter** | 400, 500, 600 | system-ui, Segoe UI, sans-serif |
| Technical / data | **IBM Plex Mono** | 400, 500 | Consolas, monospace |

All three are free on [Google Fonts](https://fonts.google.com).

---

## Available images

| File | Content | Good for |
|------|---------|----------|
| `00-cover.jpg` | Cover / ArcGIS scene | Social card background, LinkedIn hero |
| `01-qgis-osm-extraction.jpg` | QGIS OSM layers | Methodology slide |
| `02-recap-point-cloud.jpg` | Point cloud, cutaway | Scan-to-BIM illustration |
| `03-blender-bonsai-ifc.jpg` | IFC tree in Blender | openBIM / interoperability slide |
| `04-qgis2threejs-lod1-loss.jpg` | LoD1 degradation | The "before/after" interoperability point |
| `05-gis-synthesis-map.jpg` | GIS synthesis map | Strong standalone visual, cartography skill |
| `06-gis-zoom-district.jpg` | District zoom | Detail shot |
| `07-revit-lod500-model.jpg` | Revit LOD 500 model | BIM skill demonstration |
| `08-lod500-in-context.jpg` | LOD 500 among LoD1 | **Best single image for LinkedIn** — the contrast is instantly legible |
| `09-video-thumbnail.jpg` | Video opening frame | Video link preview |
| `10-arcgis-final-scene.jpg` | Final scene, LoD1 blue | README hero, social card |
| `11-author-portrait.jpg` | Author portrait | About section, LinkedIn |

---

## LinkedIn image recommendations

| Post type | Size | Suggested file |
|-----------|------|----------------|
| Single image post | 1200 × 627 px | `08-lod500-in-context.jpg` |
| Carousel (PDF) | 1080 × 1350 px per page | Sequence: 05 → 02 → 07 → 04 → 10 |
| Article header | 1280 × 720 px | `10-arcgis-final-scene.jpg` |
| Featured section | 1200 × 627 px | Custom card with title overlay |

> **Tip:** a carousel following the project narrative (territory → cloud → model → the loss → the result) consistently outperforms a single screenshot on LinkedIn.

---

## Repository badges

Already present and fully configured in `README.md`:

```markdown
[![Live Demo](https://img.shields.io/badge/Live_Demo-GitHub_Pages-00707f?style=for-the-badge&logo=github)](https://benhassaneamine.github.io/geobim-tamansourt/)
[![License: MIT](https://img.shields.io/badge/License-MIT-b3222a?style=for-the-badge)](LICENSE)
```

Optional additions once the repository is live:

```markdown
![GitHub stars](https://img.shields.io/github/stars/benhassaneamine/geobim-tamansourt?style=social)
![GitHub last commit](https://img.shields.io/github/last-commit/benhassaneamine/geobim-tamansourt)
![GitHub repo size](https://img.shields.io/github/repo-size/benhassaneamine/geobim-tamansourt)
```
