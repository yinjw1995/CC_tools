# requirement-skills

智驾软件需求标准化全流程 Skills

## 安装

### 方式一：复制到插件目录（永久安装，推荐）

```bash
# Windows Git Bash 环境
cp -r ./requirement-skills ~/.claude/plugins/
```

或手动操作：将整个 `requirement-skills` 文件夹复制到 `~/.claude/plugins/` 目录下。

**最终结构应为**：
```
~/.claude/plugins/requirement-skills/
├── .claude-plugin/
│   └── plugin.json
└── skills/
    ├── require/SKILL.md
    ├── cts-intake/SKILL.md
    └── ... (其他 6 个 skills)
```

**更新 skills**：修改 skills 后，只需重新复制 skills 目录：
```bash
cp -r ./requirement-skills/skills ~/.claude/plugins/requirement-skills/
```

### 方式二：临时加载（当前会话有效）

```bash
claude --plugin-dir "./requirement-skills/.claude-plugin"
```

### Windows 环境注意

如果遇到 "requires git-bash" 错误，需要设置环境变量：

```bash
export CLAUDE_CODE_GIT_BASH_PATH="D:/Program Files/Git/usr/bin/bash.exe"
claude --plugin-dir "./requirement-skills/.claude-plugin"
```

或使用完整路径：

```bash
CLAUDE_CODE_GIT_BASH_PATH="D:\\Program Files\\Git\\usr\\bin\\bash.exe" claude --plugin-dir "d:/Work/需求标准化项目/requirement-skills/.claude-plugin"
```

## Skills 列表

| Skill | 说明 | 触发示例 |
|-------|------|---------|
| `require` | 一键生成 SwRS，自动串联所有环节 | "生成 SwRS" 或 "从 CTS 生成需求" |
| `cts-intake` | CTS 准入审查 | "审查 CTS" 或 "CTS 准入检查" |
| `boundary-def` | 软件边界定义 | "定义软件边界" 或 "划分软件职责" |
| `fc-extract` | FC 功能提取 | "提取功能需求" 或 "生成 FC 清单" |
| `module-decomp` | 模块分解 | "模块分解" 或 "功能分配到模块" |
| `swrs-write` | SwRS 软件需求编写 | "编写 SwRS" 或 "生成软件需求规格" |
| `quality-gate` | 质量网关审查 | "质量审查" 或 "检查 SwRS 质量" |
| `change-track` | 变更跟踪 | "跟踪变更" 或 "分析变更影响" |

## 使用

**重要**：Skills 不是通过 `/command` 调用，而是通过自然语言触发。

```bash
# ❌ 错误方式
/require ./CTS_泊车功能.docx

# ✅ 正确方式
"帮我从 CTS_泊车功能.docx 生成 SwRS"
"审查这个 CTS 文档的完备性"
"定义泊车功能的软件边界"
```

Skills 会根据你的描述自动激活，无需手动调用命令。
