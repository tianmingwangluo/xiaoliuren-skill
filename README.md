# 道传小六壬 AI 代理技能 (xiaoliuren-skill)小六壬skill

一个为 AI 代理（Cursor / Claude Code / OpenClaw / VS Code Copilot 等）提供专业级小六壬起卦排盘与解卦能力的技能包。

## 特点

- **算法经过审核**：修正了网络上常见的五行归属错误（留连属土、小吉属水）
- **完整知识体系**：涵盖三种起卦方式、五行生克、六亲、死活六神、六步解卦法
- **即插即用**：单一 `SKILL.md` 文件包含全部知识，AI 代理可直接加载使用
- **标准化输出**：提供排盘表和解卦的完整输出模板

## 文件结构

```
xiaoliuren-skill/
├── SKILL.md          # 主技能文件（AI代理读取此文件即可获取全部能力）
├── README.md         # 本说明文件
└── examples.md       # 起卦示例与验证用例
```

## 使用方式

### Cursor / VS Code Copilot

将 `xiaoliuren-skill` 文件夹放入项目的 `.github/skills/`、`.agents/skills/` 或 `.claude/skills/` 目录下。AI 代理在用户请求小六壬占卜时会自动调用。

### Claude Code

将 `SKILL.md` 的内容作为系统提示或工具说明提供给 Claude。

### OpenClaw / 其他 AI 代理

将 `SKILL.md` 加载为知识库或技能文件即可。

### 通用方式

直接将 `SKILL.md` 的内容粘贴到任何 AI 对话的系统提示中，即可赋予 AI 专业的小六壬起卦能力。

### DeepSeek Harness

DSH 会扫描以下技能根目录（一层深度的 `<name>/SKILL.md` 目录包或 `<name>.md` 平铺文件）：

| 优先级 | 目录 | 说明 |
| ------ | ---- | ---- |
| 项目级 | `<项目根>/.dsh/skills/` | 仅该项目会话可用 |
| 项目级 | `<项目根>/.agents/skills/` | 兼容共享 agent 配置 |
| 用户级 | `~/.dsh/skills/` | 所有会话可用（推荐） |
| 用户级 | `~/.agents/skills/` | 兼容共享 agent 配置 |

安装方法（用户级，推荐）：

```powershell
# 把整个仓库目录复制为技能包
New-Item -ItemType Directory -Force "$env:USERPROFILE\.dsh\skills\xiaoliuren-skill" | Out-Null
Copy-Item SKILL.md, examples.md "$env:USERPROFILE\.dsh\skills\xiaoliuren-skill\"
```

安装后无需重启 DSH，技能目录会热刷新：

- **自动调用**：会话中直接描述占卜需求（如"帮我用小六壬算一下今天的财运"），模型会自动加载本技能执行排盘解卦。
- **手动调用**：在输入框输入 `/xiaoliuren-divination` 可显式加载技能正文。
- **资源解析**：`SKILL.md` 正文引用的相对路径（如 `examples.md`）以技能目录为基准解析，模型会按需读取验证用例。

本技能已按 DSH 技能规范提供 frontmatter（`name`、`description`、`whenToUse`、`user-invocable`、`metadata`），同时保持与 Cursor / Claude Code 等代理的兼容。

## 核心校正说明

本技能基于道传小六壬体系，与传统/网络版本的关键差异：

| 宫位 | 道传（本技能·正确） | 网络常见（错误） |
|------|---------------------|-----------------|
| 留连 | **土** | 水 |
| 小吉 | **水** | 土 |

## 来源

来自 [道传小六壬在线排盘](https://wwww.xiao6ren.com) 项目，算法与数据经过系统性整理审核。
