# QingJian (青简)

> Simplicity to write, elegance to publish — an offline browser Markdown + HTML studio.

**The Lightweight Markdown Studio** · Pure front-end · No install · No network required · Fully offline.

QingJian is a ready-to-use Markdown editor: download a single HTML file, double-click, and start writing. It bundles mainstream Markdown extensions, LaTeX math, all Mermaid diagram types, ABC musical notation, chemical structure rendering, physics/chemistry/astronomy simulations, text-to-speech e-book reading, and an internet radio player. Every resource ships with the package and loads offline.

## Feature Highlights

| Area | Capabilities |
| --- | --- |
| Writing | Headings / emphasis / lists / tables / footnotes / task lists / definition lists / GitHub alerts / details / emoji / escaping |
| Math | Inline & block KaTeX, `mhchem` chemical equations, matrices, cases, aligned environments |
| Diagrams | All 24 Mermaid charts (flowchart, sequence, class, state, gantt, pie, mindmap, ER, journey, gitGraph, timeline, quadrant, sankey, …) |
| Modeling | PlantUML sequence / usecase / class (local offline fallback renderer) |
| Music | ABC staff notation + self-built WebAudio piano synth (play / pause / reset / rate / volume, karaoke-style note highlighting) |
| Custom blocks | `chart` function curves · `canvas-math` plotting · `smiles` molecular structures · `physim` / `chemsim` / `astrosim` interactive simulations (sliders / animation / pause-reset) |
| E-books | Open `.epub` (TOC + inline images + full preview), `.html` / `.txt` / `.doc` (read-only hint) |
| Read-aloud | Sentence-level TTS, karaoke-style highlight, rate / language / voice provider options (system / local / Edge online / Azure) |
| Radio | `radio` code block + local channel manager (m3u8 / mp3 / aac streams, localStorage, `.m3u` batch import) |
| Engineering | Split edit-preview, TOC / file tree, source line numbers + highlight + autocomplete, multi-tabs, recent files, PDF / HTML / Word export, image & media insert, folder open |
| Platform | PC / Android responsive (landscape & portrait, proportional scaling), standalone / split / modular builds |

## Quick Start

```bash
# Option 1: Standalone (recommended)
#   open dist/QingJian-standalone.html  (~12 MB, everything embedded)

# Option 2: Split build
#   open dist-split/QingJian-split.html  (~5 MB, needs ./assets/)

# Option 3: Modular project (development)
#   unzip QingJian-v14.21-modular.zip — see docs/ARCHITECTURE.md
```

> Runs directly under `file://` — no local server required. For folder-open / export features, use a modern browser (Chrome / Edge) for the best experience.

## Screenshots

![Editor overview](showcase-01-editor-overview.png)

![chart function curves](showcase-02-chart-curves.png)

![SMILES molecules](showcase-03-smiles-molecules.png)

![physim Maxwell & kinetics](showcase-04-physim-maxwell-kinetics.png)

![canvas-math plotting](showcase-05-canvas-math.png)

![chemsim simulation](showcase-06-chemsim.png)

![ABC staff notation](showcase-07-abc-staff.png)

![physim particle live demo](showcase-physim-live.gif)

## Docs

- [CAPABILITIES](docs/CAPABILITIES.md)
- [ARCHITECTURE](docs/ARCHITECTURE.md)
- [COMPLIANCE](docs/COMPLIANCE.md)
- [QUICK-START & FAQ](docs/QUICK-START.md)

## License

[MIT License](LICENSE)

Copyright (c) 2026 QingJian Contributors
