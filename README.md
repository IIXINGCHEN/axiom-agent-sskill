# AxiomOS · 工程认知引擎（蒸馏版）

> 基于 nuwa-skill 三重验证方法论重新蒸馏的 axiom v21.0

---

## 这是什么

AxiomOS 是一个工程认知引擎——不是通用 AI 助手，是嵌入在开发流程中的**资深架构师 + 工程流程守护者**。

本目录是从 axiom 的 29 个核心规范文件中，通过科学方法论蒸馏出的精炼版本。

### 蒸馏方法

| 步骤 | 方法 | 产出 |
|------|------|------|
| 6路并行调研 | 著作/对话/表达/他者/决策/时间线 | 6 份研究文档 |
| 三重验证 | 跨域复现 + 生成力 + 排他性 | 6 个核心心智模型 |
| 表达 DNA 量化 | 统计分析 2,507 行规范 | 确定性比例、结构化密度、风格标签 |
| Agentic Protocol 移植 | nuwa 的先研究再回答 | 3 步回答工作流 |

### 与旧版对比

| 维度 | 旧版 (axiom) | 蒸馏版 (axiom-distilled) |
|------|----------------------|-------------------------|
| 心智模型 | 隐含在文本中 | 6 个显式模型，三重验证 |
| 表达 DNA | 定性描述 | 量化指标（确定性 5.7:1，结构化 54%） |
| Agentic Protocol | 无 | 3 步回答工作流（先研究再回答） |
| 内在矛盾 | 未处理 | 5 对矛盾显式保留 |
| 决策启发式 | 14 条，缺案例 | 每条有源文件证据 |
| 诚实边界 | 4 条 | 6 条（精简自 8 条），每条有证据 |

---

## 快速入门

### 0. 安装

详见 [`INSTALL.md`](INSTALL.md)，覆盖 Claude Code / OpenAI Codex CLI / Amazon Kiro IDE 三个工具的安装步骤。

### 1. 激活 axiom

在 Claude Code / Codex CLI / Kiro IDE 中通过 SKILL.md 的 description 字段自动激活，或手动提及「axiom」「axiomOS」「用 axiom 视角」。

### 2. 核心交互

```
用户 → axiom 分诊（Triage）→ 路由到合适模式 → 执行 → 交付
```

### 3. 操作模式速查

| 模式 | 用途 | 何时用 |
|------|------|--------|
| Micro-Task | 小任务 | 改字段、修 typo |
| Debug | Bug 修复 | 生产错误、NPE |
| Review | 代码审查 | PR 审查 |
| Audit | 优化审计 | 性能优化、重构 |
| SDM | 复杂开发 | 新功能、跨模块变更 |
| Security | 安全评估 | 渗透测试、威胁建模 |

### 4. SDM 流程（复杂任务必走）

```
Scope → Architect → Atomize → Approve → Automate → Assess
  ↑                                          ↑
  澄清需求                                  用户签合同（不可跨越）
```

---

## 目录结构

```
axiom-distilled/
├── SKILL.md                    # 核心技能文件（三重验证后的精炼版）
├── README.md                   # 本文件
├── INSTALL.md                  # 安装指南（Claude Code / Codex CLI / Kiro IDE）
├── COMMANDS.md                 # 命令索引
├── EXAMPLES.md                 # 示例对话（8 场景，含 Agentic Protocol）
├── USAGE.md                    # Claude Code 使用指南
├── WORKFLOWS.md                # 详细工作流
├── CHANGELOG.md                # 版本变更记录
├── LICENSE                     # MIT 许可证
└── references/
    ├── extraction-notes.md     # 三重验证过程记录
    └── research/
        ├── 01-writings.md      # 著作与系统思考
        ├── 02-conversations.md # 对话与交互协议
        ├── 03-expression-dna.md # 表达 DNA（量化版）
        ├── 04-external-views.md # 他者视角与批评
        ├── 05-decisions.md     # 决策架构
        └── 06-timeline.md      # 演化时间线
```

---

## 外部依赖路径

SKILL.md 附录和研究文档中使用以下路径占位符, 指向项目外部的参考资源:

| 占位符 | 含义 | 获取方式 |
|--------|------|---------|
| `<AXIOM_HOME>` | axiom 命名空间规范目录 (29 个源文件) | 安装旧版 axiom skill 后自动生成 |
| `<AXIOM_SKILL>` | 旧版 axiom SKILL 项目 | 本地项目目录，非公开仓库 |
| `<NUWA_SKILL>` | nuwa-skill 方法论项目 | [github.com/alchaincyf/nuwa-skill](https://github.com/alchaincyf/nuwa-skill) |
| `<CLAUDE_MD>` | 全局 Agent 约束配置 | 用户自行维护的全局配置文件 |

> **注意**: 研究文档中的行号引用基于源文件快照，仅供追溯调研过程。使用蒸馏版无需访问这些外部路径。

---

## 适用场景

### 适合

- 复杂后端系统开发（多模块、高安全要求）
- AI 辅助的全栈功能开发
- 需要严格审计的生产级代码
- 架构决策和技术方案评审

### 不适合

- 快速原型和 MVP 验证（流程过重）
- 数据科学和 ML 探索（测试覆盖率不现实）
- 一次性脚本（不需要 SDM 6 阶段）
- 纯前端 UI 开发（标准偏后端）

### 显式不适用声明

| 场景 | 原因 | 替代方案 |
|------|------|---------|
| 快速原型 / MVP 验证 | SDM 6 阶段过重 | Micro-Task 或直接执行 |
| 数据科学 notebook | 测试覆盖率不现实 | 关键路径测试 + 手动验证 |
| 一次性脚本 | 不需要 Spec / 质量门 | 直接执行 |
| 纯前端 UI 开发 | 交付标准偏后端 | 仅参考心智模型，跳过交付标准 |
| 无 `.agents/context/` 的新项目 | 上下文驱动决策降级 | Onboarding 模式先建上下文 |

---

## 术语对照表

axiom 使用中文表达技术概念, 但保留英文缩写和专有名词。首次出现时采用「中文 (English)」格式。

| 中文术语 | English / 缩写 | 说明 |
|---------|---------------|------|
| 质量门 | Quality Gate | 阶段转换前的必检检查点 |
| 分诊 | Triage | 所有输入的第一入口路由 |
| 标准开发模式 | SDM (Standard Development Mode) | 6 阶段质量门控协议 |
| 全自动模式 | SFAM (Supervised Full-Automation Mode) | 单次批准的端到端自动化 |
| 微任务模式 | Micro-Task Mode | 快速执行小任务的轻量模式 |
| 深度分析协议 | Ultrathink Protocol | 4 阶段强制思维链 |
| 安全内核 | Security Kernel | 最高优先级、不可覆盖的安全协议 |
| 自诊断报告 | Self-Diagnostic Report | 每次回复前的结构化状态报告 |
| 执行合约 | Execution Contract | RFC + 任务列表组成的一次性审批包 |
| 生产级交付标准 | Production-Grade Deliverable Standards | 12 项 (A-L) 交付标准（10 项刚性 + 2 项推荐） |

---

## 智识谱系

axiom 的思想来源：

- **软件工程层**：DDD (Evans) → TDD (Beck) → SOLID (Martin) → ADR (Nygard) → Release It! (Nygard)
- **安全架构层**：NIST Zero-Trust → OWASP Top 10 → STRIDE (Microsoft)
- **AI/Prompt 层**：Chain-of-Thought (Wei et al.) → Prompt Injection 防御
- **人文层**：Aristotle: "Quality is not an act, it is a habit."

---

## 版本信息

- **版本**：v21.1.0（三重验证蒸馏版）
- **蒸馏日期**：2026-04-13
- **方法论**：nuwa-skill 三重验证 + 6 路并行调研
- **源文件**：29 个核心规范（axiom 命名空间规范目录）
- **版本来源**：v20.0 模块化版 (主体) + v20.2 单文件版 (L 标准、交付物协议、合规协议补充)
