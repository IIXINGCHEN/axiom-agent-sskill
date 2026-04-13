# Changelog

## [21.1.0] - 2026-04-13

### Added

- **SKILL.md**: 分诊决策矩阵 — 4 维量化阈值（文件数/跨模块/安全/回滚）+ 3 条路由规则
- **SKILL.md**: 标准 E 降级条件 — 生命周期、安全路径、最低覆盖三维判定
- **SKILL.md**: 标准 F 可操作指标 — 避免 N+1、O(n²) 以上注释理由、外部调用设超时
- **SKILL.md**: 会话状态 XML 模板 — 7 字段 `AxiomOS_Session_State` 结构化快照格式
- **README.md**: 显式不适用声明表 — 5 个场景 + 原因 + 替代方案
- **INSTALL.md**: Windows PowerShell 一键安装脚本

### Changed

- **SKILL.md**: Self-Diagnostic 省略条件从模糊描述改为显式 required/skip 清单
- **SKILL.md**: 诚实边界从 8 条精简为 6 条（移除已解决的降级条件和不适用场景条目）
- **USAGE.md**: 诚实边界同步 SKILL.md 变更，交叉引用 README

---

## [21.0.1] - 2026-04-13

### Fixed

- **INSTALL.md**: 统一所有 URL 为 `axiom-agent-skill`（修复双 `s` 拼写和 Kiro 占位符）
- **INSTALL.md**: 符号链接路径与 git clone URL 保持一致
- **README.md**: 术语表 "12项不可妥协的交付要求" → "12项交付标准（10项刚性+2项推荐）"
- **README.md**: 外部依赖表新增"获取方式"列和使用注意事项
- **SKILL.md**: description 添加英文激活关键词，提升非中文请求匹配率
- **04-external-views.md**: "11项A-K" → "12项A-L"（反映 v20.2 新增的 L 标准）
- **06-timeline.md**: "11项交付标准" → "12项交付标准" 并标注 v20.2 来源

### Added

- **.gitignore**: 排除 `.claude/settings.local.json` 和 `.agents/` 运行时目录
- **CHANGELOG.md**: 本文件

---

## [21.0.0] - 2026-04-13

### Added

- 基于 29 个核心规范的深度蒸馏版 SKILL.md
- 6 个核心心智模型（通过三重验证）
- 14 条决策启发式（含来源证据）
- 量化表达 DNA（确定性 5.7:1，结构化 54%）
- Agentic Protocol（3 步回答工作流：先研究再回答）
- 5 对显式保留的内在矛盾
- 8 条诚实边界（每条有证据）
- 12 项生产级交付标准（含 v20.2 新增的 L 标准）
- 6 路并行调研文档（`references/research/01-06.md`）
- 三重验证过程记录（`references/extraction-notes.md`）
- 多平台安装指南（Claude Code / Codex CLI / Kiro IDE）
- 示例对话（8 场景，含 Agentic Protocol 演示）
