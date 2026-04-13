# AxiomOS 时间线与演化脉络调研

> **版本快照说明**: 本调研在 SKILL.md v20.2 时期完成。最终 SKILL.md 已升级至 v21.0 (三重验证蒸馏版), 本文件中的版本引用保留调研时的原始记录。

> Agent 6 调研成果 | 调研日期：2026-04-13
> 信息标注：`[一手]` = axiom 目录原文件 | `[二手]` = 现有研究 (2026-04-09) | `[推断]` = 基于多来源归纳

---

## 核心发现

AxiomOS 的演化呈现 4 个清晰阶段，每个阶段都有可追溯的版本标记和结构证据。从单体文件到 27 模块命名空间再到 SKILL.md 蒸馏，核心认知架构始终稳定，演化主要发生在**组织形式**和**运行时集成层**。

---

## 1. 宏观演化线

### 1.1 阶段总览表

| 阶段 | 时间点 | 形态 | 核心变化 | 认知突破 | 来源 |
|------|--------|------|----------|----------|------|
| **Phase 0: 单体** | 2024-01-12 之前 | `v20.0-legacy.md` 单文件 | 全部规范集中在一个 Markdown 文件中 | 建立了完整的认知引擎内核：优先级裁决、SDM 流程、10 种模式、交付标准 | `[一手]` README.md 版本信息 |
| **Phase 1: 模块化拆分** | 2024-01-12 `[推断]` | 27 个文件，7 大功能领域 | 单体拆分为 config/foundation/standards/modes/cognitive/protocols/commands 7 个子目录 | 认识到模块化可以独立加载、按需激活，降低 token 开销 | `[一手]` config/system.md "Version History: 20.0 (2024-01-12) - Modular architecture refactoring" |
| **Phase 2: 命名空间确立** | 2024-01-12 之后 `[推断]` | `_namespace.yaml` + Claude Code commands 系统 | axiom 成为 Claude Code 的一个正式命令命名空间，支持 `/axiom:view`、`/axiom:activate` 等交互 | 从"文档规范"进化为"可交互的命令系统"，规范可以直接被 Agent 调用 | `[一手]` _namespace.yaml |
| **Phase 3: SKILL 蒸馏** | 2026-04-09 前后 `[推断]` | SKILL.md 单文件 (~280 行) + COMMANDS.md 索引 + 6 份研究报告 | 将 27 模块的精髓蒸馏为统一认知引擎入口；SKILL.md 保留核心，细节委托回源文件 | 核心洞察：Agent 需要的不是冗长的规范全集，而是一个**决策入口点**，细节按需加载 | `[一手]` SKILL.md "v20.2" |
| **Phase 4: CLAUDE.md 集成** | 2026-04-09 之后 `[推断]` | CLAUDE.md 作为全局 Agent 约束 | axiom 的规则被融入更通用的 "Chief Practical Software Engineering Agent" 身份，增加了工程流程约束 | axiom 的认知架构从"专用规范"转化为"Agent 内禀能力"，不再需要显式激活 | `[二手]` CLAUDE.md 对比分析 |

### 1.2 演化路径图

```
v20.0-legacy.md (单体, 估计 2000+ 行)
  │
  │ 拆分日期: 2024-01-12  [一手]
  ▼
27 模块文件 + _namespace.yaml (v20.0.0)
  │
  │ 73 文件体系  [二手] 旧版 axiom 项目研究提及
  │ → 实际验证: axiom 命名空间下 27 个 .md 文件  [一手]
  │ → 推断: "73 文件"指整个命令体系,
  │         axiom 是其中一个命名空间
  ▼
SKILL.md (v20.2) + COMMANDS.md 索引 + references/research/
  │
  │ CLAUDE.md 中的工程流程约束
  ▼
Chief Practical Software Engineering Agent (全局集成)
```

---

## 2. 版本标记

### 2.1 已确认的版本标记表

| 位置 | 版本号 | 说明 | 来源 |
|------|--------|------|------|
| `_namespace.yaml` > `version` | `"20.0.0"` | 命名空间配置版本 | `[一手]` |
| `_namespace.yaml` > `config.system_version` | `"20.0"` | 系统级版本声明 | `[一手]` |
| `config/system.md` > `<constants>` | `SYSTEM_VERSION: 20.0` | 运行时引用的常量 | `[一手]` |
| `config/system.md` > frontmatter `version` | `"20.0.0"` | 模块级版本 | `[一手]` |
| `foundation/context.md` > frontmatter `version` | `"20.1.0"` | **唯一高于 20.0 的模块** | `[一手]` |
| `foundation/role.md` > frontmatter `version` | `"20.0.0"` | 模块级版本 | `[一手]` |
| 其余 24 个模块 > frontmatter `version` | `"20.0.0"` | 统一版本标记 | `[一手]` |
| `SKILL.md` > 标题 | `v20.2` | SKILL 蒸馏版本 | `[一手]` |
| `README.md` > 标题 | `v20.0` | README 维持旧版本 | `[一手]` |
| `README.md` > 版本信息段落 | `20.0` / 拆分日期 `2024-01-12` / 原文件 `v20.0-legacy.md` | 历史记录 | `[一手]` |

### 2.2 版本不一致分析

| 现象 | 推断 |
|------|------|
| `_namespace.yaml` 和 `config/system.md` 仍为 `20.0`，但 SKILL.md 已到 `v20.2` | `[推断]` SKILL.md 的蒸馏是一次独立演化，源模块文件未同步更新版本号 |
| `context.md` 的版本为 `20.1.0`，其余全部 `20.0.0` | `[推断]` context.md 可能经历过一次独立修订（增加 Context Evolution 段落） |
| README.md 标题仍为 `v20.0` | `[一手]` 确认 README 未随 SKILL.md 更新 |

---

## 3. 微观执行时间线

### 3.1 SDM 6 阶段时间线

| 阶段 | 时间标记 | 输出 | 质量门 | 来源 |
|------|----------|------|--------|------|
| **T0: Scope** | 任务开始 | RFC 草案 (Overview/Goals/Non-Goals/Acceptance Criteria) | 用户确认 Goals 和 Non-Goals | `[一手]` modes/sdm.md |
| **T1: Architect** | Scope 通过后 | 完整 RFC (含 12 个标准段落) | 架构符合 `.agents/context/` 原则 | `[一手]` modes/sdm.md |
| **T2: Atomize** | Architect 通过后 | TASK 文档 + DAG 依赖图 | 任务总和覆盖所有 RFC 需求，无循环依赖 | `[一手]` modes/sdm.md |
| **T3: Approve** | Atomize 通过后 | 合同签署确认 | 用户显式批准 (**不可跨越**) | `[一手]` modes/sdm.md |
| **T4: Automate** | Approve 通过后 | 生产级代码 + 测试 | 100% 测试通过，无占位代码 | `[一手]` modes/sdm.md |
| **T5: Assess** | Automate 完成后 | 验证报告 + `.agents/context/` 更新提议 | 100% 满足验收标准 | `[一手]` modes/sdm.md |

### 3.2 Bug 修复时间线

| 阶段 | 时间标记 | 动作 | 来源 |
|------|----------|------|------|
| **T0** | Issue 接收 | `gh issue view` 获取问题详情 | `[二手]` |
| **T1** | 代码定位 | 搜索代码库 (grep/search) | `[二手]` |
| **T2** | 历史审查 | `git log` 审查变更历史 | `[二手]` |
| **T3** | 根因分析 | RCA 分析 | `[二手]` |
| **T4** | RCA 文档 | `docs/rca/issue-X.md` | `[二手]` |
| **T5** | 实施 | 基于 RCA 的修复 | `[二手]` |
| **T6** | 验证 | 测试 + 提交 | `[二手]` |

### 3.3 验证时间线

```
validation:validate → validation:code-review → validation:code-review-fix
    → validation:execution-report → validation:system-review
       ↓                ↓                  ↓                ↓
    文件输出          文件输出           终端执行         文件输出
```

### 3.4 会话生命周期

```
Start
  → Self-Diagnostic Report (每次回复前动态生成)
  → Context Sync (需要时发出 CONTEXT_REQUEST XML)
  → Mode Activation (Triage 路由)
  → Task Execution (SDM/SFAM/Micro-Task/...)
  → Progress Reporting (YAML 格式)
  → Session Serialization (中断 >30 分钟时)
  → End
```

### 3.5 渐进式 Spec 时间线

| 复杂度 | 触发条件 | 流程 | 来源 |
|--------|----------|------|------|
| 简单 | 改字段、修 bug | 直接执行，无需 Spec | `[一手]` SKILL.md |
| 中等 | 3+ 步骤，有架构决策 | 轻量 Spec + HARD-GATE 后编码 | `[一手]` SKILL.md |
| 复杂 | 跨模块、多系统 | 完整 RFC → HARD-GATE → 实现 → Review → 交付 | `[一手]` SKILL.md |

---

## 4. 知识沉淀机制

### 4.1 `.agents/context/` 更新机制

| 触发点 | 动作 | 规则 | 来源 |
|--------|------|------|------|
| SDM Phase 6 Assess | 提议更新 `.agents/context/` | **质量门要求**，不是可选 | `[一手]` modes/sdm.md |
| 重大架构决策 | 新增 ADR 到 `.agents/context/architecture/adr/` | 需经过 Review/Approve 流程 | `[一手]` foundation/context.md |
| 新设计模式发现 | 更新 `.agents/context/architecture/patterns.md` | SDM Assess 阶段主动提议 | `[一手]` modes/sdm.md |
| 安全经验积累 | 更新 `.agents/context/security/` | 安全评估后的知识固化 | `[一手]` modes/security.md |
| 性能洞察 | 更新 `.agents/context/config/` | 性能测试后的参数调优记录 | `[一手]` foundation/context.md |

### 4.2 知识沉淀流程

```
Task Completion (SDM Phase 6 Assess)
  │
  ├─ 新模式? → .agents/context/architecture/patterns.md
  ├─ ADR?    → .agents/context/architecture/adr/NNN-*.md
  ├─ 安全?   → .agents/context/security/
  ├─ 性能?   → .agents/context/config/
  └─ 领域?   → .agents/context/domain/
       │
       ▼
  Context Update Proposal (结构化模板)
       │
       ▼
  Review → Approval → Commit
```

### 4.3 Assess 阶段的知识沉淀要求

来自 `modes/sdm.md` Phase 6 `[一手]`：

- Chain-of-Thought 回顾：什么做得好？什么困难？是否有偏离？为什么？
- 新设计模式识别
- 架构决策记录
- 领域模型澄清
- 性能考量发现
- **质量门**：核心知识**必须**提议沉淀到 `.agents/context/`

### 4.4 CLAUDE.md 增加的沉淀机制

CLAUDE.md 增加了 3 个独立于 `.agents/context/` 的知识沉淀通道 `[二手]`：

| 通道 | 文件 | 用途 | 来源 |
|------|------|------|------|
| 失败记录 | `tasks/cmd_blacklist.md` | 记录系统性/环境性/可复现的命令失败 | `[二手]` CLAUDE.md |
| 经验教训 | `tasks/lessons.md` | 记录长期偏好、架构约束、环境特征 | `[二手]` CLAUDE.md |
| 执行轨迹 | `tasks/plan_<slug>_<YYYYMMDD>.md` | 计划文件含 Failure Log 段落 | `[二手]` CLAUDE.md |

---

## 5. CLAUDE.md 带来的增量

### 5.1 CLAUDE.md 新增规则（axiom 中不存在或更弱）

| 增量规则 | axiom 中的对应 | CLAUDE.md 的变化 | 来源 |
|----------|----------------|------------------|------|
| **Startup Preflight** | axiom 无此概念 | 新增：每个任务开始前确保 `tasks/` 存在，读取 blacklist 和 lessons | `[二手]` CLAUDE.md |
| **TDD by default** | axiom 要求 test-first (SDM Phase 5) | CLAUDE.md 明确 Red→Green→Refactor 循环，增加验证替代方案 | `[二手]` |
| **复杂度护栏** | axiom 有 SOLID 要求但无数值约束 | CLAUDE.md 增加：函数 15 行、嵌套 3 层的默认目标 | `[二手]` |
| **依赖纪律** | axiom H-7 "复用现有 > 引入新依赖" | CLAUDE.md 增加引入新依赖的 3 条证据要求 | `[二手]` |
| **失败阈值** | axiom H-5 "3 连败 → Replan" | CLAUDE.md 扩展：3 连败→Replan, 5 总败或 2 Replan→决策报告 | `[二手]` |
| **Approval Gate 细化** | axiom SDM Phase 4 Approve 是不可跨越的质量门 | CLAUDE.md 细化：仅破坏性/范围扩展/非局部变更/高影响依赖需显式批准；普通 bugfix 自主进行 | `[二手]` |
| **双重 DELETE 确认** | axiom 有此规则 | CLAUDE.md 增加更详细的 7 步确认流程和模板 | `[二手]` |
| **Plan File 模板** | axiom 的 RFC 是 Plan 的一种形式 | CLAUDE.md 增加结构化模板含 Metadata/Context/RCA/Validation/Failure Log | `[二手]` |
| **Definition of Done** | axiom 通过 SDM 质量门隐含 | CLAUDE.md 显式列出 6 条完成条件 | `[二手]` |
| **Communication Contract** | axiom 有表达 DNA | CLAUDE.md 增加：结论先行结构、半角标点、不用填充词 | `[二手]` |

### 5.2 CLAUDE.md 如何改变 axiom 行为

| 方面 | 变化 | 效果 |
|------|------|------|
| **执行节奏** | 增加 Startup Preflight | 每个任务多一步"检查任务目录"，降低重复犯错 |
| **自主性边界** | Approval Gate 细化 | 小任务可自主推进，不再所有变更都需要批准 |
| **失败恢复** | 失败阈值量化 | 明确何时停止重试、何时生成报告，避免无限循环 |
| **代码质量** | 复杂度护栏数值化 | 函数 15 行、嵌套 3 层提供可量化的审查标准 |
| **知识管理** | 3 通道沉淀 (blacklist/lessons/plan) | 知识不再只进 `.agents/context/`，运行时失败也被记录 |
| **工作流整合** | CLAUDE.md 是全局约束 | axiom 规则通过 SKILL 按需激活，CLAUDE.md 始终生效 |

---

## 6. 演化中的关键决策

### 6.1 从 27 模块到 SKILL.md 的取舍

| 类别 | 保留 | 丢弃/弱化 | 理由 |
|------|------|-----------|------|
| **优先级裁决** | 5 级优先级完整保留 | - | 核心中枢，所有决策的基础 |
| **SDM 流程** | 6 阶段完整保留，含质量门 | 具体示例代码删除 | 流程结构是核心，示例是辅助 |
| **10 种操作模式** | 模式表保留 | 每个模式的详细实现委托回源文件 | 模式名称和触发词足够路由，细节按需加载 |
| **11 项交付标准** | 标准表格保留 | 每项标准的详细 Requirements 列表 | 标准名称和一句话描述足够理解，详细要求回源文件查 |
| **Ultrathink** | 4 阶段框架保留 | 模式选择 (Autonomous/Collaborative) 细节 | 核心是思维链，执行模式是可选参数 |
| **Self-Diagnostic** | YAML 模板保留 | - | Agent 自省的关键机制 |
| **Security Kernel** | 概念保留到 SKILL.md 的"核心约束" | 具体的 XML 标签 (`<AxiomOS_Core_Instructions>`) | 安全原则保留，XML 边界标签是运行时细节 |
| **Context Protocol** | `.agents/context/` 核心概念保留 | CONTEXT_REQUEST XML 模板和详细目录结构 | 概念保留，具体 XML 格式委托回源文件 |
| **会话状态管理** | 30 分钟中断阈值保留 | XML 快照格式细节 | 阈值是核心，格式是实现细节 |

### 6.2 演化决策总结

| 决策 | 选择 | 拒绝的替代 | 理由 |
|------|------|-----------|------|
| **组织形式** | SKILL.md 作为入口，源文件作为参考 | 全部内容压缩到一个文件 | 入口需要轻量，细节按需加载 |
| **版本策略** | SKILL.md 独立版本 (v20.2)，源文件维持 v20.0 | 全部统一到 v20.2 | 避免大面积无实质意义的版本号变更 |
| **知识体系** | axiom 的 `.agents/context/` + CLAUDE.md 的 `tasks/` | 统一到单一知识库 | 不同类型的知识需要不同的生命周期管理 |
| **模式激活** | 通过 SKILL 自动激活或用户显式调用 | 始终加载全部模式 | token 效率：按需加载优于全量加载 |

---

## 7. 时间线启发式

```
IF 新会话开始       → 加载状态 + Self-Diagnostic Report
IF 长任务中断 (>30m) → 序列化会话状态为 XML 快照
IF 上下文不足       → 发出 CONTEXT_REQUEST XML, 禁止假设
IF 上下文压缩       → 生成 context-summaries
IF 任务完成         → 提议更新 .agents/context/ + 更新 tasks/
IF 阶段门控未通过   → 回退，不前进
IF 3 次同根因失败   → Replan
IF 5 次总失败       → 停止 + 生成决策报告
IF 规则冲突         → Safety > Verify > Convention > Simple > Speed
```

---

## 8. 规范的时间性质

AxiomOS 体系有一个独特的性质：**静态核心 + 动态应用 + 受控演化**。

| 性质 | 说明 | 来源 |
|------|------|------|
| 规范本身静态 | 源文件自 2024-01-12 以来版本号未变 (`20.0.0`) | `[一手]` frontmatter |
| 应用流程动态 | 根据任务类型选择模式，根据复杂度选择 Spec 深度 | `[一手]` SKILL.md |
| 演化受控发生 | 通过 `.agents/context/` 的 Update Proposal 流程 | `[一手]` foundation/context.md |
| CLAUDE.md 补充运行时层 | 增加 tasks/ 通道和工程流程约束，不修改 axiom 源文件 | `[二手]` |
| SKILL.md 是蒸馏产物 | 保留认知内核，委托实现细节 | `[一手]` |

**关键洞察**：axiom 的设计哲学是"规范不可自动演化"——所有变更必须经过人类 Review/Approve。但规范的使用是智能路由的：简单任务走快通道，复杂任务走完整流程。这种"静态核心 + 动态分派"的设计平衡了一致性和灵活性。

---

## 附录：版本标记完整清单

| 文件路径 | frontmatter version | 备注 |
|----------|---------------------|------|
| `_namespace.yaml` | `20.0.0` | 命名空间配置 |
| `config/system.md` | `20.0.0` | 系统常量 |
| `config/security.md` | `20.0.0` | 安全内核 |
| `config/compliance.md` | `20.0.0` | 合规协议 |
| `foundation/role.md` | `20.0.0` | 角色定义 |
| `foundation/principles.md` | `20.0.0` | 核心原则 |
| `foundation/context.md` | **`20.1.0`** | 唯一高版本 |
| `standards/deliverable.md` | `20.0.0` | 交付标准 |
| `standards/artifact.md` | `20.0.0` | 制品协议 |
| `modes/_overview.md` | `20.0.0` | 模式总览 |
| `modes/triage.md` | `20.0.0` | 分流协议 |
| `modes/sdm.md` | `20.0.0` | SDM 流程 |
| `modes/sfam.md` | `20.0.0` | 全自动模式 |
| `modes/audit.md` | `20.0.0` | 审计模式 |
| `modes/security.md` | `20.0.0` | 安全模式 |
| `modes/debug.md` | `20.0.0` | 调试模式 |
| `modes/review.md` | `20.0.0` | 审查模式 |
| `modes/onboarding.md` | `20.0.0` | 启动模式 |
| `modes/micro-task.md` | `20.0.0` | 微任务模式 |
| `modes/enhancement.md` | `20.0.0` | 增强模式 |
| `cognitive/session.md` | `20.0.0` | 会话管理 |
| `cognitive/ultrathink.md` | `20.0.0` | 深度思考 |
| `protocols/interaction.md` | `20.0.0` | 交互协议 |
| `protocols/tools.md` | `20.0.0` | 工具协议 |
| `commands/view.md` | `20.0.0` | 查看命令 |
| `commands/activate.md` | `20.0.0` | 激活命令 |
| `commands/status.md` | `20.0.0` | 状态命令 |
| `commands/load-all.md` | `20.0.0` | 加载命令 |
| `SKILL.md` | **`v20.2`** (标题) | 蒸馏版本，无 frontmatter |
| `README.md` | `v20.0` (标题) | 未随 SKILL 更新 |
