# AxiomOS · 安装指南

> 覆盖 Claude Code / OpenAI Codex CLI / Amazon Kiro IDE 三个 AI 编码工具

---

## 前置条件

本技能遵循**开放代理技能标准**（Open Agent Skills Standard），核心文件为 `SKILL.md`（含 YAML frontmatter 的 `name` + `description` 字段）。三个工具使用相同的技能格式，仅安装路径不同。

**仓库**：`https://github.com/IIXINGCHEN/axiom-agent-sskill`
**技能名**：`axiom`（SKILL.md 中 `name` 字段）

**关键约束**：安装后文件夹必须命名为 `axiom`（与 `name` 字段一致）。Git clone 时通过指定目标目录名实现：

```bash
# 关键：末尾的 axiom 指定目标目录名
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git <技能目录>/axiom
```

---

## 1. Claude Code（Anthropic）

### 目录结构

```
# 全局安装（所有项目可用）
~/.claude/skills/axiom/
├── SKILL.md
├── COMMANDS.md
├── EXAMPLES.md
├── USAGE.md
├── WORKFLOWS.md
├── README.md
└── references/
    ├── extraction-notes.md
    └── research/
        ├── 01-writings.md
        ├── 02-conversations.md
        ├── 03-expression-dna.md
        ├── 04-external-views.md
        ├── 05-decisions.md
        └── 06-timeline.md

# 项目级安装（仅当前项目可用）
<项目根>/.claude/skills/axiom/
└── (同上)
```

### 安装步骤

#### 方式 A：Git Clone（推荐）

```bash
# 全局安装
mkdir -p ~/.claude/skills
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git ~/.claude/skills/axiom

# 项目级安装
mkdir -p .claude/skills
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git .claude/skills/axiom
```

#### 方式 B：符号链接（适合本地开发迭代）

```bash
# 全局
mkdir -p ~/.claude/skills
ln -s "/path/to/axiom-agent-skill" ~/.claude/skills/axiom

# 项目级
mkdir -p .claude/skills
ln -s "/path/to/axiom-agent-skill" .claude/skills/axiom
```

### 激活方式

- **自动激活**：对话中提及「axiom」「axiomOS」「用 axiom 视角」
- **手动加载**：直接在对话中粘贴 `SKILL.md` 内容

### 验证

在 Claude Code 中新开对话，输入：

```
用 axiom 视角分析当前项目结构
```

如果回复以「**结论先行**」风格输出，包含结构化分析和质量门引用，说明安装成功。

### 与 CLAUDE.md 的关系

axiom 运行在 `CLAUDE.md`（全局基础纪律层）之上。两层协作，冲突时 `CLAUDE.md` 覆盖 axiom。详见 `USAGE.md`。

---

## 2. OpenAI Codex CLI

### 目录结构

```
# 用户级全局安装
~/.agents/skills/axiom/
├── SKILL.md
├── (其他文件同上)

# 项目级安装
<项目根>/.agents/skills/axiom/
└── (同上)

# 系统级（管理员）
/etc/codex/skills/axiom/
└── (同上)
```

### 安装步骤

#### 方式 A：Git Clone（推荐）

```bash
# 用户级全局
mkdir -p ~/.agents/skills
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git ~/.agents/skills/axiom

# 项目级
mkdir -p .agents/skills
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git .agents/skills/axiom
```

#### 方式 B：符号链接（适合本地开发迭代）

```bash
mkdir -p ~/.agents/skills
ln -s "/path/to/axiom-agent-skill" ~/.agents/skills/axiom
```

### 辅助配置（可选）

在 `~/.codex/config.toml` 中可配置技能行为：

```toml
# 禁用特定技能（不删除）
[[skills.config]]
path = "/path/to/axiom-distilled/SKILL.md"
enabled = false
```

在项目根目录创建 `AGENTS.md` 可提供项目级上下文指令（与技能互补，不替代）：

```markdown
# 项目指令

本项目的工程认知引擎通过 axiom 技能加载。
提及「axiom」「axiomOS」时自动激活。
```

### 激活方式

- **隐式激活**：Codex 根据请求内容自动匹配 `description` 字段
- **显式调用**：在 Codex CLI 中输入 `$axiom` 或通过 `/skills` 菜单选择

### 验证

```bash
codex "用 axiom 视角分析当前项目结构"
```

检查输出是否符合 axiom 的表达风格（结论先行、确定性语气、结构化输出）。

### 注意事项

- Codex 在每次会话启动时重新扫描技能目录，安装后需重启 Codex
- 技能采用**渐进式披露**——Codex 先只读取 `name` 和 `description`，决定使用后才加载完整 `SKILL.md`
- `AGENTS.md` 合并大小上限默认 32 KiB

---

## 3. Amazon Kiro IDE

### 目录结构

```
# 工作区级安装
<项目根>/.kiro/skills/axiom/
├── SKILL.md
├── (其他文件同上)

# 全局安装
~/.kiro/skills/axiom/
└── (同上)
```

### 安装步骤

#### 方式 A：通过 Kiro IDE 导入（推荐）

1. 在 Kiro IDE 中打开**代理引导与技能**面板
2. 点击 **"+"** → **导入技能** → 选择 **GitHub**
3. 粘贴仓库 URL：`https://github.com/<username>/axiom-agent-skill`
4. Kiro 自动识别 SKILL.md 并安装到 `.kiro/skills/axiom/`

#### 方式 B：Git Clone

```bash
# 工作区级
mkdir -p .kiro/skills
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git .kiro/skills/axiom

# 全局
mkdir -p ~/.kiro/skills
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git ~/.kiro/skills/axiom
```

#### 方式 C：符号链接（适合本地开发迭代）

```bash
mkdir -p ~/.kiro/skills
ln -s "/path/to/axiom-agent-skill" ~/.kiro/skills/axiom
```

### 辅助配置（可选）

在 `.kiro/steering/` 中创建 Steering 文件，为 axiom 提供项目上下文：

```
.kiro/steering/
├── product.md     # 产品概述
├── tech.md        # 技术栈
└── structure.md   # 架构和命名规范
```

Steering 文件通过 YAML frontmatter 控制加载方式：

```yaml
---
inclusion: always   # 始终加载（默认）
---
```

也可使用 `AGENTS.md` 标准文件：

```
# 在项目根目录放置 AGENTS.md，Kiro 会自动识别并始终包含
<项目根>/AGENTS.md
```

### 激活方式

- **自动激活**：Kiro 根据请求内容匹配 `description` 字段（CLI v1.26.0+ 自动检测技能）
- **手动引用**：在提示词中使用 `#axiom` 引用技能

### 验证

在 Kiro 的代理面板中输入：

```
用 axiom 视角分析当前项目结构
```

### 注意事项

- 文件夹名**必须**为 `axiom`（与 `name` 字段一致）
- `description` 包含中文关键词，英文请求时匹配率可能降低——如需支持英文激活，可在 `description` 中补充英文关键词
- `references/` 目录会被按需加载，符合渐进式披露
- 额外 `.md` 文件（`COMMANDS.md`、`WORKFLOWS.md` 等）需从 `SKILL.md` 中引用才能被自动读取
- Kiro 由 Anthropic Claude 驱动，axiom 的表达风格和心智模型与 Claude 原生能力高度兼容

---

## 速查对照表

| 维度 | Claude Code | OpenAI Codex CLI | Amazon Kiro IDE |
|------|------------|-----------------|-----------------|
| **全局技能目录** | `~/.claude/skills/axiom/` | `~/.agents/skills/axiom/` | `~/.kiro/skills/axiom/` |
| **项目技能目录** | `.claude/skills/axiom/` | `.agents/skills/axiom/` | `.kiro/skills/axiom/` |
| **指令文件** | `CLAUDE.md` | `AGENTS.md` | `.kiro/steering/*.md` 或 `AGENTS.md` |
| **技能格式** | SKILL.md (frontmatter) | SKILL.md (frontmatter) | SKILL.md (frontmatter) |
| **自动检测** | 是 | 是（会话启动时扫描） | 是（CLI v1.26.0+） |
| **渐进式披露** | 是 | 是 | 是 |
| **隐式激活** | 通过 description 匹配 | 通过 description 匹配 | 通过 description 匹配 |
| **显式调用** | 手动粘贴 | `$axiom` 或 `/skills` | `#axiom` |
| **AI 引擎** | Claude | GPT / o-series | Claude |
| **配置文件** | `.claude/settings.json` | `~/.codex/config.toml` | `.kiro/` 目录 |

---

## 一键安装脚本（macOS / Linux）

```bash
#!/bin/bash
# install.sh — axiom-agent-skill 全平台安装
set -e

REPO_URL="https://github.com/IIXINGCHEN/axiom-agent-sskill.git"
SKILL_NAME="axiom"

install_to() {
  local target_dir="$1"
  local label="$2"
  mkdir -p "$target_dir"

  if [ -e "$target_dir/$SKILL_NAME" ]; then
    echo "[跳过] $label — 已存在: $target_dir/$SKILL_NAME"
    return
  fi

  git clone "$REPO_URL" "$target_dir/$SKILL_NAME"
  echo "[已安装] $label → $target_dir/$SKILL_NAME"
}

# Claude Code
install_to "$HOME/.claude/skills" "Claude Code (全局)"

# OpenAI Codex CLI
install_to "$HOME/.agents/skills" "Codex CLI (全局)"

# Amazon Kiro IDE
install_to "$HOME/.kiro/skills" "Kiro IDE (全局)"

echo ""
echo "安装完成。在对应工具中提及「axiom」「axiomOS」即可激活。"
echo "更新技能: 在各 skills/axiom/ 目录下执行 git pull"
```

使用方式：

```bash
# 下载并执行
curl -sL <raw-url>/install.sh | bash

# 或 clone 后本地执行
git clone https://github.com/IIXINGCHEN/axiom-agent-sskill.git /tmp/axiom-install
cd /tmp/axiom-install
chmod +x install.sh
./install.sh
```

> **Windows 用户**：在 Git Bash 中可直接执行。或手动在各工具的 skills 目录下执行 `git clone <url> axiom`。

---

## 卸载

删除对应的技能目录：

```bash
# Claude Code
rm -rf ~/.claude/skills/axiom

# Codex CLI
rm -rf ~/.agents/skills/axiom

# Kiro IDE
rm -rf ~/.kiro/skills/axiom
```

## 更新

由于通过 git clone 安装，更新只需 pull：

```bash
# Claude Code
cd ~/.claude/skills/axiom && git pull

# Codex CLI
cd ~/.agents/skills/axiom && git pull

# Kiro IDE
cd ~/.kiro/skills/axiom && git pull
```

---

## 故障排查

| 问题 | 可能原因 | 解决方法 |
|------|---------|---------|
| 技能未被检测到 | 文件夹名不是 `axiom` | 重命名为 `axiom` |
| 提及 axiom 未激活 | `description` 未匹配 | 确认 frontmatter 格式正确（`---` 包裹） |
| Codex 中不生效 | 需要重启会话 | 重新启动 Codex |
| Kiro 导入失败 | URL 指向仓库根而非子目录 | 使用子目录 URL |
| 符号链接不工作 | Windows 权限问题 | 用开发者模式或手动复制 |
