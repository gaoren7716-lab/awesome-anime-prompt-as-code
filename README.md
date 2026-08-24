<div align="center">

# awesome-anime-prompt-as-code

**Structured, model-agnostic anime image prompting library for GPT-Image-2, Midjourney, Flux, SDXL and more.**

Characters, art styles, materials, lighting, camera, environment and narrative — decomposed into reusable **Prompt protocols (Anime Prompt as Code)**.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Templates](https://img.shields.io/badge/Templates-49-blueviolet)](prompts/)
[![Styles](https://img.shields.io/badge/Styles-40+-blue)](data/styles.json)

[📖 中文文档](README.zh-CN.md) | [🌐 Homepage](https://gaoren7716-lab.github.io/awesome-anime-prompt-as-code/)

</div>

---

## Not another "100 magic words" list

Most prompt libraries copy nice sentences. This project **engineers** anime visual language:

- 🧩 **7-Layer Formula as Schema** — subject + L1 base system + L2 genre/era + L3 rendering/material + L4 lighting + L5 camera + L6 environment + L7 mood. Each layer is independently searchable, composable, and validatable.
- 🎨 **Anime visual language library** — Japanese anime, Chinese donghua (xianxia / ink-wash / gongbi), hand-drawn & watercolor, game character art, cyberpunk / mecha / horror / post-apocalyptic, western animation. 40+ style anchors.
- 🎬 **Camera & narrative library** — first frames, novel covers, short-drama storyboards, two-character standoffs, emotional close-ups, establishing shots.
- 👥 **Multi-character scene control** — the anti-same-face triad: hair contrast × silhouette contrast × explicit positioning, plus emotional-opposition templates.
- 🔁 **Character consistency protocol** — Character Bible freezes anchors; no drift across scenes.
- 🔌 **Model adapter layer** — one YAML, auto-adapted to GPT-Image-2 / Midjourney niji / Flux / SDXL / Jimeng / Kling.
- 🤖 **Agent Skill** — drop `skills/anime-prompt-library` into Claude Code / Cursor.

> Positioning: inspired by [awesome-gpt-image-2](https://github.com/freestylefly/awesome-gpt-image-2)'s structured approach — but their axis is UI/commercial/infographics. **Anime, donghua camera language and narrative first-frame control are this repo's axis.**

## Quick Start

### 1. Copy a template

Open any YAML under `prompts/`, replace `{{variables}}`, then adapt per `docs/model-guides.md`.

### 2. Install as an Agent Skill

```bash
npx skills add gaoren7716-lab/awesome-anime-prompt-as-code --skill anime-prompt-library --global --yes --copy
```

Then just ask: *"Use anime-prompt-library to compose a rainy-night standoff with two characters."*

### 3. Validate your own templates

```bash
ajv validate -s schemas/anime-prompt.schema.json -d your-template.yaml --all-errors
```

## The 7-Layer Formula

| Layer | Role | Example |
|---|---|---|
| Subject | who/what is in frame | mature detective, torn photograph |
| L1 Base system | aesthetic family | Japanese anime / Chinese donghua |
| L2 Genre/era | identity & period | seinen manga style / 1990s anime |
| L3 Rendering | medium feel | cel shading / ink wash |
| L4 Lighting | first mood layer | golden hour / neon lighting |
| L5 Camera | viewer position | low angle / extreme wide shot |
| L6 Environment | story container | rainy street / misty mountains |
| L7 Mood | story feeling (≤2 words, last) | quiet tension |

## Three traps we already solved for you

1. **GPT-Image-2 has NO negative prompt field** — negatives must be rewritten as natural-language constraints ("Do not include: ..."). Conversion rules live in `data/model-adapters.json`.
2. **Anime on Midjourney = `--niji 6`**, not `--v`.
3. **Conflicting material words fight each other** — e.g. `cel shading + soft blending`. All verified conflict pairs are in [docs/style-conflicts.md](docs/style-conflicts.md) and flagged inline via each template's `conflicts:` field.

## Repository Layout

```text
data/          # 9 layered vocabularies (JSON)
schemas/       # JSON Schemas: anime-prompt + character-bible
prompts/       # 49 YAML templates in 10 categories
examples/      # full cases with per-platform adapted output
docs/          # formula, conflicts, model guides, consistency, roadmap
skills/        # Agent Skill
```

## License & Boundaries

- Prompt structures, vocabularies, docs and original cases: **MIT**.
- No templates imitating the precise style of living artists/studios; visual-feature descriptions instead.
- Community cases must declare source & authorization; third-party content remains with its owners.

Full rules: [CONTRIBUTING.md](CONTRIBUTING.md).

<div align="center">

**License**: MIT • **中文文档**: [README.zh-CN.md](README.zh-CN.md)

</div>
