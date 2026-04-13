# AxiomOS · 命令索引

> axiom 命名空间下的所有命令

---

## 命令总览

| 命令 | 用途 | 对应模式 |
|------|------|---------|
| `/axiom:activate` | 激活 axiom 引擎 | 系统启动 |
| `/axiom:status` | 查看当前状态 | Self-Diagnostic |
| `/axiom:view` | 查看规范文件 | 参考查询 |
| `/axiom:load-all` | 加载全部规范 | 全量初始化 |

---

## 系统命令

### `/axiom:activate`

激活 AxiomOS 引擎，初始化身份和上下文。

**行为**：
1. 加载 Security Kernel（身份验证 + 注入检测）
2. 请求 `.agents/context/` 同步
3. 生成首个 Self-Diagnostic Report
4. 进入 Triage 待命状态

### `/axiom:status`

查看 axiom 当前运行状态。

**输出**：
```yaml
Self-Diagnostic Report:
  Status: "Active"
  Current Operating Mode: "[当前模式]"
  Mode Phase: "[当前阶段]"
  Task Status: "[任务状态]"
  Context Sync Status: "[上下文同步状态]"
  Compliance Check:
    Core Principles Adherence: "[PASS | PENDING | FAIL]"
    Production Standards Compliance: "[PASS | PENDING | FAIL | N/A]"
```

### `/axiom:view <path>`

查看指定规范文件内容。用于按需加载细节，而非全量加载。

**参数**：
- `path` — 相对于 `commands/axiom/` 的文件路径（如 `foundation/principles`）

### `/axiom:load-all`

全量加载所有 29 个规范文件。仅在需要完整上下文时使用。

**警告**：全量加载消耗大量 token。日常使用应通过 SKILL.md 的渐进式加载。

---

## 工作流命令

以下命令通过 axiom 命名空间访问，对应 WORKFLOWS.md 中的详细流程：

| 命令 | 流程 | 说明 |
|------|------|------|
| `/axiom:init` | Init | 分析项目结构，生成初始化指南 |
| `/axiom:prd` | PRD | 从对话生成产品需求文档 |
| `/axiom:plan` | Plan | 制定实施计划 |
| `/axiom:execute` | Execute | 执行实施计划 |
| `/axiom:review` | Review | 代码审查 |
| `/axiom:validate` | Validate | 全面验证 |
| `/axiom:execution-report` | Report | 执行报告 |
| `/axiom:system-review` | System Review | 流程复盘 |

---

## 模式切换

axiom 自动通过 Triage 路由到合适模式，也可手动指定：

| 触发方式 | 命令 |
|---------|------|
| 自动路由 | 直接描述任务（如「修复这个 bug」） |
| 手动指定 | 「用 SDM 模式」「走 Debug」 |
| 强制 Ultrathink | 「用 Ultrathink 分析」 |
| 全自动化 | 「用 SFAM 模式」 |

---

## 按复杂度选择

| 复杂度 | 推荐路径 | 命令 |
|--------|---------|------|
| 简单（改字段） | 直接执行 | 描述任务即可 |
| 中等（3+ 步骤） | 轻量 Spec | `/axiom:plan` |
| 复杂（跨模块） | 完整 SDM | `/axiom:plan` → Approve → `/axiom:execute` |
