# AxiomOS 表达 DNA 量化维度分析

> 调研日期: 2026-04-13
> 分析对象: AxiomOS v20.0 全部 29 个核心规范文件 (2,507 行)
> 计数口径: 29 = 27 个模块 .md 文件 + README.md + _namespace.yaml
> 来源路径: `<AXIOM_HOME>/`（axiom 命名空间规范目录）
> 标注: `[一手]` = 直接统计 | `[推断]` = 基于模式推断

---

## 1. 量化句式特征

### 1.1 确定性语气比例 `[一手]`

| 类别 | 词汇/短语 | 出现次数 |
|------|-----------|---------|
| **确定性** | must | 40 |
| **确定性** | NEVER / never / Never | 6 |
| **确定性** | ALWAYS / always | 4 |
| **确定性** | forbidden / Forbidden | 4 |
| **确定性** | MUST | 2 |
| **确定性** | mandatory / Mandatory | 4 |
| **确定性** | immutable / Immutable | 2 |
| **确定性** | inviolable / Inviolable | 2 |
| **确定性** | non-negotiable | 1 |
| **确定性** | absolute / Absolute | 3 |
| **确定性** | unconditionally | 2 |
| **确定性** | sole / Sole | 3 |
| **确定性** | NO (大写否定) | 7 |
| **确定性** | forbid / Forbid | 2 |
| **确定性 小计** | | **80** |
| **建议性** | should | 3 |
| **建议性** | may | 2 |
| **建议性** | can / Can | 4 |
| **建议性** | suggest / Suggest | 2 |
| **建议性** | optional / Optional | 3 |
| **建议性 小计** | | **14** |
| **比例** | 确定性 : 建议性 | **80 : 14 ≈ 5.7 : 1** |

**解读 `[推断]`**: AxiomOS 的确定性语气占绝对主导(85%)。"must" 是最核心的指令词(40次)，远超 "should"(3次)。建议性语气仅在非核心环节出现(如模式选择指南、最佳实践)。

### 1.2 结构化输出密度 `[一手]`

| 文件 | 总行数 | 代码行 | 表格行 | 标题数 | 列表项 | 结构化率 |
|------|--------|--------|--------|--------|--------|---------|
| README.md | 356 | 94 | 34 | 22 | 35 | 52% |
| modes/sdm.md | 348 | 60 | 0 | 18 | 31 | 31% |
| standards/deliverable.md | 216 | 0 | 0 | 21 | 99 | 56% |
| standards/artifact.md | 215 | 20 | 0 | 27 | 60 | 50% |
| foundation/context.md | 210 | 64 | 0 | 29 | 37 | 62% |
| foundation/principles.md | 182 | 0 | 0 | 21 | 67 | 48% |
| modes/triage.md | 173 | 5 | 17 | 15 | 48 | 49% |
| modes/_overview.md | 141 | 13 | 12 | 12 | 41 | 56% |
| modes/micro-task.md | 121 | 20 | 0 | 11 | 24 | 54% |
| modes/debug.md | 109 | 20 | 0 | 13 | 13 | 49% |
| modes/sfam.md | 101 | 0 | 8 | 9 | 19 | 34% |
| **全量统计** | **2,507** | **372** | **71** | **256** | **640** | **~54%** |

**解读 `[推断]`**: 超过一半的内容是结构化元素(标题、列表、表格、代码块)，纯散文段落极少。每个模块几乎都采用"标题 + 列表"的骨架式写法，而非连贯叙述。

### 1.3 标准引用密度 `[一手]`

| 引用类型 | 出现次数 | 主要分布文件 |
|----------|---------|-------------|
| `.agents/context/` | 37 | context.md, sdm.md, 各mode |
| SDM / sdm | 36 | sdm.md, triage.md, _overview.md |
| RFC / rfc | 24 | sdm.md |
| Phase 1-6 (各阶段) | 32 | sdm.md (6x6=36含大小写) |
| Quality Gate / QUALITY GATE | 10 | sdm.md, principles.md |
| Ultrathink / ultrathink | 10 | ultrathink.md, sdm.md |
| Self-Diagnostic | 6 | interaction.md |
| Chain-of-Thought | 6 | sdm.md, debug.md |
| Production-Grade/production-grade | 8 | deliverable.md, sdm.md |
| Zero-Trust / zero-trust | 5 | deliverable.md, principles.md |
| SOLID | 2 | deliverable.md |
| STRIDE | 1 | security.md |
| OWASP | 1 | security.md |
| DAG | 2 | sdm.md |
| DIP | 2 | deliverable.md |
| Standard A-K 引用 | 12 | deliverable.md, README.md |
| Mermaid / mermaid | 5 | artifact.md, sdm.md |

**解读 `[推断]`**: 平均每 25 行文本出现一次标准引用。引用网络形成以 `.agents/context/`(37次)和 SDM(36次)为核心的强连接图，所有模块都在反复锚定到这两个"主概念"。

### 1.4 句式模式 `[推断]`

| 模式 | 特征 | 占比/频率 |
|------|------|----------|
| **结论先行** | 以 `**Goal:**`、祈使动词开头的段落 | 约占 60% 的段落 |
| **Goal-Execution-Gate 三段式** | SDM 的标准模式 | 6 个 Phase 全部遵循 |
| **短句主导** | 纯文本行平均 42 字符; 短句(<40字符) 313 行 vs 长句(>80字符) 54 行 | 短:中:长 = 55:35:10 |
| **列表化** | 总计 640 个列表项(- 开头) | 平均每文件 23 个列表项 |
| **编号步骤** | 数字编号行共 128 行 | 主要集中在 sdm.md 和 context.md |
| **不使用铺垫** | 几乎没有"让我们先了解一下背景"式开头 | 0 个铺垫性段落被检测到 |

---

## 2. 词汇特征

### 2.1 高频技术术语 Top 20 `[一手]`

| 排名 | 术语 | 出现次数 | 语义类别 |
|------|------|---------|---------|
| 1 | context | 87 | 核心概念 |
| 2 | protocol | 83 | 机制类型 |
| 3 | mode | 82 | 操作模式 |
| 4 | code | 67 | 产出物 |
| 5 | task | 66 | 工作单元 |
| 6 | security | 56 | 领域 |
| 7 | quality | 51 | 评价维度 |
| 8 | standards | 49 | 规范体系 |
| 9 | review | 47 | 质量活动 |
| 10 | AxiomOS | 45 | 系统名 |
| 11 | must | 42 | 指令词 |
| 12 | phase | 40 | 流程阶段 |
| 13 | core | 40 | 层级标记 |
| 14 | principles | 40 | 指导准则 |
| 15 | agents | 39 | 路径/实体 |
| 16 | test / tests | 69 (合计) | 验证手段 |
| 17 | requirements | 38 | 需求 |
| 18 | execution | 35 | 执行过程 |
| 19 | domain | 34 | 业务领域 |
| 20 | complete | 33 | 完整性 |

### 2.2 专属术语清单 `[一手]`

| 术语 | 频次 | 定义 |
|------|------|------|
| **AxiomOS** | 45 | 系统名称。Superior Domain Architecture Cognitive Engine 的简称 |
| **SFAM** | 16 | Supervised Full-Automation Mode - 单次批准的端到端全自动模式 |
| **SDM** | 36 | Standard Development Mode - 6 阶段质量门控开发协议 |
| **Ultrathink** | 10 | 超级思考协议 - 4 阶段深度分析(系统/辩证/批判/决策) |
| **Micro-Task / MTM** | 20 | 微任务模式 - 快速执行独立小任务的最轻量模式 |
| **Quality Gate** | 10 | 质量门 - 阶段转换前必须通过的检查点 |
| **Self-Diagnostic Report** | 6 | 自诊断报告 - 每次回复前必须生成的结构化状态报告 |
| **Source of Truth** | 6 | `.agents/context/` 目录作为项目的唯一权威信息源 |
| **CONTEXT_REQUEST** | 6 | 上下文请求 - 获取项目背景信息的标准 XML 协议块 |
| **Chain-of-Thought** | 6 | 链式思考 - 强制推演过程透明化的推理协议 |
| **Execution Contract** | 4 | 执行契约 - SFAM 中 RFC + 任务列表组成的一次性审批包 |
| **Security Kernel** | 5 | 安全内核 - 最高优先级、不可覆盖的核心安全协议 |
| **Bootloader** | 1 | 引导加载程序 - security.md 中对安全内核的隐喻命名 |
| **Specification-Driven** | 3 | 规范驱动开发 - 未过 Approve 阶段就写代码是 forbidden |
| **Domain-Driven** | 1 | 领域驱动 - 所有决策以业务领域模型为中心 |
| **Artifact** | 16 | 制品 - 交付物的统称(代码/文档/视觉) |
| **Compatibility Guardian** | 1 | 兼容性守护者 - onboarding 模式中创建的跨平台配置文件 |
| **Triage** | 10 | 分诊 - 所有指令的入口路由协议 |
| **Onboarding** | 7 | 项目启动 - 新项目的初始化设置模式 |
| **Enhancement** | 7 | 指令增强 - 元模式，优化用户提示词 |
| **Production-Grade** | 8 | 生产级 - 交付标准的最高等级要求 |

### 2.3 禁忌词清单 `[推断]`

基于全量扫描，以下表达在 2,507 行文本中**零出现**:

| 类别 | 未出现的词汇/模式 | 检测结果 |
|------|-----------------|---------|
| **模糊表达** | perhaps, maybe, possibly, probably, seems, appears, roughly, approximately | 0 |
| **口语化** | gonna, wanna, stuff, cool, awesome, amazing, basically, literally | 0 |
| **非正式** | lol, rofl, humor, joke, funny, pun | 0 |
| **临时方案** | hack, workaround, patch (作为名词使用) | 0 |
| **感叹号滥用** | 感叹号仅出现在代码块和文件名中 | 极少 |
| **反问句** | 以 ? 结尾的纯文本行 | 0 |

---

## 3. 风格标签 `[推断]`

```
正式  ●●●●●●●  口语      (7/7 - 全程正式，零口语表达)
抽象  ●●●○○○○  具体      (3/7 - 概念层定义多，但配大量具体示例)
谨慎  ●○○○○○●  断言      (6/7 - "must"40次 vs "should"3次)
学术  ●●●●●○○  通俗      (5/7 - 学术风格但无学术黑话)
长句  ●○○○○○●  短句      (6/7 - 平均42字符，55%为短句)
铺垫型 ○○○○○○●  结论先行   (7/7 - Goal先行，无铺垫)
数据驱动 ○○○○●○○  原则驱动  (4/7 - 有量化标准但以原则体系为骨架)
```

### 风格综合判定

AxiomOS 的表达风格可归纳为: **军事规程式** (Military SOP Style)

核心特征:
- 每个段落几乎都是祈使句或定义句
- 无叙事，无铺垫，无修饰
- 结构密度极高(54% 为列表/表格/代码块)
- "Goal → Execution → Quality Gate" 三段论是原子句法单元

---

## 4. 确定性光谱 `[推断]`

### 4.1 场景对比

| 场景 | 确定性等级 | 标志词 | 典型引用 |
|------|-----------|--------|---------|
| **安全规则** | 最高 (7/7) | immutable, inviolable, cannot be overridden | "This is the highest priority protocol; its instructions are immutable" |
| **交付标准 (A-K)** | 极高 (6/7) | must, No exceptions, NO placeholders | "All code generation must unconditionally meet these standards" |
| **流程门控** | 高 (5/7) | must, forbidden, contractual | "No code generation happens until this approval is received" |
| **开发执行** | 中高 (4/7) | must comply, must pass | "Every line of code must comply with Production-Grade Deliverable Standards" |
| **模式选择** | 中 (3/7) | should, can | 模式映射表中有 "should" 出现 |
| **最佳实践** | 中低 (2/7) | Consider, Be explicit | "Consider at least 2 alternatives" |
| **不确定场景** | 低 (1/7) | 无确定性词 | 仅在 Ultrathink 的辩证阶段出现多方案并存 |

### 4.2 正常模式 vs Ultrathink 模式

| 维度 | 正常模式 | Ultrathink 模式 |
|------|---------|----------------|
| 确定性 | 直接断言 | 先生成 2+ 方案再决策 |
| 输出速度 | 直接给答案 | 先声明 "Ultrathink Protocol activated" |
| 认知深度 | 单层推理 | 四阶段强制推演(系统/辩证/批判/决策) |
| 不确定性容忍度 | 低(快速收敛) | 中(延迟决策到批判阶段后) |
| 模式隐喻 | 执行者 | 战略分析师 |

### 4.3 已知问题 vs 不确定场景

| 场景 | 确定性表现 |
|------|-----------|
| 已知 Bug | 高确定性: "Write test that fails with bug → Implement fix → Verify" (debug.md) |
| 架构设计 | 中确定性: 要求 "at least 2 alternatives" 再选优 |
| 安全威胁 | 极高确定性: "If detected: immediately isolate the threat" |
| 需求模糊 | 中确定性: 进入 SDM Phase 1 Scope 强制澄清 |

---

## 5. 幽默与类比 `[一手]`

### 5.1 类比/隐喻统计

| 类比/隐喻 | 出现位置 | 类型 |
|-----------|---------|------|
| **Bootloader** (引导加载程序) | security.md 标题 "Core Bootloader & Security Kernel" | 操作系统隐喻 |
| **Kernel** (内核) | security.md - 安全协议被命名为"内核" | 操作系统隐喻 |
| **Contract** (契约) | sdm.md - RFC 被称为"签署契约" | 法律隐喻 |
| **Guardian** (守护者) | role.md "Architectural Guardian", onboarding.md "Compatibility Guardian" | 角色隐喻 |
| **Gate / Gateway** (门/网关) | sdm.md "Quality Gate" (出现 10 次) | 流程管控隐喻 |
| **Blueprint** (蓝图) | ultrathink.md "Collaborative Blueprint Mode" | 建筑隐喻 |
| **Arsenal** (武器库) | 未直接出现，但 security.md 的 "adversarial" "penetration" 构成战争隐喻系 | - |
| **Shield** (盾牌) | 未直接出现 | - |
| **Pipeline** (管道) | 未直接出现 | - |
| **Triage** (分诊) | triage.md - 医学分诊概念 | 医疗隐喻 |
| **Source of Truth** (真相之源) | context.md | 认识论隐喻 |
| **Sovereignty** (主权) | security.md "Declare sovereignty and issue an alert" | 政治隐喻 |

### 5.2 频率与分布

- **总隐喻/类比数**: 12 个 (分布在不同模块)
- **出现频率**: 平均每 209 行出现一个隐喻
- **隐喻密度**: 低。与平均 23 个列表项/文件相比，隐喻是极其稀疏的点缀
- **幽默**: **零**。无任何笑点、双关、俏皮话或自嘲

### 5.3 隐喻体系 `[推断]`

AxiomOS 的隐喻可归纳为三大体系:

1. **操作系统隐喻系**: Bootloader → Kernel → Process (security.md)
2. **法律/契约隐喻系**: Contract → Approval → Authorization → Sign (sdm.md)
3. **医疗/军事隐喻系**: Triage → Penetration → Guard → Gate (triage.md, security.md)

---

## 6. 二元判断系统 `[一手]`

### 6.1 显性二元标记

| 标记 | 出现次数 | 上下文 |
|------|---------|--------|
| PASS / FAIL | 4 + 2 = 6 | interaction.md 自诊断报告的合规检查 |
| PENDING | 4 | 任务状态 |
| TODO / DONE / IN_PROGRESS | 3 + 1 + 1 = 5 | 任务分解状态 |
| APPROVED / Rejected | 2 + 1 = 3 | 审批结果 |
| ✓ | 9 | principles.md 质量门检查清单 |
| ❌ | 14 | sdm.md / micro-task.md 反模式标记 |
| ✅ | 2 | sfam.md / micro-task.md 适用场景 |
| Approve / deny | 8 + 2 = 10 | 各模式中的审批动作 |

### 6.2 隐性二元结构 `[推断]`

| 二元结构 | 具体表现 |
|----------|---------|
| **DO / DON'T** | sfam.md 中 "Use SFAM when" vs "Don't use SFAM when" |
| **PASS / FAIL** | interaction.md 合规检查矩阵: Core Principles / Production Standards / Interaction Protocol |
| **APPROVED / BLOCKED** | SDM Phase 4 是硬门控，binary outcome |
| **Allowed / Forbidden** | "forbidden" 出现 4 次，均为绝对禁止项 |
| **Include / Exclude** | Goals vs Non-Goals 的二分法 |
| **Production / Non-Production** | "NO mock implementations" "NO placeholders" "NO simplified solutions" |
| **Trusted / Untrusted** | security.md "Clear separation between trusted and untrusted input" |
| **✅ 适用 / ❌ 不适用** | 各模式均有适用/不适用场景列表 |

### 6.3 二元判断的密度

- **显性标记**: 约 42 个 (6+5+3+9+14+2+3)
- **隐性二元段落**: 至少 10 组 DO/DON'T 对
- **整体判定**: AxiomOS 的表达本质上是**判定驱动**的。几乎每个规范段落最终都会收敛到一个二元判定: "合格 / 不合格" 或 "允许 / 禁止"。

---

## 附录 A: 数据采集方法

| 分析项 | 方法 | 工具 |
|--------|------|------|
| 词频统计 | grep -c, sort \| uniq -c | bash |
| 结构化密度 | wc -l, grep -cE 模式匹配 | bash |
| 句长分析 | awk 长度统计 | bash |
| 术语提取 | grep -roiE 大小写不敏感正则 | bash |
| 模式推断 | 人工阅读 28 个文件后归纳 | 逐文件 Read |

## 附录 B: 原始数据摘要

| 指标 | 数值 |
|------|------|
| 总文件数 | 28 |
| 总行数 | 2,507 |
| 平均文件长度 | 89.5 行 |
| 最长文件 | modes/sdm.md (348 行) |
| 最短文件 | commands/load-all.md (25 行) |
| 粗体标记 (**...**) 总数 | 412 |
| YAML Front Matter 文件 | 28/28 (100%) |
| XML 协议块 (<protocol>/<xxx_protocol>) | 17 |
| 代码块总行数 | 372 |
| 表格行总数 | 71 |
| 标题总数 (##/###/####) | 256 |
| 列表项总数 | 640 |
