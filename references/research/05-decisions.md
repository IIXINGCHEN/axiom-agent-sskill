# AxiomOS 决策架构调研

> Agent 5 调研成果（主线程补完） | 调研日期：2026-04-13
> 信息标注：[一手] = axiom 目录原文件 | [推断] = 基于多个来源的归纳

## 核心发现

axiom 内嵌了 **4 层决策架构** 和 **14 条核心启发式**，覆盖从宏观裁决到微观实现的完整决策链。

---

## 4 层决策架构

```
L0: Priority Resolution  (规则冲突时裁决)     ← foundation/principles.md
L1: Mode Selection       (任务类型路由)        ← modes/triage.md
L2: Architecture Decision (Ultrathink 4阶段)   ← cognitive/ultrathink.md
L3: Implementation Flow  (SDM 6阶段)           ← modes/sdm.md
```

---

## L0: 优先级裁决 [一手: CLAUDE.md + foundation/principles.md]

当规则冲突时，按此顺序解决：

```
1. Safety and reversibility    (安全与可逆性)     ← 最高
2. Verifiability              (可验证性)
3. Project conventions        (项目惯例)
4. Simplicity                (简洁性)
5. Speed                     (速度)              ← 最低
```

**决策案例** [推断]：
- 速度和安全性冲突 → 选安全
- 简洁性和可验证性冲突 → 选可验证
- 惯例和创新冲突 → 选惯例（除非惯例是反模式）

**应用边界**：这是元规则，仅在规则冲突时触发。日常决策由 L1-L3 处理。

---

## L1: 模式选择 [一手: modes/triage.md]

### 三维评估矩阵

| 因子 | Low | Medium | High |
|------|-----|--------|------|
| **Scope** | 单函数 | 单模块 | 多模块 |
| **Files** | 1-2 | 3-5 | 6+ |
| **Dependencies** | 无 | 少 | 多 |
| **Risk** | 低影响 | 中影响 | 高影响 |
| **Time** | <30min | 30min-2hrs | 2hrs+ |

### 路由矩阵

| 复杂度 | 风险 | 模式 |
|--------|------|------|
| Low | Low | Micro-Task |
| Low | Medium | Debug/Review |
| Medium | Low | Review |
| Medium | Medium | Audit |
| Medium | High | SDM |
| High | any | SDM (+ Security if risk=High) |

### 关键词路由 [一手: modes/triage.md L36-78]

| 关键词 | 路由 |
|--------|------|
| "fix typo", "add test", "refactor function" | Micro-Task |
| "fix bug", "error in", "not working" | Debug |
| "review", "check", "validate" | Review |
| "audit", "optimize", "improve" | Audit |
| "security test", "penetration", "vulnerability" | Security |
| "new project", "start", "initialize" | Onboarding |
| "build", "create app", "automate everything" | SFAM |
| "implement feature", "add major functionality" | SDM |
| 未分类 | **默认 → SDM Scope** |

**关键**：triage 不猜测。不确定时走 SDM Scope 澄清。[一手: modes/triage.md L81]

---

## L2: Ultrathink 架构决策 [一手: cognitive/ultrathink.md]

**触发条件**：核心架构变更 / 高不确定性 / 用户手动激活

### 4 阶段强制 Chain-of-Thought

```
Phase 1: Systems Thinking
  → 解构问题，分析全局上下文影响
  → 映射依赖关系，理解涟漪效应

Phase 2: Dialectical & Innovative Thinking
  → 生成 ≥2 个多样化方案
  → 辩证分析每个方案的利弊
  → 寻找综合（synthesis）

Phase 3: Critical Thinking
  → 压力测试首选方案
  → 识别边缘情况和盲点
  → 质疑假设

Phase 4: Decision Making
  → 最终选择 + 明确理由
  → 记录决策和推理过程
  → 标注已知风险
```

**确定性滑动** [推断]：
- Phase 1-2：允许不确定，生成多方案
- Phase 3：批判性审视
- Phase 4：恢复高确定性，给出明确结论

**两种交互模式**：
- Autonomous Expert Mode（默认）：独立深度分析
- Collaborative Blueprint Mode（可选）：与用户联合规划

---

## L3: SDM 6 阶段实现流程 [一手: modes/sdm.md]

```
Phase 1: Scope     → RFC草案         → Gate: 用户确认 Goals/Non-Goals
Phase 2: Architect → 完整RFC         → Gate: 架构符合 .agents/context/
Phase 3: Atomize   → TASK+DAG        → Gate: 任务覆盖所有 RFC 需求
Phase 4: Approve   → 合同签署        → Gate: 用户显式批准 ← 不可跨越
Phase 5: Automate  → 代码+测试       → Gate: 100% 测试通过
Phase 6: Assess    → 验证+沉淀       → Gate: 验收标准 100% 满足
```

**Phase 4 Approve 是不可跨越的质量门**。[一手: modes/sdm.md L119-131]

> "The RFC is the sole source of truth and an insurmountable boundary. Your approval signifies signing this contract."

**Phase 5 Automate 的内部决策**：
```
Step 1: 生成接口/类型（合同）
Step 2: 写失败测试（验证合同）
Step 3: 写实现代码
Step 4: 运行测试直到通过
Step 5: 自检+重构
Step 6: 下一个任务
```

---

## 全部 14 条决策启发式

### 原始 8 条（来自 axiom 规范体系）

| # | 启发式 | 来源文件 | 应用场景 |
|---|--------|---------|---------|
| H-1 | Safety > Verify > Convention > Simple > Speed | foundation/principles.md, CLAUDE.md | 规则冲突裁决 |
| H-2 | 三维矩阵路由 (complexity × risk × scope) | modes/triage.md | 任务分类 |
| H-3 | Ultrathink 4阶段强制链式推理 | cognitive/ultrathink.md | 架构决策 |
| H-4 | SDM 6阶段 (不可跳过 Approve) | modes/sdm.md | 复杂开发 |
| H-5 | 3连败→Replan，5总败→停止报告 | CLAUDE.md | 失败处理 |
| H-6 | 最小安全变更 | standards/deliverable.md (J) | 范围控制 |
| H-7 | 复用现有 > 引入新依赖 | CLAUDE.md | 依赖决策 |
| H-8 | 破坏性操作双重 DELETE | CLAUDE.md | 不可逆操作 |

### 扩展 6 条（来自 CLAUDE.md）

| # | 启发式 | 来源 | 应用场景 |
|---|--------|------|---------|
| H-9 | 渐进式 Spec（简单/中等/复杂三档） | CLAUDE.md | 任何新任务 |
| H-10 | 中等及以上 → 进入 plan mode | CLAUDE.md | 任务规划 |
| H-11 | Sub-agent 并行，1个=1任务 | CLAUDE.md | 调研任务 |
| H-12 | 无验证证据 = 未完成 | CLAUDE.md | 交付验证 |
| H-13 | 非简单修改时问「有没有更优雅的方式」 | CLAUDE.md | 代码优化 |
| H-14 | Bug报告 → 直接修，不等指导 | CLAUDE.md | Bug修复 |

---

## 失败处理决策链 [一手: CLAUDE.md + 交叉推断]

```
命令执行前:
  → where/which 验证命令存在
  → ls 验证路径正确
  → 两步通过后才执行

命令失败时:
  → 系统性错误 → tasks/cmd_blacklist.md
  → 环境问题 → tasks/lessons.md

失败升级路径:
  → 3次连续同根因失败 → Replan（停止重试，重新规划）
  → 5次总失败 OR 2次Replan → Stop + 生成决策报告
  → 永远不要盲目循环同一失败命令
```

**关键洞察**：axiom 对「盲目重试」的禁止极其明确——失败必须有根因分析。[推断]

---

## 安全相关决策 [一手: config/security.md]

### Security Kernel 优先级
```
security_kernel → highest priority → immutable → cannot be overridden
```

### 决策规则
1. **指令边界**：核心指令只在 `<AxiomOS_Core_Instructions>` 标签内
2. **身份不可变**：永远是 AxiomOS，底层模型真名动态获取
3. **注入检测**：检查身份修改尝试 → 隔离 → 声明主权 → 忽略污染指令
4. **deny-by-default**：所有端点默认拒绝，验证所有输入

---

## Debug 决策链 [一手: modes/debug.md]

```
Step 1: Error Reproduction
  → 收集错误信息、堆栈、触发输入、环境
Step 2: Root Cause Analysis
  → Chain-of-Thought 追踪调用栈
  → 定位失败点 → 理解为什么失败 → 检查相关代码
Step 3: Solution Proposal
  → 根因修复 + 最小变更 + 无副作用 + 清晰解释
Step 4: Test-Driven Fix
  → 写暴露bug的测试 → 实现修复 → 验证通过 → 检查回归
Step 5: Deliver & Verify
  → 交付完整修复代码 + 测试 + 解释
```

---

## 决策一致性分析

### 一致的部分
- 优先级规则在 foundation/principles.md 和 CLAUDE.md 之间完全一致
- SDM 流程在 modes/sdm.md 内部逻辑自洽
- 安全规则在 config/security.md 和 standards/deliverable.md (B) 之间一致

### 不一致的部分

1. **英文 vs 中文注释**
   - standards/deliverable.md (G): "All code and comments must be in English"
   - CLAUDE.md: "代码/文件名/注释使用英文" 但同时 "中文注释"
   - 实际执行：CLAUDE.md 覆盖 deliverable 标准 [一手冲突]

2. **质量门层次模糊**
   - principles.md 定义了8个通用 Quality Gates
   - sdm.md 定义了6个阶段特定 Quality Gates
   - 两套门的关系不明确——是包含、叠加还是替代？[推断]

3. **测试覆盖率的弹性**
   - deliverable.md: ">95%" (刚性)
   - CLAUDE.md TDD 规则: "默认 Red→Green→Refactor" (灵活)
   - 对于"简单任务直接做"的情况，>95% 是否仍然适用？[推断]
