# 角色一致性协议

> 让同一个角色在 10 张图里长同一张脸。核心工具：`schemas/character-bible.schema.json` + `data/characters.json`。

## 为什么需要角色圣经

多场景叙事（小说封面、短剧分镜、角色卡）最大的敌人是**漂移**：发型变了、衣服换了、脸对不上了。角色圣经把"不能变的东西"冻结成锚点，把"可以变的东西"显式开放。

## 角色圣经结构

```yaml
id: cold-detective-v1
name_zh: 冷峻型男主
anchors:                    # ← 冻结区：每个字都不许动
  identity: mature private detective
  appearance_en:
    - sharp jawline
    - deep-set eyes
    - restrained expression
  outfit_en:
    - tailored charcoal overcoat
    - leather gloves
  signature_props_en:
    - torn photograph
  expression_range_en:      # 允许的表情范围
    - restrained and tense
    - quietly angry
    - exhausted calm
  forbidden_en:             # 绝不允许出现
    - bright cheerful smile
    - casual hoodie
style_binding:              # 绑定画风，跨图不变
  base_system: [dark anime, seinen manga style]
  rendering: [semi-realistic anime, detailed rendering]
consistency_rules:
  - "锚点块原文复制进每一条 prompt，不做同义改写"
  - "先出 3 张定妆照确认锚点有效，再批量生产"
```

## 三条实战规则

### 1. 锚点块原文复制
每次使用时把 `appearance_en` + `outfit_en` **逐词原样**拼入 prompt。改写一个词（如 charcoal → dark grey）就可能引发漂移。

### 2. 先定妆，后量产
新角色先用同一模板生成 3 张不同角度/光线的"定妆照"。三张都稳定，才进入批量生产；不稳定就回炉修改锚点词。

### 3. 变量只动"可变区"
| 可变（每张图不同） | 不可变（锚点） |
|---|---|
| 镜头、光影、环境、情绪、动作 | 发型发色、五官特征、服装、标志道具 |

## 多角色不撞脸三板斧

配合 `prompts/09-multi-character-scenes/` 使用：

1. **发型对比**：短发×长发、黑发×白发——最容易被模型读取的差异。
2. **服装轮廓对比**：大衣×开衫、盔甲×长袍。
3. **站位与姿态声明**：显式写 "on the left / on the right / back to camera"，并在 negative 里禁 `identical faces, same hairstyle`。

## 与模板的关系

- 单角色场景 → 把锚点块填入模板的 `subject` 字段。
- 关系图/全员立绘 → 用 `prompts/10-novel-and-short-drama/relationship-map.yaml`，每个角色一段锚点。
- 待补充资料清单见仓库 README「角色一致性项目启动包」一节（对应原档案第 16 节）。
