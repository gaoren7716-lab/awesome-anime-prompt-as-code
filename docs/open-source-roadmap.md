# 开源路线图

## v0.1（当前版本）—— 结构与方法论完整发布

- [x] 7 层公式 Schema 化（anime-prompt / character-bible 两个 JSON Schema）
- [x] 分层词库：styles / materials / lighting / camera / environments / moods / characters / negative-prompts / model-adapters
- [x] 49 个 YAML 模板覆盖 10 大类：基础质感、日系、国漫、手绘水彩、游戏角色、特殊与欧美、电影叙事、唯美系、多角色同框、小说短剧应用
- [x] 8 个三平台适配完整案例
- [x] 模型适配指南（GPT-Image-2 无负向字段改写法、niji 默认、Flux 正向对冲）
- [x] 角色一致性协议 + 多角色不撞脸三板斧
- [x] Agent Skill（skills/anime-prompt-library）

## v0.2 —— 案例扩容与校验工具

- [ ] examples 扩至 20+（补齐档案中剩余案例：蓝调天台、逆光海报、末日废土等）
- [ ] `scripts/validate.js`：基于 JSON Schema 自动校验所有 YAML（层级纪律/冲突词/mood 数量）
- [ ] 基础质感补齐 illustration-anime 等独立模板
- [ ] 每模板配 1 张示例生成图（仅使用无版权争议的自生成图）

## v0.3 —— 社区共建

- [ ] 模板贡献指南细化 + PR 模板
- [ ] 风格标签索引页（按题材/情绪/镜头检索）
- [ ] GitHub Pages 静态浏览站升级（筛选器）
- [ ] 英文文档全量对齐

## v1.0 —— 稳定规范

- [ ] Schema 冻结为 1.0，向后兼容承诺
- [ ] 多语言（日/韩）README
- [ ] 与 awesome-gpt-image-2 等上游生态的互引

## 明确不做

- 不收录模仿特定在世画师/工作室精确风格的模板（用视觉特征描述替代）
- 不上传任何第三方版权角色图或未授权素材
- 不做需要 API Key 的在线服务（保持纯静态开源）
