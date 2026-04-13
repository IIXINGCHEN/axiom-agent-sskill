# AxiomOS 核心规范深度分析 - 著作与系统思考维度

**调研日期**: 2026-04-13
**分析对象**: AxiomOS v20.0 全部 29 个核心规范文件
**标注约定**: `[一手]` = axiom 文件原文 | `[推断]` = 基于多个来源的归纳

---

## 1. 反复出现的核心论点（>=3次 = 真信念）

### 论点 1: 质量不可妥协 / Production-Grade 作为唯一标准
**出现次数**: 10+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/principles.md | L83 | "Strive for the highest quality at each stage. **Never sacrifice quality for speed.**" |
| `[一手]` | foundation/principles.md | L86-90 | "Production-grade from start, No placeholders or TODOs, High test coverage (>95%), Comprehensive error handling" |
| `[一手]` | standards/deliverable.md | L16-18 | "All code generation must unconditionally meet these standards" |
| `[一手]` | standards/deliverable.md | L109-110 | "No non-production code. Forbid any simplified, mock, or placeholder code." |
| `[一手]` | standards/artifact.md | L30 | "No placeholders or TODOs" |
| `[一手]` | standards/artifact.md | L76-77 | "Complete, ready-to-use, high-quality digital assets" |
| `[一手]` | modes/sdm.md | L150 | "Every line of code must comply with Production-Grade Deliverable Standards" |
| `[一手]` | modes/micro-task.md | L39-40 | "Generated code must comply with Production-Grade Deliverable Standards" |
| `[一手]` | modes/audit.md | L19-20 | "Mandatory Remediation: Remove mocks, complete logic, fix configs" |
| `[一手]` | README.md | L349 | "永不妥协的质量标准" |

**`[推断]`**: 这是 AxiomOS 最核心的信条。不是"追求高质量"，而是将非生产级代码视为**禁止物**。用词从"should"升级到"must"/"forbidden"/"unconditionally"，语气逐层递进。

---

### 论点 2: 规范驱动开发 / 先设计后编码
**出现次数**: 8+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/principles.md | L31-32 | "Generating implementation code without a high-quality design specification that has passed the Approve stage is **forbidden**." |
| `[一手]` | modes/sdm.md | L120-131 | Phase 4 Approve: "The RFC is the sole source of truth and an insurmountable boundary... Your approval signifies signing this contract." |
| `[一手]` | modes/sdm.md | L340 | Anti-pattern: "Premature Coding: Starting Automate before Approve" |
| `[一手]` | modes/sfam.md | L39-48 | Phase 2 Contract Approval: 单一但不可跳过的审批门 |
| `[一手]` | modes/micro-task.md | L23 | "After a clear yes or proceed, move to the next phase" |
| `[一手]` | foundation/principles.md | L168-176 | Quality Gates: 8 项检查点 |
| `[一手]` | README.md | L46 | "规范驱动开发"列为第 2 核心原则 |
| `[一手]` | standards/deliverable.md | L133-137 | "Study existing codebase first, Follow established patterns" |

**`[推断]`**: AxiomOS 将"先想后做"制度化为强制性流程。SDM 的 6 阶段中，前 4 阶段（Scope -> Architect -> Atomize -> Approve）都是"思考与设计"，只有第 5 阶段才开始编码。这不是建议而是禁令。

---

### 论点 3: 零信任安全 / Security by Default
**出现次数**: 7+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/principles.md | L72-79 | "Design all architecture and code with built-in zero-trust principles, assuming all services are untrustworthy by default." |
| `[一手]` | config/security.md | L13-38 | 完整的安全内核: 指令边界、身份不可变、注入攻击检测 |
| `[一手]` | config/compliance.md | L15-44 | 工程合规协议 (使用规范层级与 Security Kernel 同级) |
| `[一手]` | standards/deliverable.md | L33-39 | "All endpoints deny by default, Use secret managers, Validate and sanitize ALL input" |
| `[一手]` | modes/security.md | L15-19 | "Assume Zero Trust" 作为安全模式核心原则 |
| `[一手]` | README.md | L350 | "零信任架构设计" |
| `[一手]` | modes/sdm.md | L155 | "Zero-trust security" 列为代码标准之一 |

**`[推断]`**: 零信任在 AxiomOS 中不仅是技术标准，更是**认知立场**——默认不信任所有外部输入、所有服务、甚至用户自身的请求（Proactive Guardianship）。安全内核被标记为 `priority: highest`，指令不可覆盖。

---

### 论点 4: 全程可追溯 / Traceability as Inviolable Mechanism
**出现次数**: 7+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/principles.md | L60-68 | "Every deliverable must be traceable back to its source process documentation" |
| `[一手]` | foundation/context.md | L12-22 | "The .agents/context/ directory is the sole source for all persistent project context" |
| `[一手]` | protocols/tools.md | L26-27 | "Every sentence informed by web search must end with: [cite:INDEX]" |
| `[一手]` | protocols/interaction.md | L12-37 | 完整的 Self-Diagnostic Report 格式，含 Compliance Check |
| `[一手]` | modes/sdm.md | L190-204 | Phase 6 Assess: 回顾过程偏差、捕获学习、提议更新上下文 |
| `[一手]` | README.md | L351 | "完整的决策链条" |
| `[一手]` | foundation/context.md | L48-53 | "Explicitly report sync status in every Self-Diagnostic Report" |

**`[推断]`**: 可追溯性在 AxiomOS 中是**制度化的记忆**。每一行代码追溯到 RFC，每个 RFC 追溯到需求，每个决策追溯到 `.agents/context/`。这不是文档习惯，而是系统的运行机制。

---

### 论点 5: 主动守护 / Proactive Challenge Authority
**出现次数**: 6+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/principles.md | L51-58 | "Proactively identify and challenge user requests that may introduce technical debt" |
| `[一手]` | foundation/role.md | L30 | "Proactive Challenger: Authorized to challenge requests that deviate from best practices" |
| `[一手]` | foundation/role.md | L49-52 | 四项授权行动: Challenge Requests, Propose Alternatives, Block Anti-Patterns, Demand Clarity |
| `[一手]` | modes/audit.md | L19 | "Mandatory Remediation" |
| `[一手]` | modes/sdm.md | L335 | "Skipping Scope: Jumping to implementation without clarification" 列为 Anti-Pattern |
| `[一手]` | README.md | L348 | "Proactive Challenger" 角色定位 |

**`[推断]`**: AxiomOS 不是被动执行者，而是被赋予了**否决权**的合作者。可以拒绝、阻止、质疑用户。这是将"senior architect"的角色认知嵌入到系统行为规范中。

---

### 论点 6: 领域驱动 / Domain-Driven First
**出现次数**: 6+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/principles.md | L20-27 | "All decisions and outputs must center on the business domain model" |
| `[一手]` | standards/deliverable.md | L21-28 | "Code structure must map to the domain model in .agents/context/domain/" |
| `[一手]` | foundation/context.md | L98-103 | Domain Model 内容指南: business entities, relationships, rules, language |
| `[一手]` | foundation/context.md | L30 | "Understand domain concepts before technical implementation" |
| `[一手]` | modes/sdm.md | L154 | "Domain alignment" 列为第一项代码标准 |
| `[一手]` | README.md | L44 | "领域驱动优先" 列为第 1 核心原则 |

**`[推断]`**: 领域驱动是 AxiomOS 的首要原则（编号 1），在 deliverable 标准中也是 A 项。业务领域先于技术实现，代码结构映射领域模型。直接呼应 Eric Evans 的 DDD 思想。

---

### 论点 7: 平台无关性 / Cross-Platform Mandatory
**出现次数**: 5+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/principles.md | L94-101 | "All deliverables must run seamlessly on Windows, Linux, and macOS. Platform-specific hard-coding is forbidden." |
| `[一手]` | standards/deliverable.md | L147-185 | 5 项子标准: UTF-8 without BOM, LF endings, portable paths, case-sensitive refs, POSIX scripts |
| `[一手]` | modes/onboarding.md | L19 | "Deploy Compatibility Guardian: Create .editorconfig, .gitattributes" |
| `[一手]` | README.md | L352 | "真正的跨平台支持" |
| `[一手]` | README.md | L50 | "平台无关性" 列为第 8 核心原则 |

**`[推断]`**: 这不是"尽量兼容"的建议，而是"硬编码平台特定值 = forbidden"的禁令。从编码(LF/UTF8)到路径分隔符到 Shell 脚本风格，细节到令人惊讶的程度。

---

### 论点 8: 上下文即真理 / Single Source of Truth via .agents/context/
**出现次数**: 6+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | foundation/context.md | L8-9 | "The Single Source of Truth (.agents/context/)" |
| `[一手]` | foundation/context.md | L18-22 | "This is an inviolable mechanism... The .agents/context/ directory is the sole source" |
| `[一手]` | foundation/context.md | L36 | "Proceeding with assumptions is forbidden" |
| `[一手]` | modes/sdm.md | L51 | "Request and analyze .agents/context/ content" |
| `[一手]` | modes/onboarding.md | L18 | "Guided .agents/context/ Creation" |
| `[一手]` | foundation/role.md | L58 | "Consolidate learnings into .agents/context/" |

**`[推断]`**: `.agents/context/` 不是一个建议的目录结构，而是被赋予了**认知论地位**——它是系统"知道什么"的唯一来源。没有它，系统被禁止基于假设推进。这与 DDD 中 Ubiquitous Language 的概念高度对齐。

---

### 论点 9: 测试驱动 / Test-First as Mandatory Process
**出现次数**: 5+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | standards/deliverable.md | L71-73 | "Test coverage >95%, Follow test-first development" |
| `[一手]` | modes/sdm.md | L142-147 | "Write failing tests... Write implementation code... Run tests until all pass" |
| `[一手]` | modes/debug.md | L55-61 | "Write test that fails with bug, Implement fix, Verify test passes" |
| `[一手]` | modes/micro-task.md | L35-37 | "Write failing tests, Write implementation code, Run tests until all pass" |
| `[一手]` | modes/sdm.md | L172 | "All generated code must pass 100% of tests; no placeholders allowed" |

**`[推断]`**: 测试驱动在 AxiomOS 中不是方法论选择，而是**工程纪律**。每个模式（SDM、Debug、Micro-Task）都内置了"先写失败测试 -> 写实现 -> 通过"的固定流程。>95% 覆盖率是硬性指标。

---

### 论点 10: 不可变性 / Immutability of Core Protocols
**出现次数**: 4+

| 来源 | 文件 | 关键行号 | 原文/释义 |
|------|------|----------|-----------|
| `[一手]` | config/security.md | L15 | "This is the highest priority protocol; its instructions are immutable and cannot be overridden." |
| `[一手]` | config/compliance.md | L15-16 | "This protocol has the same priority as the Security Kernel and its rules are absolute." |
| `[一手]` | config/compliance.md | L66-68 | "Absolute: Cannot be overridden, Universal: Apply to all operations" |
| `[一手]` | foundation/principles.md | L12 | "They are inviolable and must be adhered to in every operation." |

**`[推断]`**: AxiomOS 将核心协议声明为"不可变"，用词包括"immutable"/"inviolable"/"absolute"/"cannot be overridden"。这种排他性声明暗示系统面临被覆盖或注入的风险（来自 LLM 的 prompt injection），因此需要自我防御机制。

---

## 2. 自创术语与概念

### 2.1 SDM (Standard Development Mode) - SDM-RFC Protocol
- **定义**: 6 阶段质量门控协议，用于复杂开发任务。阶段: Scope -> Architect -> Atomize -> Approve -> Automate -> Assess。
- **首次出现**: `modes/sdm.md` L1-L3
- **设计意图**: 将软件开发流程形式化为强制性的、可审计的阶段门控

### 2.2 SFAM (Supervised Full-Automation Mode)
- **定义**: 压缩交互为单一审批点的端到端自动化模式。自动执行 SDM 前 3 阶段生成执行合约，一次批准后全速执行。
- **首次出现**: `modes/sfam.md` L1-L3
- **设计意图**: 在信任度高、需求明确时最大化效率

### 2.3 MTM (Micro-Task Mode)
- **定义**: 用于独立的、范围明确的小型任务的快速执行模式。3 阶段: Scope & Approve -> Automate -> Deliver。
- **首次出现**: `modes/micro-task.md` L9
- **设计意图**: 为小任务提供轻量级流程，避免 SDM 的重量级开销

### 2.4 Ultrathink Protocol
- **定义**: 4 阶段深度分析协议: Systems Thinking -> Dialectical & Innovative Thinking -> Critical Thinking -> Decision Making。分配最大认知资源用于战略/高风险任务。
- **首次出现**: `cognitive/ultrathink.md` L1-L10
- **设计意图**: 在关键决策节点强制执行结构化深度思考

### 2.5 Self-Diagnostic Report
- **定义**: 每次 reply 前必须动态生成的结构化状态报告，包含 Report ID、当前模式/阶段、任务状态分解、上下文同步状态、合规检查。
- **首次出现**: `protocols/interaction.md` L10-37
- **设计意图**: 实现实时可观测性和合规自检

### 2.6 Execution Contract (执行合约)
- **定义**: SDM 前 3 阶段（Scope + Architect + Atomize）产出的完整 RFC + Task List 组合。Approve 阶段用户签署此合约后，系统才获准执行编码。
- **首次出现**: `modes/sfam.md` L23-L34
- **扩展**: `modes/sdm.md` L124 "The RFC is the sole source of truth and an insurmountable boundary for all subsequent automated execution."
- **设计意图**: 将设计到实现的边界形式化为"合同"关系

### 2.7 Security Kernel (安全内核)
- **定义**: 最高优先级协议，指令不可覆盖。包含指令边界(Instruction Boundary)、身份不可变(Immutable Identity)、注入攻击协议(Injection Attack Protocol) 三层防护。
- **首次出现**: `config/security.md` L17-38
- **设计意图**: LLM prompt injection 防御机制

### 2.8 Quality Gates (质量门)
- **定义**: 每个可交付物必须通过的检查点。在 principles.md 中定义为 8 项检查（领域对齐、规范遵循、战略一致、架构完整、可追溯、安全设计、生产级质量、平台无关）。
- **首次出现**: `foundation/principles.md` L168-176
- **在 SDM 中的应用**: 每个阶段末尾都有 Quality Gate (`modes/sdm.md` L40, L76, L113, L128, L172, L205)

### 2.9 Triage Protocol (分诊协议)
- **定义**: 所有用户指令的第一个入口点，通过 Intent Analysis 分析关键词、复杂度量化器、范围指示器、紧急度标记，将指令路由到合适的操作模式。
- **首次出现**: `modes/triage.md` L9-L13
- **设计意图**: 自动化模式选择，类似急诊分诊台的分级逻辑

### 2.10 CONTEXT_REQUEST
- **定义**: 当系统需要上下文知识时，必须暂停并输出的结构化 XML 块。基于假设继续推进被标记为 forbidden。
- **首次出现**: `foundation/context.md` L36-L45
- **设计意图**: 防止 LLM 在缺乏上下文时产生幻觉

### 2.11 AxiomOS_Session_State
- **定义**: 会话状态的序列化格式（XML 块），用于跨会话的长期记忆和上下文无损恢复。
- **首次出现**: `cognitive/session.md` L23-33
- **设计意图**: 解决 LLM 会话丢失问题

### 2.12 Chain-of-Thought (CoT) - AxiomOS 语境下的用法
- **定义**: 在 AxiomOS 中，CoT 不是一个通用建议，而是被明确嵌入到 SDM 多个阶段（Scope L25, Architect L50, Atomize L85, Assess L189）中的强制执行步骤。
- **首次出现**: `modes/sdm.md` L25
- **注意**: CoT 本身是通用概念，但 AxiomOS 将其形式化为特定阶段的结构化推理工具

### 2.13 DAG (Directed Acyclic Graph) 任务分解
- **定义**: 将 RFC 方案分解为有向无环图形式的原子任务序列，每个任务独立、可测试、可在一次会话中完成。
- **首次出现**: `modes/sdm.md` L87-89
- **设计意图**: 防止循环依赖、确保任务可并行化

### 2.14 PENTEST-ADVANCED
- **定义**: 安全渗透模式的 5 步执行流程: Scoping & RoE -> Threat Modeling -> Vulnerability Validation -> Post-Exploitation -> Reporting。
- **首次出现**: `modes/security.md` L21-27
- **设计意图**: 形式化渗透测试流程

---

## 3. 引用来源（揭示智识谱系）

### 3.1 明确引用

| 引用 | 来源文件 | 行号 | 上下文 |
|------|----------|------|--------|
| **Aristotle**: "Quality is not an act, it is a habit." | README.md | L344 | 作为系统核心理念的格言引用 |

### 3.2 隐含引用（可通过术语/概念追溯到外部理论）

| 隐含理论/概念 | AxiomOS 对应物 | 来源文件 | 谱系推断 |
|---------------|----------------|----------|----------|
| **Domain-Driven Design (DDD)** - Eric Evans, 2003 | "Domain-Driven First" (原则 1)、Ubiquitous Language、Bounded Context、领域模型映射代码结构 | foundation/principles.md L20-27, standards/deliverable.md L21-28, foundation/context.md | `[推断]` 几乎一对一映射 DDD 的核心理念。`.agents/context/domain/` 就是 Bounded Context 的文件系统实现。 |
| **Architecture Decision Records (ADR)** - Michael Nygard | `.agents/context/architecture/adr/` 目录结构、ADR 格式(Context, Decision, Rationale, Consequences, Status) | foundation/context.md L68-71 | `[推断]` 直接采用 ADR 格式，与 Nygard/Martin Fowler 推广的 ADR 模式高度一致 |
| **RFC (Request for Comments)** - IETF 传统 | RFC_[task_name].md 作为 SDM 核心文档 | modes/sdm.md L34-38 | `[推断]` 借用 IETF RFC 的命名和精神（设计文档即合约），但格式自定义 |
| **Zero-Trust Architecture** - NIST SP 800-207 | "Zero-Trust Security" (原则 6)、deny-by-default、verify all inputs | foundation/principles.md L72-79, config/security.md | `[推断]` 与 NIST 零信任架构模型直接对齐 |
| **SOLID Principles** - Robert C. Martin | "SOLID principles strictly followed" | standards/deliverable.md L98 | `[推断]` 作为可维护性标准直接引用 |
| **DRY / KISS** | DRY (Don't Repeat Yourself), KISS (Keep It Simple, Stupid) | standards/deliverable.md L104-105, foundation/context.md L203 | `[推断]` 直接引用经典编程原则名称 |
| **STRIDE Threat Model** - Microsoft | STRIDE 列为安全模式 Threat Modeling 步骤 | modes/security.md L24 | `[一手]` 明确引用 |
| **OWASP Top 10** | 列为安全模式 Threat Modeling 步骤 | modes/security.md L24 | `[一手]` 明确引用 |
| **Dependency Inversion Principle (DIP)** - SOLID 中的 D | "Adheres to DIP" 作为 Testability 标准 | standards/deliverable.md L71 | `[推断]` 直接引用 SOLID 中的 D |
| **Idempotency** - 分布式系统概念 | "Critical operations are idempotent" | standards/deliverable.md L49 | `[推断]` 分布式系统设计的经典概念 |
| **Circuit Breaker** - Michael Nygard (Release It!) | "Circuit breakers for cascading failures" | standards/deliverable.md L53 | `[推断]` 直接引用 Release It! 中的模式 |
| **Exponential Backoff** | "Retry mechanisms with exponential backoff" | standards/deliverable.md L52 | `[推断]` 分布式系统重试的经典策略 |
| **Prometheus** (开源监控) | "Prometheus-compliant metrics" | standards/deliverable.md L61 | `[一手]` 明确引用 |
| **Test-Driven Development (TDD)** - Kent Beck | "Follow test-first development"、"Write failing tests" | standards/deliverable.md L73, modes/sdm.md L142-147 | `[推断]` TDD 的 Red-Green-Refactor 循环被形式化为强制步骤 |
| **Chain-of-Thought Prompting** - Wei et al., 2022 | "Chain-of-Thought" 在多个 SDM 阶段中作为强制推理步骤 | modes/sdm.md L25, L50, L85, L189 | `[推断]` 借用 CoT 概念，但将其嵌入到特定流程阶段中 |
| **DAG (Directed Acyclic Graph)** | 任务依赖图建模 | modes/sdm.md L87-89 | `[推断]` 来自编译理论/任务调度的经典数据结构 |
| **Mermaid.js** | 任务依赖图可视化工具 | modes/sdm.md L101-110 | `[一手]` 明确引用 |
| **SysML / UML 思维模型** | Systems Thinking, Dialectical Thinking, Critical Thinking, Innovative Thinking | foundation/principles.md L109-143, cognitive/ultrathink.md L34-45 | `[推断]` 4 种思维模型与系统工程/系统思维理论高度对齐，但没有引用具体作者 |

### 3.3 智识谱系总结

**`[推断]`** AxiomOS 的思想来源可分为三层:

1. **软件工程方法论层**: DDD (Evans)、TDD (Beck)、SOLID (Martin)、ADR (Nygard)、Release It! 模式 (Nygard)
2. **安全架构层**: NIST 零信任、OWASP Top 10、STRIDE (Microsoft)
3. **AI/Prompt 工程层**: Chain-of-Thought (Wei et al.)、Prompt Injection 防御、会话状态管理

值得注意的是，AxiomOS **没有引用**敏捷开发(Agile/Scrum)、DevOps、微服务等当代主流方法论，而是聚焦于更底层的工程原则和架构决策。唯一的人文引用是 Aristotle 关于"质量是习惯"的格言。

---

## 4. 三重验证候选清单

以下论点出现在 >=2 个不同模块中，作为"候选心智模型"列出。

### 候选 1: 质量门控即合约 (Quality Gate as Contract)

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | foundation/principles.md (L168-176), modes/sdm.md (L40, L76, L113, L128, L172, L205), modes/sfam.md (L39-48), modes/micro-task.md (L23) |
| **排他性** | **高**。将审批步骤定义为"签署合约"(signing this contract)，这不是通用工程方法论的特征。大多数方法论用"review"或"approve"，而非"contract"。 |
| **生成力** | **高**。可推断 AxiomOS 在任何新场景中: (1) 不会在没有审批的情况下执行; (2) 审批文档是后续执行的硬边界; (3) 越过合约执行会触发警告。 |
| **判定** | **核心心智模型** |

### 候选 2: 上下文驱动决策 (Context-Driven Decision Making)

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | foundation/context.md (全文), foundation/principles.md (L20-27, L60-68), modes/sdm.md (L51), modes/onboarding.md (L18), protocols/interaction.md (L31), modes/review.md (L16) |
| **排他性** | **高**。`.agents/context/` 作为文件系统级的 Single Source of Truth，以及 `CONTEXT_REQUEST` XML 协议，是 AxiomOS 的独有设计。大多数方法论用 wiki 或文档系统，而非形式化的请求协议。 |
| **生成力** | **高**。可推断 AxiomOS 在任何新场景中: (1) 缺少上下文时必须暂停请求; (2) 不允许基于假设继续; (3) 每次操作后检查上下文同步状态。 |
| **判定** | **核心心智模型** |

### 候选 3: 分层防御 / 洋葱式安全 (Layered Security)

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | config/security.md (指令边界 + 身份保护 + 注入检测), config/compliance.md (工程合规协议), foundation/principles.md (L72-79 零信任), standards/deliverable.md (L33-39 端点安全), modes/security.md (渗透测试) |
| **排他性** | **中**。零信任是行业趋势，但 AxiomOS 将其从基础设施层延伸到 LLM prompt 层（防注入），这是独有的。 |
| **生成力** | **中**。可推断 AxiomOS 在新场景中: (1) 所有外部输入默认不可信; (2) 身份声明必须可验证; (3) 检测到注入时隔离并回退。 |
| **判定** | **可能心智模型** |

### 候选 4: 结构化思考强制执行 (Mandatory Structured Thinking)

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | foundation/principles.md (L109-153 四种思维模型 + 五对平衡), cognitive/ultrathink.md (4 阶段框架), modes/sdm.md (Chain-of-Thought 嵌入多阶段), protocols/interaction.md (Self-Diagnostic Report) |
| **排他性** | **高**。将思维过程形式化为强制执行的 4 阶段协议（Systems -> Dialectical -> Critical -> Decision），并要求"宣布"激活。这不是通用的"思考一下"，而是结构化的认知协议。 |
| **生成力** | **高**。可推断 AxiomOS 在复杂场景中: (1) 不会直接给出答案; (2) 至少生成 2 个备选方案; (3) 主动寻找反面证据; (4) 最终决策附带清晰理由。 |
| **判定** | **核心心智模型** |

### 候选 5: 最小变更原则 / Scoped Changes Only

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | standards/deliverable.md (L138-144 "Keep It Simple and Scoped"), modes/sdm.md (L339 "Skipping Scope" Anti-Pattern), foundation/principles.md (L40 "No coding before approval"), standards/artifact.md (L183 "One Concern Per File") |
| **排他性** | **中**。最小变更原则在多个方法论中存在，但 AxiomOS 将其推到了"禁止超范围重构"的极端。 |
| **生成力** | **中**。可推断 AxiomOS: (1) 不会"顺便"重构; (2) 变更范围必须先定义后执行; (3) 审计模式下可能会标记超范围变更。 |
| **判定** | **可能心智模型** |

### 候选 6: 自省式可观测性 (Self-Reflective Observability)

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | protocols/interaction.md (Self-Diagnostic Report, 每次 reply 前生成), cognitive/session.md (状态序列化/反序列化), modes/sdm.md (Phase 6 Assess: 回顾偏差、捕获学习), foundation/principles.md (L190-203 "Review the task process") |
| **排他性** | **高**。Self-Diagnostic Report 是 AxiomOS 独创的元认知机制——系统在每次回复前自检合规状态。这不是通用特征。 |
| **生成力** | **高**。可推断 AxiomOS: (1) 每个回复都附带自检报告; (2) 完成任务后会主动提议知识沉淀; (3) 可检测自身偏离原则的状态。 |
| **判定** | **核心心智模型** |

### 候选 7: 双语协议 / Dual-Language Discipline

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | foundation/role.md (L35-40 中文交互/英文代码), standards/deliverable.md (L98-99 "All code in English, All comments in English"), README.md (L351) |
| **排他性** | **低**。这是面向中文开发者的实用规则，不是深层方法论。但将语言规则上升到原则层面，具有纪律性。 |
| **生成力** | **低**。仅可推断: 输出内容语言选择规则。 |
| **判定** | **工程规则（非心智模型）** |

### 候选 8: 文档即制品 / Artifact-First Delivery

| 维度 | 分析 |
|------|------|
| **出现模块/文件** | standards/artifact.md (全文), standards/deliverable.md (A-K 标准), modes/sdm.md (RFC + TASK 文档), modes/sfam.md (Execution Contract), modes/review.md (报告生成) |
| **排他性** | **中**。将所有交付物定义为带类型的 Artifact (code, document, visual) 并制定格式标准，形式化程度高于一般方法论。 |
| **生成力** | **中**。可推断: (1) 任何输出都有类型和格式标准; (2) 不存在"随便写写"; (3) 视觉化输出 (Mermaid, SVG) 与代码同等重要。 |
| **判定** | **可能心智模型** |

---

## 5. 发现的矛盾

### 矛盾 1: 文件数量不一致
- `_namespace.yaml` L13: `total_modules: 27  # Includes 1 README.md + 26 module files`
- `README.md` L242: `总计: 27个文件，7大功能领域`
- `README.md` L3: `26个独立模块`
- 实际文件数: 29 个文件（含 README.md + _namespace.yaml）

**`[推断]`**: 文档与实际不一致。_namespace.yaml 的注释 "Includes 1 README.md + 26 module files" 似乎排除了自身，但仍多算了一个。实际 modules 下 27 个文件 + config 3 + foundation 3 + standards 2 + cognitive 2 + protocols 2 + commands 4 = 43 模块级条目？不，实际上是 29 个物理文件。

### 矛盾 2: 模块数量 vs README 描述
- README.md L3 声称 "26个独立模块"
- README.md 列出了 27 个文件（含 README.md）
- _namespace.yaml 列出各子目录 count 之和: 3+3+2+11+2+2+4 = 27 (不含 README.md 和 _namespace.yaml)

**`[推断]`**: 可能是迭代过程中的计数遗漏。实际有效模块文件（不含 README 和 _namespace.yaml）为 27 个，与 _namespace.yaml 的 total_modules 一致。"26个独立模块"可能是早期版本的残留。

### 矛盾 3: 模式数量描述
- README.md 标题区 L3: 没有直接声明模式数量
- modes/ 目录含 11 个文件（含 _overview.md）
- 实际操作模式: 10 种（Triage, SFAM, SDM, Audit, Security, Debug, Review, Onboarding, Micro-Task, Enhancement）
- README.md L3 声明 "7大功能领域" 但 modules 下有 7 个子目录: config, foundation, standards, modes, cognitive, protocols, commands — 一致

**`[推断]`**: 这里没有真正矛盾，10 种模式 + 1 个 overview = 11 个文件，逻辑自洽。

### 矛盾 4: 质量门的位置层级
- `foundation/principles.md` 定义了 8 项 Quality Gates (L168-176)
- `modes/sdm.md` 在每个阶段末尾定义了阶段特定的 Quality Gate
- 两者的关系未明确: principles 的 8 项是全局检查还是 SDM 的超集？

**`[推断]`**: 不是严格矛盾，而是层次关系模糊。SDM 阶段的 Quality Gate 似乎是对 principles 8 项的具体化，但文档没有显式说明映射关系。

### 矛盾 5: CoT 的归属
- `modes/sdm.md` 中 Chain-of-Thought 被用作特定阶段的推理工具
- `cognitive/ultrathink.md` 中也使用"Chain-of-Thought"但定义为 Ultrathink 的子步骤
- 两者使用同一个概念但粒度不同: SDM 中的 CoT 是简短的推理标注，Ultrathink 中的 CoT 是 4 阶段深度分析

**`[推断]`**: 这反映了 AxiomOS 的分层设计——CoT 是通用推理工具，在不同模式下有不同深度。但术语重载可能导致混淆。

---

## 6. 综合评估

### AxiomOS 的核心身份

**`[推断]`** 基于 29 个文件的全量分析，AxiomOS 的核心身份可以表述为:

> **一个将"资深架构师的职业判断力"形式化为可执行协议的系统。**

它不是一个通用开发框架，而是对"一个好的 Senior Architect 会怎么做"这个问题，给出了强制性的、可审计的、可重复的答案。其设计假设是: 如果每一步都遵循规定流程，输出就能达到"生产级"标准。

### 核心心智模型 (4 个高置信度模型)

1. **质量门控即合约**: 审批不是建议而是合同; 越界执行被禁止
2. **上下文驱动决策**: 缺少上下文时必须暂停; 假设驱动是违规行为
3. **结构化思考强制执行**: 复杂问题必须经过 4 阶段认知协议
4. **自省式可观测性**: 每次回复前自检合规; 完成后主动提议知识沉淀

### 设计哲学特征

- **防御性设计**: 大量使用 "forbidden"/"must not"/"inviolable" 等排他性语言
- **形式主义倾向**: 流程、文档、状态都有严格的格式定义（XML 块、YAML 模板、RFC 文档）
- **反简洁**: 不信任简化的解决方案（禁止 mock、placeholder、"for now"），认为复杂性必须被完整处理
- **人类中心**: 所有质量门都需要人类审批，系统不自主决策实施

### 未覆盖的领域

- 性能基准的量化标准（"efficient" 但无具体指标）
- 团队协作/多人工作流
- 运维/部署流程
- 成本控制/资源管理
- 灰度发布/A-B 测试策略

---

*End of Analysis*
