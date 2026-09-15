# AI Workflow Advisor

飞书文档、Excel、会议纪要——你每天碰的这些东西，其实已经有 CLI 和 MCP 能接管一半。问题是没人告诉你该装哪个，也没人说清装了之后它会读你哪些文件。

这个 Skill 先**只读**扫一遍你的工作区，告诉你现在有哪些能力缺口，再按顺序推荐该装什么。每条推荐都附官方入口、权限范围、验证命令和卸载方式。默认不读文件正文、不碰密钥、不执行安装。

## 30 秒装上

```bash
npx skills add Ming00777/ai-workflow-advisor
```

装完对你的 Agent 说：

> 帮我分析当前工作区适合安装哪些 CLI、MCP 和 Agent，先只读扫描，不要安装。

## 为什么做这个项目

国内常用的 CLI、MCP 和 Agent 分散在不同官网、GitHub 仓库和文档中，工具更新后，用户经常不知道已有能力发生了变化。本项目把工具目录、适用场景、安装前提和安全信息整理成可被 AI Agent 使用的技能，让用户先了解自己的缺口，再按优先级配置工具。

## 当前版本

第一版包含一个用户入口 Skill 和三个可组合的内部 Skill：

- `ai-workflow-advisor`：用户打开的入口，串联审计、推荐和配置引导。

- `workspace-audit`：在明确授权后检查当前工作区的文件类型、项目依赖、已安装命令和常见配置痕迹，只输出能力画像，不读取敏感内容。
- `tool-recommendation`：根据用户明确的工作目标与画像，从目录中推荐 CLI、MCP 和 Agent，解释推荐理由和不推荐原因。
- `setup-guide`：为已选工具生成官方安装、授权、只读验证和卸载步骤。遇到没有稳定官方入口的项目，明确标为社区项目或仅提供产品介绍。

## 安装

### 使用 Skills CLI

```bash
npx skills add Ming00777/ai-workflow-advisor
```

如果只想安装用户入口 Skill：

```bash
npx skills add Ming00777/ai-workflow-advisor --skill ai-workflow-advisor
```

全局安装到当前用户的 Agent 环境：

```bash
npx skills add Ming00777/ai-workflow-advisor --skill ai-workflow-advisor --global
```

### 也可以让 Agent 安装

将下面这句话发送给支持 Skills 的 Agent：

```text
安装这个 Skill：https://github.com/Ming00777/ai-workflow-advisor/tree/main/skills/ai-workflow-advisor
```

安装完成后，可以这样开始：

```text
帮我分析当前工作区适合安装哪些 CLI、MCP 和 Agent，先只读扫描，不要安装。
```

`npx skills add` 的参数格式参考开放 Skills CLI 文档；安装前请检查仓库内容、权限范围和目标 Agent。该命令会从 GitHub 获取文件，具体安装位置由 CLI 和 `--global` 选项决定。

## 首批目录

| 类型 | 项目 | 状态 |
|---|---|---|
| CLI | 飞书官方 Lark/Feishu CLI | 已收录，官方 GitHub |
| CLI | Kimi Code CLI | 已收录，官方文档 |
| CLI | 腾讯云 CodeBuddy CLI | 已收录，官方文档 |
| CLI | 百度网盘 CLI | 已收录为社区项目，安装前核对来源 |
| Agent | 扣子 Agent | 已收录，官方文档 |
| Agent | 腾讯 WorkBuddy | 已收录为产品候选，暂不声称有公开 CLI |
| Agent | 通义灵码 / Qwen 办公相关产品 | 作为待核验候选，不生成虚构安装命令 |
| MCP | 扣子官方文档 MCP | 已收录，官方文档 |
| MCP | 飞书能力 | 通过官方 CLI / 开放平台配置，按用户场景推荐 |
| MCP | CodeBuddy MCP 管理能力 | 已收录，官方文档 |

完整字段见 `catalog/`。目录里的“官方”“社区”“待核验”状态是有意保留的，不把搜索结果当成官方背书。

## 使用方式

将 `skills/` 下的 Skill 放入支持 `SKILL.md` 的 Agent 工作区，然后使用类似请求：

> 帮我检查当前工作区能看到哪些工具缺口，我主要处理飞书文档、Excel 和会议纪要。先只读扫描，不要安装任何东西。

Skill 应先询问授权范围，再执行检查。推荐结果应包含：适用原因、官方入口、前置条件、权限范围、验证方式、风险和退出方式。

### 只读试运行

可以直接请求：

> 帮我分析当前工作区适合安装哪些 CLI、MCP 和 Agent，先只读扫描，不要安装。

试运行会报告扫描范围、文件类型、项目依赖、可检测到的命令和未检查的信息。没有发现某个文件或工具，只表示它不在本次扫描范围内；最终推荐还必须结合用户自己描述的工作方式。

## 安全边界

- 默认只读，不执行安装、不写入配置、不登录第三方服务。
- 不读取或展示 API Key、Cookie、Token、OAuth refresh token 和私密文件正文。
- 不因为发现某个文件类型就断言用户的工作习惯；区分事实、推断和待确认假设。
- 外部工具的版本、许可证、权限和官方链接需要在目录中记录验证日期。
- 社区 CLI 不冒充官方项目；使用前提醒用户审阅源码、发布页和权限。

## 目录结构

```text
ai-workflow-advisor/
├── README.md
├── skills/
│   ├── ai-workflow-advisor/SKILL.md
│   ├── workspace-audit/SKILL.md
│   ├── tool-recommendation/SKILL.md
│   └── setup-guide/SKILL.md
├── catalog/
│   ├── clis.yaml
│   ├── mcps.yaml
│   └── agents.yaml
├── examples/
├── docs/
└── LICENSE
```

项目目前是本地第一版，尚未发布到 GitHub，也没有自动安装器。真正发布前，需要补充评估用例、链接健康检查和版本更新流程。
