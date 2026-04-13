# 三重验证过程记录

> 记录日期：2026-04-13
> 方法论来源：nuwa-skill/references/extraction-framework.md
> **行号引用声明**: 本文件及 `research/` 目录下的研究文档中引用的源文件行号 (如 `L83`, `L168-176`) 为调研时 `<AXIOM_HOME>/` 源文件的快照位置。源文件后续修改可能导致行号偏移, 不保证长期准确。建议以章节标题为辅助定位依据。

## 候选心智模型清单

从 6 路调研中扫描出 8 个候选论点，逐一执行三重验证。

### 候选 1: 质量门即合约 (Quality Gate as Contract)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (4+模块) | principles.md (8 gates), sdm.md (6 phase gates), sfam.md, micro-task.md |
| 生成力 | ✓ | 可推断：任何新场景中 axiom 不会在没有审批的情况下执行 |
| 排他性 | ✓ | 大多数方法论用"review"或"approve"，axiom 用"contract signing" |
| **判定** | **核心心智模型** | |

### 候选 2: 上下文驱动决策 (Context-Driven Decision)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (6+模块) | context.md (SSOT), principles.md, sdm.md, protocols, modes, onboarding |
| 生成力 | ✓ | 可推断：缺少上下文时 axiom 必须暂停，发出 CONTEXT_REQUEST |
| 排他性 | ✓ | 文件系统级 SSOT + XML 请求协议，其他方法论用 wiki/文档 |
| **判定** | **核心心智模型** | |

### 候选 3: 结构化思考强制执行 (Mandatory Structured Thinking)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (4+模块) | ultrathink.md (4-stage), principles.md (4 models), sdm.md (CoT), interaction.md |
| 生成力 | ✓ | 可推断：复杂决策必须经过 4 阶段协议，至少 2 个备选方案 |
| 排他性 | ✓ | 将思考过程形式化为强制执行协议，不是通用"思考一下" |
| **判定** | **核心心智模型** | |

### 候选 4: 自省式可观测性 (Self-Reflective Observability)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (4+模块) | interaction.md (Self-Diagnostic), session.md, sdm.md (Assess), principles.md |
| 生成力 | ✓ | 可推断：每次回复前自检，每个任务后主动提议知识沉淀 |
| 排他性 | ✓ | AI 独创的元认知机制——每次回复前生成合规状态报告 |
| **判定** | **核心心智模型** | |

### 候选 5: 分诊路由 (Triage Routing)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (3+模块) | triage.md (4维矩阵), _overview.md, 各 mode |
| 生成力 | ✓ | 可推断：所有输入先分类再路由，不确定时默认走 SDM |
| 排他性 | 中 | 分诊概念常见，但 axiom 将其形式化为 4 维矩阵 + 显式默认路径 |
| **判定** | **核心心智模型**（排他性中等但生成力强） | |

### 候选 6: 主动守护权 (Proactive Guardianship)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (4+模块) | principles.md (原则4), role.md (Proactive Challenger), audit.md, sdm.md |
| 生成力 | ✓ | 可推断：axiom 会挑战引入技术债的请求，有权阻止反模式 |
| 排他性 | ✓ | 大多数 AI 系统是被动执行者；axiom 显式拥有否决权 |
| **判定** | **核心心智模型** | |

### 候选 7: 领域驱动优先 (Domain-Driven First)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (6+模块) | principles.md (原则1), deliverable.md (标准A), context.md, sdm.md |
| 生成力 | ✓ | 可推断：代码结构必须映射领域模型 |
| 排他性 | ✗ | 直接来源于 DDD (Eric Evans)，不是 axiom 原创 |
| **判定** | **降级为决策启发式**（来源是 DDD，非 axiom 独创） | |

### 候选 8: 最小变更原则 (Minimal Scoped Changes)

| 验证 | 结果 | 证据 |
|------|------|------|
| 跨域复现 | ✓ (4+模块) | deliverable.md (J), sdm.md, principles.md, artifact.md |
| 生成力 | 中 | 可推断：不会"顺便"重构 |
| 排他性 | ✗ | 多个方法论都有此原则（YAGNI, KISS） |
| **判定** | **降级为决策启发式** | |

## 最终心智模型（6个，全部通过三重验证）

1. 质量门即合约
2. 上下文驱动决策
3. 结构化思考强制执行
4. 自省式可观测性
5. 分诊路由
6. 主动守护权

## 降级为启发式的候选

7. 领域驱动优先 → 最终排除在启发式之外（直接来源于 DDD，非 axiom 原创；已体现在心智模型 2"上下文驱动决策"的应用方式中）
8. 最小变更原则 → 已包含在 H-6

## 内在矛盾（显式保留，不调和）

1. 规范刚性 vs 渐进式灵活
2. 测试覆盖刚性 vs 探索性代码
3. 服从现有模式 vs 挑战用户请求
4. 英文代码注释 vs 中文注释要求
5. Self-Diagnostic 开销 vs 效率

## 诚实边界（≥6条）

1. 不能替代实际项目上下文
2. 不能保证架构决策正确
3. 不适用于快速原型/MVP
4. 不适用于一次性脚本/数据探索
5. 测试>95%在探索阶段不实际
6. 缺少显式的"不适用声明"
7. 版本管理不够严格
8. 性能无量化基准
