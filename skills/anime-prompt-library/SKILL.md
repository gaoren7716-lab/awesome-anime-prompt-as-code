---
name: anime-prompt-library
description: Compose, adapt, and validate structured anime image prompts using the 7-layer formula. Use when the user wants to create anime/donghua/manga style image prompts, needs platform-specific versions (GPT-Image-2 / Midjourney niji / Flux / SDXL / 即梦/可灵), wants multi-character scene control, or needs character consistency anchors for novels, short dramas, and game art.
---

# Anime Prompt Library

Structured anime prompt generation based on the **7-Layer Formula**:

```
主体 + L1 基础体系 + L2 流派/时代 + L3 渲染质感 + L4 光影 + L5 镜头 + L6 环境 + L7 情绪
```

## When This Skill Activates

User asks to: 写动漫提示词 / 生成二次元绘图 prompt / 小说封面 / 短剧首帧 / 角色立绘 / 角色卡 / 多角色同框 / 跨平台适配提示词（GPT-Image-2、MJ、Flux、SDXL、即梦、可灵）。

## Workflow

### Step 1 — Identify intent
Classify the request into one of:
- **风格图**（单角色/场景）→ pick template from `prompts/01`~`08`
- **多角色同框** → `prompts/09-multi-character-scenes/`
- **小说封面/短剧首帧/关系图** → `prompts/10-novel-and-short-drama/`
- **角色一致性项目** → build a character bible first (`schemas/character-bible.schema.json`, examples in `data/characters.json`)
- **已有 prompt 优化** → run Step 4 validation, fix conflicts

### Step 2 — Load vocabulary
Read only the data files needed:
- `data/styles.json` — style anchors (L1/L2/L3)
- `data/materials.json` — texture words + conflict pairs
- `data/lighting.json`, `data/camera.json`, `data/environments.json`, `data/moods.json` — cinematography layers
- `data/negative-prompts.json` — negative lists per style family

### Step 3 — Compose
1. Pick the closest template YAML; replace `{{variables}}`.
2. Respect layer order: subject → style(L1..L3) → lighting → camera → environment → mood.
3. Mood: **max 2 words**, placed last, never bare words (use "quiet tension" not "tension").
4. Check `conflicts:` field and `docs/style-conflicts.md`.

### Step 4 — Validate
Before output, check:
- [ ] No conflicting material words co-occur (cel shading + soft blending = fail)
- [ ] No cross-system mixing (anime sparkling eyes + bold ink halftone = fail)
- [ ] Camera words not inside lighting layer
- [ ] mood_en length ≤ 2
- [ ] Negative list present and adapted per platform

### Step 5 — Adapt to platform
Per `data/model-adapters.json`:
- **GPT-Image-2**: natural language paragraph; negatives rewritten as "Do not include: ..."; can render title text directly.
- **Midjourney**: `--niji 6 --ar {ratio} --no {top negatives}` (max 8 items).
- **SDXL**: tags + native negative field; steps 30, cfg 6.
- **Flux**: long sentences; positive counter-descriptions instead of negatives.
- **即梦/可灵**: Chinese OK; separate negative box.

### Step 6 — Deliver (fixed four-part format)

```text
中文说明        ← 一句话：这是什么、适合什么场景
英文正向提示词   ← 平台适配后
英文负面提示词   ← 平台策略转换后
参数建议        ← 比例/steps/cfg/版本后缀
```

## Hard Rules

1. 不擅自删除用户已确认的人物锚点、画风锚点、负面词、有效参数；冲突时先说明冲突，再给「保守兼容版」和「风格强化版」两个选项。
2. 未被指定的部分默认继承最终确认版。
3. 多角色必须写明站位（left/right/center/back to camera）+ 发型/轮廓差异，negative 禁 identical faces。
4. 不生成模仿特定在世画师精确风格的模板。

## Quick References

- 公式详解: docs/prompt-formula.md
- 冲突表: docs/style-conflicts.md
- 平台适配: docs/model-guides.md
- 角色一致性: docs/character-consistency.md
