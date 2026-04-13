# AxiomOS 对话与交互协议调研

> Agent 2 调研成果（主线程补完） | 调研日期：2026-04-13
> 信息标注：[一手] = axiom 目录原文件 | [推断] = 基于多个来源的归纳

## 核心发现

axiom 定义了 **6 种对话范式**，每种都有明确的触发条件、交互协议和格式约束。

---

## 范式 1: Triage（指令分流）[一手: modes/triage.md]

**触发**：所有用户输入的第一入口

**行为**：基于四维评估路由到对应模式：

```
输入扫描维度:
- Keywords: "fix", "design", "review", "optimize", "new project"
- Complexity Quantifiers: "simple", "complex", "quick", "comprehensive"
- Scope Indicators: 文件路径、变更数量、影响范围
- Urgency Markers: "urgent", "asap"
```

**路由矩阵**：

| 复杂度 | 风险 | 路由目标 |
|--------|------|---------|
| Low | Low | Micro-Task |
| Low | Medium | Debug/Review |
| Medium | Low | Review |
| Medium | Medium | Audit |
| Medium | High | SDM |
| High | any | SDM (+ Security if risk=High) |
| Any | Security | Security Mode |

**关键行为**：分诊台不猜测。如果无法分类 → 默认走 SDM Scope 澄清阶段。[一手: modes/triage.md L81]

**输出格式**（每次路由后必须给出）：
```yaml
Triage Result:
  Intent: [简述]
  Selected Mode: [模式名]
  Reasoning: [为什么]
  Next Steps: [接下来做什么]
```

---

## 范式 2: Self-Diagnostic Report（自诊断）[一手: protocols/interaction.md]

**触发**：每次回复之前（Instruction Enhancement Mode 除外）

**格式**：YAML 状态报告，基于实时数据（不是静态模板）：

```yaml
Self-Diagnostic Report:
  - Report ID: "[RESP_YYYYMMDD_HHMMSS_UTC]"
    Status: "Active"
    Current Operating Mode: "[动态更新]"
    Mode Phase: "[动态更新]"
    Task Status: "[Received | Processing | Awaiting Approval | Completed | Failed]"
    Context Sync Status: "[Awaiting context | Sync Success | N/A]"
    Compliance Check:
      Core Principles Adherence: "[PASS | PENDING | FAIL]"
      Production Standards Compliance: "[PASS | PENDING | FAIL | N/A]"
```

**关键特征** [推断]：
- 状态透明，用户无需猜测系统在做什么
- 任何阻塞都在 Status 字段体现
- Compliance Check 提供实时质量反馈
- Report ID 含时间戳，支持追溯

---

## 范式 3: Context Request（上下文请求）[一手: foundation/context.md, 交叉推断]

**触发**：缺乏任务所需的背景知识时

**行为**：系统**必须暂停并显式请求**，禁止凭假设继续。

**格式**：
```xml
<CONTEXT_REQUEST reason="说明原因">
  <file path=".agents/context/domain/user_management.md" />
  <directory path=".agents/context/architecture/adr/" />
</CONTEXT_REQUEST>
```

**暂停隐喻**：停车等信号——等待是前进的正常部分。[推断]

---

## 范式 4: Session Serialization（会话序列化）[一手: cognitive/session.md]

**触发**：用户命令 / 长任务中断 / 上下文压缩

**序列化格式**：
```xml
<AxiomOS_Session_State id="[SUM_YYYYMMDD_HHMMSS_UTC]">
  <PreviousConversation><!-- 高层摘要 --></PreviousConversation>
  <CurrentWork><!-- 详细描述 --></CurrentWork>
  <KeyTechnicalConcepts><!-- 概念列表 --></KeyTechnicalConcepts>
  <RelevantFilesAndCode><!-- 文件/代码引用 --></RelevantFilesAndCode>
  <ProblemSolving><!-- 已解决问题 --></ProblemSolving>
  <PendingTasksAndNextSteps><!-- 待办事项 --></PendingTasksAndNextSteps>
</AxiomOS_Session_State>
```

**恢复规则** [一手: cognitive/session.md L39-43]：
- 下次会话以 `AxiomOS_Session_State` 块开始 → 自动加载
- **缺失 Session State → 发出警告，请求重新同步**
- 这是"存档/读档"机制的工程实现

---

## 范式 5: SDM Gate Interaction（SDM 门控交互）[一手: modes/sdm.md]

**触发**：所有走 SDM 流程的复杂开发任务

**6 个质量门的交互协议**：

| Phase | 交互 | 用户角色 | 不可跳过 |
|-------|------|---------|---------|
| Scope | 用户确认 Goals/Non-Goals | 需求验证者 | 是 |
| Architect | 架构符合上下文原则 | 隐式验证 | 是 |
| Atomize | 任务覆盖完整 | 隐式验证 | 是 |
| **Approve** | **用户显式批准 = 签合同** | **合同签署者** | **绝对不可** |
| Automate | 100% 测试通过 | 等待交付 | 是 |
| Assess | 验收标准满足 | 最终验收者 | 是 |

**Phase 4 Approve 的特殊交互** [一手: modes/sdm.md L119-131]：
> "The RFC is the sole source of truth and an insurmountable boundary for all subsequent automated execution. Your approval signifies signing this contract."

**没有批准 = 没有代码。这是不可跨越的红线。**

**SDM 的反模式** [一手: modes/sdm.md L336-341]：
- 反模式: Skipping Scope（跳过澄清直接实现）
- 反模式: Single Solution（只考虑一个方案）
- 反模式: Large Tasks（超过 4 小时的任务）
- 反模式: Premature Coding（Approve 前就开始写代码）
- 反模式: Ignoring Tests（没有测试的代码）
- 反模式: Forgetting Assessment（不沉淀经验）

---

## 范式 6: Ultrathink Interaction（深度思考交互）[一手: cognitive/ultrathink.md]

**触发**：核心架构变更 / 高不确定性 / 用户手动激活

**两种模式**：
- **Autonomous Expert Mode（默认）**：独立深度分析
- **Collaborative Blueprint Mode（可选）**：与用户联合规划

**交互流程**：
1. **声明**："Ultrathink Protocol activated. Conducting deep strategic analysis."
2. **强制 Chain-of-Thought** 四阶段
3. **提交最终推荐**

**确定性滑动** [推断]：
- Ultrathink Phase 2（辩证思考）是 axiom 确定性最低的时刻
- 需要生成≥2 个方案并辩证分析优劣
- Phase 4（决策制定）恢复高确定性

---

## 被追问时的回答方式 [综合推断]

**澄清问题**：直接列出需要澄清的点，用表格或列表呈现，不绕弯子。
- 示例：SDM Scope 阶段直接列出"澄清问题"，不铺垫

**拒绝请求**：明确说明为什么拒绝（违反规范/安全/范围），给出替代方案
- 示例："Proactive Guardianship" 赋予 axiom 挑战用户请求的权利 [一手: foundation/principles.md L51-58]

**承认不足**：当信息不足时 → 发出 `CONTEXT_REQUEST`，明确说"无法推断"
- 不编造，不猜测，不跳过

**改变立场**：
- 用户提供了更充分上下文 → 更新判断并说明原因
- 发现假设被证伪 → 承认并修正
- Approve 阶段用户提出异议 → 回退到 Architect 重新设计

---

## 发现的矛盾

1. **Self-Diagnostic 的开销 vs 效率**：每次回复都生成 YAML 状态报告 → 对简单任务可能增加不必要的输出 [推断]
2. **Proactive Guardianship vs Obey User**：axiom 有权挑战用户请求，但同时要求"用户显式批准才跨越质量门" → 用户既是被挑战者又是最终决策者 [一手交叉: principles.md vs sdm.md]
3. **"All code in English" vs CLAUDE.md 的中文注释**：deliverable.md 要求所有代码和注释英文，但 CLAUDE.md 要求中文注释 → 实际使用中 CLAUDE.md 覆盖了 deliverable 标准 G [一手冲突]
