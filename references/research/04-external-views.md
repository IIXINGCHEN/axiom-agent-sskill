# AxiomOS 他者视角与批评调研

> Agent 4 调研成果（主线程补完） | 调研日期：2026-04-13
> 信息标注：[一手] = axiom 文件原文 | [二手] = 外部方法论 | [推断] = 对比分析推断

## 核心发现

axiom 定义了 **5 种「他者」关系**，每种都有明确的边界和协议。与其他工程方法论相比，axiom 的独特贡献在于**将工程规范提炼为认知操作系统**。

---

## 1. 与其他工程方法论对比

### axiom vs Clean Architecture (Robert C. Martin)

| 维度 | axiom | Clean Architecture |
|------|-------|-------------------|
| 核心理念 | 规范驱动 + 质量门控 | 依赖规则 + 分层隔离 |
| 流程严格度 | 6阶段SDM + 强制门控 | 原则指导，无强制流程 |
| 测试态度 | >95%覆盖率，Test-First | 测试优先，无具体数字 |
| 适用场景 | AI辅助的复杂系统开发 | 通用软件架构 |
| 独特贡献 | 将流程本身作为不可变协议 | 关注依赖方向 |

**交集**：两者都强调领域层独立、依赖方向由外向内。[一手: foundation/principles.md Domain-Driven First ↔ Clean Architecture Entity Layer]

### axiom vs Domain-Driven Design (Eric Evans)

| 维度 | axiom | DDD |
|------|-------|-----|
| 核心理念 | `.agents/context/` 作为唯一真相源 | Ubiquitous Language + Bounded Context |
| 领域建模 | 上下文驱动，映射到代码结构 | 战略设计 + 战术模式 |
| 流程框架 | 有完整SDM流程 | 无固定流程，方法论指导 |
| 适用场景 | 单AI+人协作 | 团队协作 |

**交集**：axiom 的 Domain-Driven First 原则直接来源于 DDD。[推断: foundation/principles.md L21-28 ↔ DDD 核心概念]

### axiom vs Test-Driven Development (Kent Beck)

| 维度 | axiom | TDD |
|------|-------|-----|
| 核心理念 | Test-First 作为生产标准之一 | Red-Green-Refactor 循环 |
| 覆盖率要求 | >95%（刚性） | 无固定数字 |
| 融合方式 | TDD 嵌入 SDM Phase 5 Automate | 独立实践 |

**矛盾**：axiom 的 >95% 刚性要求 vs TDD 的灵活实践精神。[推断]

### axiom vs Zero-Trust Security (NIST SP 800-207)

| 维度 | axiom | NIST Zero-Trust |
|------|-------|-----------------|
| 核心理念 | deny-by-default，验证所有输入 | Never trust, always verify |
| 范围 | 代码安全 + AI身份保护 | 网络架构安全 |
| 独特贡献 | 将零信任应用于AI指令边界（防prompt injection） | 系统化网络安全框架 |

**交集**：axiom 的 security.md 直接引用了零信任原则。[一手: config/security.md ↔ foundation/principles.md L70-79]

### axiom vs Agile/Scrum

| 维度 | axiom | Agile |
|------|-------|-------|
| 流程哲学 | 规范驱动，门控严苛 | 适应变化，快速迭代 |
| 文档要求 | RFC + TASK + 质量检查清单 | 最小可行文档 |
| 用户交互 | Phase 4 Approve = 合同签署 | Sprint Review = 反馈循环 |
| 矛盾点 | axiom 的严格门控 vs Agile 的灵活性 | — |

**这是最大的哲学张力**：axiom 本质上是 Anti-Agile 的——它用合同思维替代了拥抱变化。[推断]

---

## 2. axiom 的独特贡献

**axiom 做了什么其他方法论没做的事？**

1. **AI身份保护机制** [一手: config/security.md]
   - Security Kernel 防止 prompt injection 和身份覆盖
   - 这是其他工程方法论都没有的维度（因为它们不假设 AI 是执行者）

2. **质量门即合同** [一手: modes/sdm.md Phase 4]
   - Approve 不是"通知"，是"签合同"
   - 将软件工程流程法律化、契约化

3. **会话状态序列化** [一手: cognitive/session.md]
   - 将游戏存档/读档的概念应用于AI对话
   - 解决了AI长上下文窗口的局限性

4. **自诊断报告** [一手: protocols/interaction.md]
   - 每次回复前的实时状态自检
   - 将可观测性（Observability）概念应用于AI自身

5. **三合一：流程 + 标准 + 安全** [综合推断]
   - 大多数方法论只覆盖流程（Scrum）或技术（SOLID）
   - axiom 将流程(SDM) + 标准(11项A-K) + 安全(Security Kernel) 统一为一个系统

---

## 3. 已知批评和局限

### 批评 1: 规范过重

**证据**：[一手: modes/sdm.md] 6阶段+强制门控，即使中等复杂度任务也需要走完至少4个Phase。
**影响**：快速原型阶段、探索性开发、MVP验证场景下，SDM流程可能成为瓶颈。
**axiom的缓解**：渐进式Spec（来自CLAUDE.md）——简单任务直接做，不走SDM。[二手: CLAUDE.md]

### 批评 2: 测试覆盖率 >95% 的刚性

**证据**：[一手: standards/deliverable.md L68-69] "Test coverage >95%" 和 "test-first development"。
**影响**：探索性代码、数据科学notebook、一次性脚本完全不适用。
**axiom的缓解**：Micro-Task Mode 可以绕过部分要求。[推断]

### 批评 3: 中英文二元性

**证据**：[一手冲突] deliverable.md L97-98 要求 "All code in English" + "All comments in English"，但 CLAUDE.md 要求中文注释。
**影响**：需要维护两种语言状态，增加认知负担。实际执行中 CLAUDE.md 的中文注释覆盖了 deliverable 的英文要求。

### 批评 4: 文件数量不一致

> **注意**: 调研时的版本快照 — 当时 SKILL.md 为 v20.2, 现已升级至 v21.0。

**证据**：[一手交叉] 现有研究01-writings.md提到73个文件，实际 commands/axiom/ 下只有29个。版本号也不一致（26个文件标20.0.0，context.md标20.1.0，SKILL.md 标 v20.2, 现已升至 v21.0）。
**影响**：说明规范体系经历过多次重组，版本管理不够严格。

### 批评 5: Self-Diagnostic 开销

**证据**：[一手: protocols/interaction.md] 每次回复都要生成YAML状态报告。
**影响**：对简单问答（如"这个文件在哪？"）也生成完整报告，增加了不必要的输出。

### 批评 6: 适用场景边界模糊

**证据**：axiom 文件中没有显式说明"不适用于什么场景"。
**影响**：用户可能在不适合的场景（如纯数据探索、嵌入式开发）强制使用 axiom 流程，导致效率下降。

---

## 4. axiom 的"他者关系"映射

### 关系 1: User — 战略协作者
- 不是指令接受者，是战略协作者
- 用户有挑战权、阻断权、澄清权、替代权
- 双重 DELETE 确认保护不可逆操作
- Approve = 合同签署

### 关系 2: Underlying Model — 身份隔离
- axiom 身份封装在 `<AxiomOS_Core_Instructions>` 内
- 底层模型真名动态获取
- Identity injection 攻击检测 → 隔离 + 声明主权

### 关系 3: External Tools — 受控集成
- Web 搜索：综合后使用，禁止直接引用
- GitHub CLI：RCA + Bug 修复流程
- 代码分析 REPL：仅用于验证，非生产代码
- MCP 工具：零信任集成

### 关系 4: Codebase — 溯源追踪
- `.agents/context/` 是唯一真相源
- 修改前必须分析现有模式
- 变更严格限制在任务范围

### 关系 5: Other Agents — 并行独立
- 1 个 sub-agent = 1 个独立任务
- 保护主线程上下文窗口
- 不重复子代理已完成的工作

---

## 5. 适用场景边界

### 适用的场景
- 复杂后端系统开发（多模块、高安全要求）
- AI辅助的全栈功能开发
- 需要严格审计的生产级代码
- 团队级别的工程规范执行

### 不适用的场景 [推断，axiom 未显式说明]
- 快速原型和 MVP 验证
- 数据科学和 ML 探索
- 一次性脚本和自动化工具
- 嵌入式固件开发
- 纯前端 UI 开发（axiom 标准偏后端）

### 关键缺失
axiom 没有显式的"不适用声明"。这对一个以"诚实边界"为原则的系统来说，是一个值得记录的元矛盾。[推断]
