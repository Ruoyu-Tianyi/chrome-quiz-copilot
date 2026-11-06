<h1 align="center">AI 网络答题自动化 Skill</h1>

<p align="center">
  通过浏览器扩展连接 Chrome。AI 读题或按标准答案勾选，逐题核对，由你交卷。
</p>

<p align="center">
  <a href="https://github.com/Ruoyu-Tianyi/chrome-quiz-copilot/releases/latest"><img alt="GitHub 最新版本" src="https://img.shields.io/github/v/release/Ruoyu-Tianyi/chrome-quiz-copilot?style=flat-square&amp;color=2563eb"></a>
  <a href="https://agentskills.io/specification"><img alt="Agent Skills 规范" src="https://img.shields.io/badge/Agent%20Skills-开放规范-0f766e?style=flat-square"></a>
  <a href="LICENSE"><img alt="MIT 许可证" src="https://img.shields.io/badge/License-MIT-64748b?style=flat-square"></a>
</p>

<p align="center">
  <strong><a href="https://github.com/Ruoyu-Tianyi/chrome-quiz-copilot/releases/latest/download/chrome-quiz-copilot.zip">下载 ZIP</a></strong>
  · <a href="#快速开始">快速开始</a>
  · <a href="#中国大陆办公智能体">桌面端导入</a>
  · <a href="#接入-chrome">接入 Chrome</a>
</p>

## 快速开始

**1. 安装 Skill。** 可直接把下面这句话发给智能体。

```text
请从 https://github.com/Ruoyu-Tianyi/chrome-quiz-copilot 下载并安装 chrome-quiz-copilot Skill，使用当前智能体支持的技能目录或导入入口，保留 SKILL.md 和 references/，完成后告诉我如何调用。
```

如果当前智能体需要你手动导入，可以[下载 ZIP](https://github.com/Ruoyu-Tianyi/chrome-quiz-copilot/releases/latest/download/chrome-quiz-copilot.zip)，再按[桌面端导入步骤](#中国大陆办公智能体)操作。

**2. 连接 Chrome。** 按[浏览器接入说明](#接入-chrome)启用连接，然后在你自己的 Chrome 里打开允许使用辅助工具的练习。

**3. 让智能体开始。** 直接发给它下面这句话。

```text
使用 chrome-quiz-copilot 填写我在 Chrome 打开的练习。只上下滚动和点击选项，填完逐题核对，交卷由我确认。
```

## 使用场景

| 你可以这样说 | 智能体会怎么做 |
| --- | --- |
| 「根据页面上的题目作答。」 | 识别试卷，根据题干作答，再回读实际勾选状态。 |
| 「这份附件有标准答案，按它重新填一遍。」 | 提取标准答案，按题号和选项文本对应后重填。 |
| 「继续下一部分，我已打开。」 | 重新读取当前页面，确认是新的一部分，再使用本轮的题目和答案。 |

遇到已有答案冲突、题目无法对应或页面会自动提交时，智能体会说明情况并把相关操作留给你。

## 安装 Skill

仓库根目录就是 `chrome-quiz-copilot` Skill。把它放进智能体的技能目录，保留 `SKILL.md` 和 `references/` 的相对位置。支持多个智能体的项目可优先使用共享目录。

| 智能体 | 项目级目录 | 个人目录 |
| --- | --- | --- |
| [Codex](https://developers.openai.com/api/reference/cli) | `.agents/skills/` | `~/.agents/skills/` |
| [Claude Code](https://code.claude.com/docs/en/skills) | `.claude/skills/` | `~/.claude/skills/` |
| [Cursor](https://cursor.com/docs/skills#skill-directories) | `.agents/skills/` | `~/.agents/skills/` |
| [Gemini CLI](https://geminicli.com/docs/cli/skills/#discovery-tiers) | `.agents/skills/` | `~/.agents/skills/` |
| [GitHub Copilot](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills) | `.agents/skills/` | `~/.copilot/skills/` |
| [OpenClaw](https://docs.openclaw.ai/tools/skills) | `.agents/skills/` | `~/.openclaw/skills/` |
| [OpenCode](https://docs.opencode.ai/docs/skills/) | `.opencode/skills/` | `~/.config/opencode/skills/` |
| [Cline](https://docs.cline.bot/customization/skills) | `.cline/skills/` | `~/.cline/skills/` |
| [Google Antigravity](https://antigravity.google/docs/skills) | `.agents/skills/` | `~/.gemini/config/skills/` |

例如，在目标项目根目录为使用共享目录的智能体安装。Claude Code 将最后的目标路径改成 `.claude/skills/chrome-quiz-copilot`。

```sh
git clone https://github.com/Ruoyu-Tianyi/chrome-quiz-copilot.git .agents/skills/chrome-quiz-copilot
```

也可下载仓库，将 `SKILL.md` 和 `references/` 复制到上表任一适用目录下的 `chrome-quiz-copilot/`。启动或刷新智能体会话后，直接说「使用 chrome-quiz-copilot，填写我打开的 Chrome 练习」。其他支持 [Agent Skills 规范](https://agentskills.io/specification) 的宿主可使用自己的技能目录。未提供原生技能发现的宿主可以手动读入 [SKILL.md](SKILL.md)，并在需要时读入其中引用的文件。

### 中国大陆办公智能体

下载上方的 Skill 安装包。ZIP 顶层包含 `SKILL.md`、`references/` 和 `LICENSE`。支持 ZIP 的桌面端可直接上传，使用文件夹导入时请解压到名为 `chrome-quiz-copilot` 的文件夹，并保留原有目录结构。

| 智能体 | 安装 Skill | 操作已打开的 Chrome |
| --- | --- | --- |
| 腾讯 WorkBuddy | 左侧进入「专家·技能·连接器」，选择「技能 → 添加技能 → 上传技能」，上传下载的 ZIP。[技能文档](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market) | 在「设置 → 智能体 → 浏览器操控」安装 Chrome 对应扩展。确认扩展已连接后，在对话中指定当前已打开的答题页。[浏览器文档](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Right-Sidebar) |
| Kimi Work | 切换到桌面端 Work 模式，在对话中上传 ZIP，也可以提供本仓库 GitHub 链接。安装后在输入框用 `/` 选择技能。[技能文档](https://www.kimi.com/resources/skill-development-skills-for-agents) | 在「插件」中启用「Kimi 浏览器扩展」，按指引在 Chrome 安装并连接。开始前确认目标是用户打开的 Chrome 标签页，会话内置浏览器是另一个入口。[扩展文档](https://www.kimi.com/help/kimi-webbridge/kimi-webbridge-introduction) |
| 豆包工作 | 解压 ZIP，在桌面端选择「插件·技能·伙伴 → 技能 → 添加 → 上传技能」，导入解压后的完整文件夹。[技能文档](https://www.doubao.com/work/docs/zh-cn/articles/081010973544) | 在「插件 → 添加 → 新建自定义连接器」选择 STDIO，按下文配置 Playwright MCP。在「本地电脑」模式连接后先核对目标 Chrome 标签页。官方文档尚未确认内置浏览器能直接接管外部 Chrome 标签页。[插件文档](https://www.doubao.com/work/docs/zh-cn/articles/705018132598) |
| 千问办公（QwenWork） | 在「扩展 → 技能 → 添加 → 上传技能」导入 ZIP，或通过技能页上传 `SKILL.md` 与辅助文件。大陆版桌面端的技能目录为 `~/.qwenworkcn/skills/`。[技能文档](https://docs.qwenwork.cn/features/skills) · [ZIP 导入说明](https://learn.qwenwork.cn/docs/features/skills.html) | 在「扩展 → 连接器」打开「浏览器」，按引导安装 Chrome 扩展。看到「扩展已连接」后，指定当前已打开的答题页。[连接器文档](https://docs.qwenwork.cn/features/connectors) |

这些入口依据各产品的公开文档整理。导入后可先用一页练习确认智能体能读取题目与勾选状态，并执行上下滚动和选项点击。如果当前版本只能使用隔离浏览器，或只能读取网页，可以先在对话中整理答案，由你手动勾选。

## 接入 Chrome

Skill 定义答题流程。Chrome 控制能力由智能体宿主或浏览器插件提供，安装 Skill 后需单独连接。默认使用你已经打开题目的 Chrome 标签页。

使用 Playwright MCP 的扩展模式时，底层通过 `chrome.debugger` 传输 Chrome DevTools Protocol（CDP）指令。使用宿主自带的浏览器连接时，底层实现由宿主决定。[Playwright 扩展源码](https://github.com/microsoft/playwright/blob/main/packages/extension/src/relayConnection.ts) · [Chrome 扩展 API](https://developer.chrome.com/docs/extensions/reference/api/debugger)

1. **已有原生 Chrome 集成。** 优先使用宿主已有的连接，例如 [Codex 桌面端的 Chrome 扩展](https://learn.chatgpt.com/docs/chrome-extension) 或 [Claude Code 的 Chrome 集成](https://code.claude.com/docs/en/chrome)。
2. **只有本地 MCP 支持。** 安装 [Microsoft Playwright 浏览器扩展](https://github.com/microsoft/playwright/blob/main/packages/extension/README.md)，并按宿主的设置方式添加 Playwright MCP。运行端需要 Node.js 和 `npx`。下面是常见的 JSON 写法，配置位置和外层结构以宿主文档为准。

   ```json
   {
     "mcpServers": {
       "playwright": {
         "command": "npx",
         "args": ["-y", "@playwright/mcp@latest", "--extension"]
       }
     }
   }
   ```

3. **开始前确认连接。** 在同一个 Chrome 用户配置中打开答题页。若扩展弹出连接提示，由你确认目标标签页。只提供隔离浏览器或无法接入本机 Chrome 的环境，可以在对话中整理题目和答案。

实际操作取决于该宿主能否连接本机 Chrome，并在目标网页读取、滚动和点击选项。

## 文件

- [SKILL.md](SKILL.md) · 智能体入口，包含答题、重填、核对和交接规则。
- [长试卷与控件定位](references/long-quiz.md) · 按需处理页面截断、重复选项和批量点击中断。
- [MIT 许可证](LICENSE) · 可复制、修改和再分发。
