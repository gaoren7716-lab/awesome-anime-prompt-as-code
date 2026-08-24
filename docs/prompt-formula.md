# 7 层动漫 Prompt 公式

> 本仓库所有模板共享的底层方法论。Prompt 不是"100 个高级词的加法"，而是分层信息的组合。

## 公式

```text
主体
+ L1 基础体系
+ L2 流派/时代
+ L3 渲染质感
+ L4 光影
+ L5 镜头
+ L6 环境
+ L7 情绪
```

| 层级 | 功能 | 示例 | 数据文件 |
|---|---|---|---|
| 主体 | 谁/什么在画面里 | mature detective, torn photograph | `input_variables` + `subject` |
| L1 基础体系 | 定审美体系 | Japanese anime / Chinese donghua / cyberpunk anime | data/styles.json |
| L2 流派时代 | 定身份和年代 | shoujo manga style / 1990s anime / xianxia aesthetic | data/styles.json |
| L3 渲染质感 | 定媒介手感 | cel shading / semi-realistic anime / ink wash | data/materials.json |
| L4 光影 | 定第一层氛围 | golden hour / neon lighting / rim light | data/lighting.json |
| L5 镜头 | 定叙事视角 | medium shot / low angle / dynamic action shot | data/camera.json |
| L6 环境 | 定空间和剧情容器 | school rooftop / misty mountains / rainy street | data/environments.json |
| L7 情绪 | 定故事感 | nostalgic mood / tense atmosphere / epic mood | data/moods.json |

## 核心写作原则

1. 风格词决定"画面**像什么**"；材质词决定"画面像**怎么画出来**"。
2. 光影、镜头、环境、颜色、情绪决定"画面有没有故事"。
3. 每个词应有明确分工，避免同义词堆砌。
4. 同方向材质词可以强化；跨方向/相反的词会打架（见 [style-conflicts.md](style-conflicts.md)）。
5. 先定视觉中心，再选镜头、光影、环境和材质。

## 硬性纪律（Schema 已强制）

- **L7 情绪最多 2 个词**，且必须放在提示词最后；先让光影/镜头/环境说话，情绪只做点睛。
- **禁止裸情绪词**：不用 peaceful/warm/cozy/dreamy 这类孤立词，用 `peaceful atmosphere` / `melancholic mood` 组合形式。
- **镜头词不得混入光影字段**：shot/angle/composition 只属于 L5。
- **backlighting ≠ rim light**：前者整体逆光易成剪影，后者仅勾边缘用于分离背景。

## 记忆口诀

```text
先选基础质感，再选流派题材，最后补光影、镜头、环境、情绪。

风格词：画面像什么。    材质词：画面像怎么画出来。
镜头词：观众站在哪里看。环境词：故事在哪里发生。
光影和颜色：观众先感到什么。情绪词：最后只用 1—2 个定调。

同方向叠词 = 增强。矛盾方向混词 = 打架。

梦幻拍情绪。少女系拍人物。唯美幻想拍世界。
仙侠拍人靠近天空。武侠拍人走进江湖。
水墨：少即是多。工笔：细节即美。
```

## 从模板到成品的流程

1. 在 `prompts/` 找到目标模板 YAML；
2. 替换 `input_variables` 中带 `{{}}` 的变量；
3. 用 `data/negative-prompts.json` 组装负面清单；
4. 按 [model-guides.md](model-guides.md) 适配目标平台；
5. 按 `data/model-adapters.json` 的四段式交付格式输出。
