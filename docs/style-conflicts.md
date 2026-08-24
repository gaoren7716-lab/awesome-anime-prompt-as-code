# 风格冲突规则

> 同方向叠词 = 增强；矛盾方向混词 = 打架。本文件列出已验证的冲突对，Schema 校验与人工检查均以此为据。

## 材质冲突（最高频翻车点）

| 冲突组合 | 原因 |
|---|---|
| `clean lineart` + `rough lineart` | 线稿方向相反 |
| `cel shading` + `soft blending` | 硬边分色 vs 柔融混合 |
| `flat colors` + `rich brush strokes` | 平涂 vs 厚涂笔触 |
| `watercolor washes` + `hard shadows` | 水彩没有硬阴影 |
| `polished rendering` + `heavy film grain` | 精修 vs 重颗粒 |

## 体系冲突（跨文化审美）

| 不要混 | 说明 |
|---|---|
| 日系词 × 强美漫词 | 日系重细腻线条/眼神/情绪；欧美重形体/强轮廓/光影对比 |
| `large sparkling eyes` / `soft pastel` / `clean anime lineart` × `bold ink lines` / `halftone texture` | 少女系 × 美漫画是典型打架 |

## 风格专属禁区

| 风格 | 避免使用 |
|---|---|
| 手绘家族 | clean/perfect lineart, sharp outlines, ultra polished, hyper detailed |
| 赛璐璐 | soft shading, subtle gradients, soft blending, rich brush strokes |
| 水墨 | vibrant saturated colors, thick outlines, cel shading, dense urban background |
| 工笔 | rough brush strokes, abstract washes, negative space composition |
| 少女漫/少女系 | realistic proportions, gritty realism, hard shadows |
| 青年漫/悬疑 | chibi, large sparkling eyes, pastel colors |
| 复古80年代 | modern polished rendering, digital gradients, neon colors |
| teal and orange | 不适用于水彩、绘本、少女漫、工笔——它们有自己的色彩逻辑 |

## 已验证安全组合

```text
现代商业二次元：clean lineart + soft shading + subtle gradients + polished rendering
传统赛璐璐：    clean lineart + flat colors + cel shading + hard shadows
手绘绘本：      organic linework + watercolor washes + paper texture + soft pigments
复古旧番：      rough hand-drawn lineart + muted colors + analog texture + subtle film grain
游戏原画：      painterly rendering + rich brush strokes + textured painting + canvas texture
```

## 光影易混点

- `backlighting`：人物整体逆光，易形成剪影。
- `rim light`：仅边缘勾亮，利于从背景分离。
- 黑暗系避免"一团死黑"：必须给次级光源（cold moonlight / candlelight glow / cold rim light）。

## 提交新模板时的自查

1. L3 字段内是否同时出现了两个相反方向的材质词？
2. 是否混用了日系+欧美体系的核心锚点？
3. 情绪是否超过 2 个词？是否有裸情绪词？
4. 冲突信息是否写入了 YAML 的 `conflicts:` 字段？
