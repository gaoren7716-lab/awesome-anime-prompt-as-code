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
- 🖼️ **Game-character pack, field-tested** — 4 combos with real generated previews & one-click copy: [docs/game-character-gallery.md](docs/game-character-gallery.md).

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
examples/      # full cases with per-platform adapted output (+ real previews)
docs/          # formula, conflicts, model guides, consistency, game-character gallery, roadmap
skills/        # Agent Skill
```

## License & Boundaries

- Prompt structures, vocabularies, docs and original cases: **MIT**.
- No templates imitating the precise style of living artists/studios; visual-feature descriptions instead.
- Community cases must declare source & authorization; third-party content remains with its owners.

Full rules: [CONTRIBUTING.md](CONTRIBUTING.md).

<div align="center">

**License**: MIT • **中文文档**: [README.zh-CN.md](README.zh-CN.md)



① 90年代校园怀旧

```
Japanese anime, 1990s anime, shoujo anime, retro cel animation,
hand-drawn lineart, golden hour, warm sunset light, medium shot,
Japanese high school rooftop, nostalgic mood, youthful atmosphere
```

适合：青春/校园题材

![90年代校园怀旧](https://github.com/gaoren7716-lab/awesome-anime-prompt-as-code/blob/main/90%E5%B9%B4%E4%BB%A3%E6%A0%A1%E5%9B%AD%E6%80%80%E6%97%A7.png?raw=true)



② 赛博朋克少女

```
cyberpunk anime, futuristic anime, semi-realistic anime, detailed rendering,
neon lighting, rim lighting, low angle shot, futuristic city, rainy street,
dark atmosphere, tense mood
```

适合：科幻/都市题材

![赛博朋克少女](https://github.com/gaoren7716-lab/awesome-anime-prompt-as-code/blob/main/%E8%B5%9B%E5%8D%9A%E6%9C%8B%E5%85%8B%E5%B0%91%E5%A5%B3.png?raw=true)

③ 国风仙侠

```
Chinese animation, xianxia aesthetic, Chinese cultivation fantasy,
ink wash, detailed brushwork, volumetric light, wide cinematic shot,
misty mountains, ancient Chinese architecture, mysterious atmosphere, epic mood
```

适合：古风/玄幻题材

![国风仙侠](https://github.com/gaoren7716-lab/awesome-anime-prompt-as-code/blob/main/%E5%9B%BD%E9%A3%8E%E4%BB%99%E4%BE%A0.png?raw=true)

④ 水墨武侠

```
Chinese ink wash animation, wuxia aesthetic, ink painting,
expressive brush strokes, traditional Chinese clothing, misty mountains,
negative space, dynamic martial arts pose
```

适合：武侠/江湖题材

![水墨武侠](https://github.com/gaoren7716-lab/awesome-anime-prompt-as-code/blob/main/%E6%B0%B4%E5%A2%A8%E6%AD%A6%E4%BE%A0.png?raw=true)

⑤ 治愈系日常

```
hand-drawn anime, soft watercolor texture, warm natural lighting,
pastel colors, medium shot, lush greenery, cozy environment,
peaceful atmosphere
```

适合：日常/慢生活题材

![治愈系日常](https://github.com/gaoren7716-lab/awesome-anime-prompt-as-code/blob/main/%E6%B2%BB%E6%84%88%E7%B3%BB%E6%97%A5%E5%B8%B8.png?raw=true)

⑥ 黑暗心理向

```
dark anime, mature character design, deep shadows, desaturated colors,
dramatic lighting, close-up shot, ruined buildings,
psychological atmosphere, tense mood
```

适合：悬疑/犯罪题材

![黑暗心理向](https://github.com/gaoren7716-lab/awesome-anime-prompt-as-code/blob/main/%E9%BB%91%E6%9A%97%E5%BF%83%E7%90%86%E5%90%91.png?raw=true)



</div>
