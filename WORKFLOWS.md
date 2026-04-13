# AxiomOS · 详细工作流

> 涵盖 init → prd → plan → execute → review 五大核心流程

---

## 流程总览

五大核心流程: init (初始化环境) → prd (需求文档) → plan (实施计划) → execute (执行落地) → review (质量审查)

输出路径: `.agents/init/` → `.agents/prds/` → `.agents/plans/` → 实际代码 → `.agents/code-reviews/`

```
用户需求
  │
  ▼
┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
│  init   │───▶│   prd   │───▶│  plan   │───▶│ execute │───▶│ review  │
│初始化环境│    │需求文档 │    │实施计划 │    │执行落地 │    │质量审查 │
└─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘
     │              │              │              │              │
     ▼              ▼              ▼              ▼              ▼
.agents/init/   .agents/prds/ .agents/plans/  实际代码      .agents/
                                                           code-reviews/
```

---

## 1. Init — 项目初始化

> 分析项目结构，生成可执行的初始化指南。

**输入**: 项目路径（默认当前目录）
**输出**: `.agents/init/{project-name}.md`

### Process

#### Step 1: 分析项目结构

识别：
1. **构建系统**: package.json, pyproject.toml, go.mod, Cargo.toml, Makefile
2. **包管理器**: npm/yarn/pnpm | uv/pip/poetry | go mod | cargo
3. **运行时环境**: Node.js / Python / Go 版本
4. **框架**: Next.js, Vite, React, FastAPI, Django, Gin
5. **开发工具**: eslint, prettier, pytest, jest, mypy, ruff

#### Step 2: 生成初始化步骤

1. **Prerequisites** — 必需运行时和工具
2. **Dependencies** — 包安装命令
3. **Environment Setup** — .env 配置
4. **Start Commands** — 开发服务器命令
5. **Common Commands** — test, build, lint 命令

#### Quality Criteria

- [ ] 所有运行时和工具要求已识别
- [ ] 命令可执行且非交互式
- [ ] 包含验证命令
- [ ] 常用命令已记录

---

## 2. PRD — 产品需求文档

> 从对话中生成完整的产品需求文档。

**输入**: 用户需求（对话上下文）
**输出**: `.agents/prds/{feature-name}.md`

### Process

#### Step 1: 提取需求

- 回顾对话历史，识别明确和隐含需求
- 记录技术约束和偏好
- 捕获成功标准

#### Step 2: 综合信息

- 组织到适当章节
- 缺少细节处填入合理假设
- 确保跨章节一致性

### PRD Structure（15 章节）

1. **Executive Summary** — 产品概述，核心价值
2. **Mission** — 使命声明，核心原则
3. **Target Users** — 用户画像，痛点
4. **MVP Scope** — 核心功能 vs 延期功能
5. **User Stories** — 5-8 个用户故事
6. **Core Architecture** — 高层架构，目录结构
7. **Tools/Features** — 详细功能规格
8. **Technology Stack** — 前后端技术及版本
9. **Security & Config** — 认证授权，配置管理
10. **API Specification** — 端点，请求/响应格式
11. **Success Criteria** — 功能需求，质量指标
12. **Implementation Phases** — 3-4 个阶段
13. **Future Considerations** — MVP 后增强
14. **Risks & Mitigations** — 3-5 个关键风险
15. **Appendix** — 相关文档和依赖

### Quality Criteria

- [ ] 所有章节存在
- [ ] 用户故事有明确收益
- [ ] MVP 范围现实
- [ ] 技术选型有理由
- [ ] 成功标准可衡量

---

## 3. Plan — 制定实施计划

> 将功能请求转化为完整的实施计划。

**输入**: 功能名称/需求描述
**输出**: `.agents/plans/{feature-name}.md`

### Core Principle

**本阶段不写代码。** 目标是创建使执行一次通过的计划。

### Process

#### Phase 1: 功能理解

- 提取核心问题
- 确定功能类型：New / Enhancement / Refactor / Bug Fix
- 评估复杂度：Low / Medium / High

#### Phase 2: 代码库情报收集（并行）

1. **项目结构** — 语言、框架、目录结构
2. **模式识别** — 搜索相似实现，识别编码约定
3. **依赖分析** — 外部库和集成方式
4. **测试模式** — 框架、结构、示例
5. **集成点** — 需更新的文件和需创建的新文件

#### Phase 3: 外部研究

- 最新库版本和最佳实践
- 官方文档和实现示例
- Breaking changes 和迁移指南

#### Phase 4: 深度战略思考

- 如何适配现有架构
- 关键依赖和操作顺序
- 边缘情况和错误场景
- 性能和安全考虑

#### Phase 5: 生成计划

### Output Structure

```markdown
# Feature: {name}

## Feature Description
## User Story
## Problem Statement
## Solution Statement
## Feature Metadata

## CONTEXT REFERENCES
### Relevant Codebase Files
### New Files to Create
### Patterns to Follow

## IMPLEMENTATION PLAN
### Phase 1: Foundation
### Phase 2: Core Implementation
### Phase 3: Integration
### Phase 4: Testing & Validation

## STEP-BY-STEP TASKS
## TESTING STRATEGY
## VALIDATION COMMANDS
## ACCEPTANCE CRITERIA
```

### Quality Criteria

- [ ] 所有必要模式已识别
- [ ] 每项任务有可执行验证命令
- [ ] 任务按依赖排序
- [ ] 其他开发者可无额外上下文执行

---

## 4. Execute — 执行实施

> 按计划顺序执行。

**输入**: 计划文件 `.agents/plans/{feature-name}.md`
**输出**: 实施报告

### Core Principle

严格按计划执行。计划未覆盖的问题记录并说明。

### Process

#### Step 1: 阅读理解

- 阅读整个计划
- 理解所有任务和依赖
- 记录验证命令

#### Step 2: 按顺序执行

每个任务：
- **a. 定位** — 识别文件和操作
- **b. 实现** — 遵循规格和现有模式
- **c. 验证** — 每次修改后检查语法和类型

#### Step 3: 实现测试

- 创建所有测试文件
- 覆盖边缘情况
- 遵循计划中的测试方法

#### Step 4: 运行验证命令

按顺序执行所有验证命令。失败则修复后重新运行。

#### Step 5: 最终验证

- [ ] 所有任务完成
- [ ] 所有测试通过
- [ ] 所有验证命令通过
- [ ] 代码遵循项目约定

---

## 5. Review — 质量审查

### 5A. Code Review — 代码审查

**类型**: 轻量级 diff 审查
**输入**: Git 变更
**输出**: `.agents/code-reviews/{name}.md`

#### 分析维度

1. **逻辑错误** — 条件判断、边界处理、空指针
2. **安全问题** — SQL 注入、XSS、敏感数据暴露
3. **性能问题** — N+1 查询、无超时、内存泄漏
4. **代码质量** — 命名、结构、重复代码
5. **规范遵循** — 标准 A-L 对照

#### 输出格式

```markdown
## Stats
## Top Issues
  severity: critical|high|medium|low
  file: path
  line: N
  issue: [描述]
  suggestion: [修复建议]
```

### 5B. Code Review Pro — 深度结构审查

**Scope**: diff | staged | all | repo
**Profile**: standard | strict

#### Strict Profile 要求

1. **Spatial Analysis** — 模块依赖一致性、无环、分层边界
2. **System Analysis** — 端到端流程、API 验证、数据库操作
3. **Reverse-Engineering** — 行为与实现匹配、异常处理覆盖真实失败
4. **No Mock Data Policy** — 生产路径无 mock/stub
5. **Production Readiness Gate** — 无 placeholder、显式错误处理、超时设置

### 5C. Validate — 全面验证

**验证层级**：

1. **Syntax & Linting** — eslint / ruff / gofmt
2. **Type Checking** — mypy / tsc / golangci-lint
3. **Unit Tests** — pytest / jest / vitest
4. **Integration Tests** — cypress / playwright
5. **Build Validation** — npm build / cargo build
6. **Security Checks** — 依赖审计、秘钥检查

### 5D. Execution Report — 执行报告

**依赖**: workflow:execute

分析 plan vs actual，记录偏差：
- [通过] Good Divergence
- [未通过] Bad Divergence

### 5E. System Review — 流程复盘

**依赖**: plan + execution-report

追溯偏差根因，生成流程改进建议。

---

## 流程间数据流

```
init  ──────────────────▶ .agents/init/{name}.md
prd   ──────────────────▶ .agents/prds/{feature}.md
plan  ──────────────────▶ .agents/plans/{feature}.md
                              │
                              ▼
                        execute（读取 plan）
                              │
                              ▼
execute ────────────────▶ .agents/execution-reports/
                              │
                              ▼
                        review 各子流程
                        ├── code-review
                        ├── code-review-pro
                        ├── validate
                        ├── execution-report
                        └── system-review
```

---

## 命令速查

| 命令 | 用途 | 输出 |
|------|------|------|
| `/axiom:init` | 初始化项目 | `.agents/init/{name}.md` |
| `/axiom:prd` | 生成 PRD | `.agents/prds/{feature}.md` |
| `/axiom:plan` | 制定计划 | `.agents/plans/{feature}.md` |
| `/axiom:execute` | 执行计划 | 实施报告 |
| `/axiom:review` | 代码审查 | `.agents/code-reviews/{name}.md` |
| `/axiom:validate` | 全面验证 | `.agents/validation/{project}.md` |
| `/axiom:execution-report` | 执行报告 | `.agents/execution-reports/` |
| `/axiom:system-review` | 流程复盘 | `.agents/system-reviews/` |
