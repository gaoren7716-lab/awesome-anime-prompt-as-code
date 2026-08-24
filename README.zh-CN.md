<div align="center">

# awesome-anime-prompt-as-code

**面向 GPT-Image-2 及通用图像模型的动漫提示词结构化模板库**
**Structured, model-agnostic anime image prompting library**

把角色、画风、材质、光影、镜头、环境和叙事拆成可复用的 **Prompt 协议（Anime Prompt as Code）**。

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Templates](https://img.shields.io/badge/Templates-49-blueviolet)](prompts/)
[![Styles](https://img.shields.io/badge/Styles-40+-blue)](data/styles.json)
[![Schemas](https://img.shields.io/badge/Schemas-2-orange)](schemas/)
[![Homepage](https://img.shields.io/badge/Homepage-GitHub_Pages-success)](https://gaoren7716-lab.github.io/awesome-anime-prompt-as-code/)

</div>

---

## 这不是又一份"100 个高级词合集"

现有提示词库大多是把好句子抄下来。本项目做的是把动漫视觉语言**工程化**：

- 🧩 **7 层公式 Schema 化** —— 主体 + L1 基础体系 + L2 流派/时代 + L3 渲染质感 + L4 光影 + L5 镜头 + L6 环境 + L7 情绪，每层可独立检索、组合、校验
- 🎨 **动漫视觉语言库** —— 日漫、国漫（仙侠/水墨/工笔）、手绘水彩、游戏立绘、赛博机甲恐怖末日、欧美动画，40+ 风格锚点
- 🎬 **镜头与叙事库** —— 角色首帧、小说封面、短剧分镜、双人对峙、情绪特写、建立镜头
- 👥 **多角色同框控制** —— 不撞脸三板斧（发型对比 × 轮廓对比 × 站位声明）+ 情绪对立模板
- 🔁 **角色一致性协议** —— Character Bible 冻结锚点，跨场景不漂移
- 🔌 **模型适配层** —— 同一 YAML 自动适配 GPT-Image-2 / Midjourney niji / Flux / SDXL / 即梦 / 可灵
- 🤖 **Agent Skill** —— `skills/anime-prompt-library` 可直接装入 Claude Code / Cursor 等 Agent 使用
- 🖼️ **游戏角色四件套实测画廊** —— 真实生成图预览 + 一键复制提示词：[docs/game-character-gallery.md](docs/game-character-gallery.md)

> 差异化定位：参考 [awesome-gpt-image-2](https://github.com/freestylefly/awesome-gpt-image-2) 的结构化思路，但其主轴是 UI/商业图/信息图；**动漫、国漫漫画镜头语言与剧情首帧控制是本仓库的主轴**。

## 快速开始

### 方式一：直接复制模板

```bash
# 1. 找到目标风格模板
prompts/03-chinese-donghua/xianxia.yaml

# 2. 替换 {{variables}} 变量
# 3. 按 docs/model-guides.md 适配你的平台
```

<details>
<summary><b>示例：仙侠模板 → GPT-Image-2 输出</b></summary>

```text
A sword cultivator standing on a floating cliff,
Chinese donghua, xianxia aesthetic, Chinese cultivation fantasy,
semi-realistic painterly rendering,
volumetric light, soft mystical glow, wide cinematic shot,
misty mountains, ancient Chinese architecture, ethereal epic atmosphere.
Do not include: text, watermark, western fantasy armor.
```
</details>

### 方式二：作为 Agent Skill 安装

```bash
npx skills add gaoren7716-lab/awesome-anime-prompt-as-code --skill anime-prompt-library --global --yes --copy
```

然后直接说："用 anime-prompt-library 给我配一个雨夜对峙的双人镜头"。

### 方式三：Schema 校验你的自定义模板

```bash
ajv validate -s schemas/anime-prompt.schema.json -d your-template.yaml --all-errors
```

## 目录结构

```text
awesome-anime-prompt-as-code/
├─ data/                      # 分层词库（9 个 JSON）
│  ├─ styles.json             # 40+ 风格条目（L1/L2/L3 锚点）
│  ├─ materials.json          # 材质词典 + 已验证组合 + 冲突表
│  ├─ lighting.json           # 光影维度（含 backlighting vs rim light 辨析）
│  ├─ camera.json             # 镜头维度
│  ├─ environments.json       # 环境维度
│  ├─ moods.json              # 情绪维度（≤2 词纪律）
│  ├─ characters.json         # 角色设计模板
│  ├─ negative-prompts.json   # 负面词库（按风格家族）
│  └─ model-adapters.json     # 平台转换规则 + 四段式交付格式
├─ schemas/                   # JSON Schema（格式基石）
│  ├─ anime-prompt.schema.json
│  └─ character-bible.schema.json
├─ prompts/                   # 49 个 YAML 模板（10 大类）
├─ examples/                  # 完整案例（三平台适配输出 + 真实预览图）
├─ docs/
│  ├─ prompt-formula.md       # 7 层公式教学
│  ├─ style-conflicts.md      # 风格冲突规则（避坑核心）
│  ├─ model-guides.md         # 平台适配指南
│  ├─ character-consistency.md# 角色一致性协议
│  ├─ game-character-gallery.md # 游戏角色四件套实测画廊（图片+一键复制）
│  └─ open-source-roadmap.md  # 路线图
└─ skills/anime-prompt-library/SKILL.md   # Agent Skill
```

## 核心方法论：7 层公式

| 层级 | 功能 | 示例 |
|---|---|---|
| 主体 | 谁/什么在画面里 | mature detective, torn photograph |
| L1 基础体系 | 定审美体系 | Japanese anime / Chinese donghua |
| L2 流派时代 | 定身份和年代 | seinen manga style / 1990s anime |
| L3 渲染质感 | 定媒介手感 | cel shading / ink wash |
| L4 光影 | 定第一层氛围 | golden hour / neon lighting |
| L5 镜头 | 定叙事视角 | low angle / extreme wide shot |
| L6 环境 | 定空间和剧情容器 | rainy street / misty mountains |
| L7 情绪 | 定故事感（≤2 词，放最后） | quiet tension, psychological suspense |

完整教学见 [docs/prompt-formula.md](docs/prompt-formula.md)。

## 三条最容易踩的坑（我们帮你规避了）

1. **GPT-Image-2 没有 negative prompt 字段** —— 负面词必须改写为 "Do not include: ..." 自然语言约束（`data/model-adapters.json` 已内置转换规则）。
2. **动漫题材 Midjourney 应该用 `--niji 6`** 而非 `--v`。
3. **矛盾材质词互相打架** —— `cel shading + soft blending` 这类组合直接毁图；所有已验证冲突对见 [docs/style-conflicts.md](docs/style-conflicts.md)，模板内 `conflicts:` 字段就地标注。

## 模板总览

| 分类 | 数量 | 代表模板 |
|---|---:|---|
| 基础质感 | 7 | standard-japanese, cel-shading, soft-shading |
| 日系经典 | 5 | retro-1980s, shoujo, seinen, shonen-battle |
| 东方国漫 | 6 | xianxia, ink-wash-wuxia, gongbi, eastern-fantasy |
| 手绘水彩 | 5 | watercolor-anime, storybook, pencil-sketch |
| 游戏角色 | 4 | gacha-standing, jrpg-card, battle-dynamic |
| 特殊与欧美 | 8 | cyberpunk-anime, mecha, horror, western-comic |
| 电影级叙事 | 5 | film-still, golden-hour-rooftop, backlit-poster |
| 唯美系 | 3 | dreamy, girl-system, beautiful-fantasy |
| 多角色同框 ⭐ | 3 | interrogation-room, rainy-duel, protagonist-trio |
| 小说短剧应用 ⭐ | 3 | novel-cover-xianxia, short-drama-first-frame |

⭐ = 本仓库差异化重点（多数提示词库未覆盖的应用层）

## 版权与使用边界

- 提示词结构、词库、文档、原创案例按 **MIT** 开源。
- 不收录模仿特定在世画师/工作室精确风格的模板；使用视觉特征描述替代。
- 社区贡献案例须声明来源与授权状态；第三方内容版权归属原作者，商用前自行确认。
- 详见 [CONTRIBUTING.md](CONTRIBUTING.md) 与 [LICENSE](LICENSE)。

## 致谢

- 方法论启发：[freestylefly/awesome-gpt-image-2](https://github.com/freestylefly/awesome-gpt-image-2)（Prompt as Code 思路）
- 全部风格词库、冲突规则与案例源自本项目原创整理的动漫 Prompt 创作实践。

## Star 历史

觉得有用请点个 Star ⭐ ，这是持续更新的最大动力。

[![Star History Chart](https://api.star-history.com/svg?repos=gaoren7716-lab/awesome-anime-prompt-as-code&type=Date)](https://star-history.com/#gaoren7716-lab/awesome-anime-prompt-as-code&Date)

<div align="center">

**License**: MIT • **Homepage**: [gaoren7716-lab.github.io/awesome-anime-prompt-as-code](https://gaoren7716-lab.github.io/awesome-anime-prompt-as-code/)

</div>
