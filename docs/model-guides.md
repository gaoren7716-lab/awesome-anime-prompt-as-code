# 模型适配指南

> 同一份 YAML 模板 = 同一个视觉意图。适配层负责把它翻译成各平台的"母语"。完整规则见 `data/model-adapters.json`。

## 一张表看懂

| 平台 | 提示词风格 | 负面词策略 | 关键差异 |
|---|---|---|---|
| **GPT-Image-2** | 自然语言指令段 | ⚠️ 无负向字段 → 改写为 "Do not include: ..." 追加句 | 文字渲染强，可直接生成书名/招牌文字；无需权重与采样参数 |
| **Midjourney Niji**（动漫默认） | 标签流 + 后缀 | `--no a, b, c`（取前 6-8 条） | 动漫一律 `--niji 6` 而非 `--v`；比例 `--ar 16:9` |
| **Midjourney v7** | 标签流 + 后缀 | `--no ...` | 仅写实/厚涂概念图用 `--v 7 --style raw` |
| **Flux** | 长自然语言段落 | 无负向通道 → 正向对冲描述（如 "five fingers on each hand"） | guidance 3.0-4.0，过高过饱和 |
| **SDXL / 二次元底模** | 标签逗号分隔 | ✅ 原生 negative prompt 字段，逐条映射 | steps 28-35, cfg 5-7, DPM++ 2M Karras |
| **即梦 / 可灵** | 可直接中文 | 中文负面输入框 | 锚点词翻译为对应中文即可 |

## 三个最容易踩的坑

### 1. GPT-Image-2 没有 negative prompt 字段
它是指令模型。把 YAML 的 `negative_prompt` 数组翻译成自然语言约束追加在末尾：

```text
Do not include: text, watermark, extra fingers, chibi features.
```

同时善用它最强的能力——画面内文字：

```text
...with the title "剑挑山河" rendered in elegant Chinese calligraphy at the top.
```

### 2. 动漫题材 Midjourney 应该用 niji 不是 v
`--niji 6` 对 anime 词汇原生友好；`--v 7` 更适合写实/概念图。

### 3. MJ 的 `--no` 不要塞太多
超过 8 条会稀释权重。优先级：解剖错误 > 文字水印 > 风格禁区 > 其他。

## 统一交付格式（四段式）

所有平台输出统一走这个格式（继承项目交接规则）：

```text
中文说明        ← 一句话：这是什么、适合什么场景
英文正向提示词   ← 按平台风格转换后
英文负面提示词   ← 按平台策略转换后
参数建议        ← 比例/steps/cfg/版本后缀
```

## 适配示例

以 `examples/detective-rainy-alley.yaml` 为例，同一意图的三种输出见该文件内的 `gpt_image_2` / `midjourney_niji` / `sdxl` 三段。
