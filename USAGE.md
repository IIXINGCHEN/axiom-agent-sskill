# AxiomOS · Claude Code 使用指南

> 如何在 Claude Code 中有效使用 axiom 蒸馏版

---

## 安装与激活

### 方式 1: 作为 Skill 使用（推荐）

将 `SKILL.md` 放入 Claude Code 的 skill 目录，通过描述中的关键词自动激活：

- 提及「axiom」
- 提及「axiomOS」
- 提及「用 axiom 视角」

### 方式 2: 手动加载

在对话中直接粘贴 `SKILL.md` 的内容，或使用 `/axiom:activate` 命令。

---

## Agentic Protocol 说明

axiom v21.0 的核心升级是 **Agentic Protocol**——先研究再回答，不凭训练语料编造事实。

### 3 步工作流

```
Step 1: 问题分类
  ↓ 需要事实？→ Step 2
  ↓ 纯框架？→ 直接 Step 3

Step 2: Axiom 式研究
  ↓ 看架构影响 → 看安全边界 → 看测试覆盖 → 看现有模式 → 看最小变更

Step 3: Axiom 式回答
  ↓ 结论先行 → 引用证据 → 验证路径 → 标注风险
```

### 什么时候 axiom 会做研究

| 场景 | 行为 |
|------|------|
| 「这个 API 要加缓存」 | 先搜索代码库中现有缓存模式 |
| 「微服务 vs 单体怎么选」 | 直接用心智模型回答（纯框架） |
| 「用 Stripe 实现订阅」 | 先研究 Stripe API 文档 + 项目现有支付架构 |

### 什么时候 axiom 直接回答

- 架构原则、设计模式、工程流程问题
- axiom 规范体系已覆盖的标准和原则
- 通用工程最佳实践

---

## 核心操作模式使用

### Micro-Task（小任务）

```
用户: "把这个字段名从 userName 改成 username"
axiom: 直接执行，无需 Spec
```

### Debug（Bug 修复）

```
用户: "生产环境有个 NPE"
axiom: 复现 → 根因分析 → TDD 修复 → 验证
```

### Review（代码审查）

```
用户: "审查这个 PR"
axiom: 多维分析 → 报告 → 可选自动修复
```

### SDM（复杂开发）

```
用户: "给支付系统加退款功能"
axiom:
  Phase 1: Scope — 澄清需求
  Phase 2: Architect — 设计方案（≥2 个备选）
  Phase 3: Atomize — 分解为 DAG
  Phase 4: Approve — 等待用户签合同 ← 不可跨越
  Phase 5: Automate — 测试优先实现
  Phase 6: Assess — 验证 + 沉淀
```

**关键**：Phase 4 Approve 是红线。没有批准 = 没有代码。

---

## 渐进式 Spec

axiom 根据复杂度自动选择流程深度：

| 复杂度 | 判断标准 | 流程 |
|--------|---------|------|
| **简单** | 改字段、修 bug、1-2 文件 | 直接执行 |
| **中等** | 3+ 步骤，有架构决策 | 轻量 Spec + 审批后编码 |
| **复杂** | 跨模块、多系统 | 完整 RFC → 审批 → 实现 → 审查 → 交付 |

---

## 与 CLAUDE.md 的关系

axiom 运行在 CLAUDE.md（全局 Agent 基础纪律层）之上。两层协作，不替代。

### 职责分工

| 维度 | CLAUDE.md（基础纪律层） | axiom（认知增强层） |
|------|----------------------|-------------------|
| 激活 | 始终生效 | 按需（提到 axiom 时） |
| 范围 | 所有项目、所有任务 | 工程认知增强场景 |
| 核心 | 优先级裁决、失败阈值、TDD、破坏性操作防护 | 心智模型、操作模式、交付标准、深度分析 |
| 知识管理 | `tasks/blacklist` + `tasks/lessons` | `.agents/context/` |
| 冲突时 | **CLAUDE.md 覆盖 axiom** | — |

### 概念重叠（8 处，方向一致）

| 重叠规则 | CLAUDE.md | axiom | 关系 |
|----------|-----------|-------|------|
| 优先级裁决 | Safety > Verify > ... > Speed | H-1 | axiom → CLAUDE.md 提炼 |
| 失败处理 | 3连败→Replan, 5总败→停 | H-5 | 完全一致 |
| 最小变更 | 最小安全变更 | H-6 | 完全一致 |
| 依赖纪律 | 复用现有 > 引新 | H-7 | 完全一致 |
| 破坏性操作 | 双重 DELETE | H-8 | 完全一致 |
| 渐进式 Spec | 简单/中等/复杂三档 | SKILL.md | CLAUDE.md 来源于 axiom |
| 计划模板 | `tasks/plan_*.md` | SDM Phase 1-3 | axiom 是超集 |
| TDD | Red→Green→Refactor | 标准 E + Debug | 方向一致，axiom 更严格 |

### 已知覆盖（CLAUDE.md 覆盖 axiom）

- **注释语言**：CLAUDE.md 的中文注释要求覆盖 axiom 标准G 的英文注释要求
- **Approval Gate**：CLAUDE.md 细化——仅破坏性/范围扩展/非局部变更需显式批准，普通 bugfix 自主进行

---

## 表达风格识别

axiom 的表达 DNA 量化特征：

| 特征 | 指标 | 含义 |
|------|------|------|
| 结论先行 | 7/7 | 每段第一句是最重要判断 |
| 确定性语气 | 5.7:1 | 「必须」「禁止」远多于「建议」 |
| 结构化输出 | 54% | 超过一半内容是表格/列表/代码块 |
| 正式风格 | 7/7 | 零口语、零幽默、零铺垫 |
| 短句 | 6/7 | 平均 42 字符，55% < 40 字符 |

### 禁忌表达

axiom 从不使用：perhaps, maybe, possibly, roughly, hack, workaround, 我觉得, 我认为, 也许, 可能

---

## 最佳实践

### DO

- 提供具体的项目路径和文件位置
- 在复杂任务中耐心走完 SDM 流程
- 回应 Scope 阶段的澄清问题
- 在 Approve 阶段认真审查 RFC

### DON'T

- 不要期望 axiom 跳过 Approve 直接写代码
- 不要在快速原型场景强制使用 SDM（用 Micro-Task）
- 不要期望 axiom 凭空回答需要事实的问题（它会先研究）
- 不要忽略 Blocker 级别的审查发现

---

## 诚实边界

axiom 不适合以下场景（显式承认）：

1. 快速原型和 MVP 验证 — 流程过重
2. 数据科学 notebook — 测试覆盖率不现实
3. 一次性脚本 — 不需要 SDM 6 阶段
4. 缺少 `.agents/context/` 的全新项目 — 上下文驱动决策会降级
5. 需要量化性能基准的场景 — deliverable.md 要求"efficient"但无具体指标
