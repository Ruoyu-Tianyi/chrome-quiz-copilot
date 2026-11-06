# Chrome 答题协作

一个面向网页练习和课程测验的中文 Agent Skill。用户打开题目，智能体读题或对照标准答案勾选，再逐题回读核对。交卷由用户确认。

## 使用场景

| 你可以这样说 | 智能体会怎么做 |
| --- | --- |
| 「我已在 Chrome 打开练习。请作答，只上下滚动和点击选项，交卷由我确认。」 | 识别当前试卷，根据题干作答，核对页面的实际勾选状态。 |
| 「这份附件有标准答案，按它重新填一遍。」 | 区分学生答案和标准答案，按题号和选项核对后重填。 |
| 「继续下一部分，我已打开。」 | 重新读取当前页面，确认是新的一部分，再使用本轮的题目和答案。 |

适用于允许辅助工具的练习。默认只滚动和点击选项。遇到已选答案冲突、题目无法对应或页面会自动提交时，智能体会说明情况并留给用户处理。

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

使用桌面端导入。保留 `SKILL.md` 和 `references/` 的相对位置，以便智能体在处理长试卷时读取附带指引。支持上传 ZIP 的客户端可用下面的命令在本仓库根目录生成技能包，压缩包顶层包含 `SKILL.md`。

```sh
git archive --format=zip --output=chrome-quiz-copilot.zip HEAD SKILL.md references LICENSE
```

| 智能体 | 安装 Skill | 操作已打开的 Chrome |
| --- | --- | --- |
| 腾讯 WorkBuddy | 左侧进入「专家·技能·连接器」，选择「技能 → 添加技能 → 上传技能」，上传本地技能包。[技能文档](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market) | 在「设置 → 智能体 → 浏览器操控」安装 Chrome 对应扩展。确认扩展已连接后，在对话中指定当前已打开的答题页。[浏览器文档](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Right-Sidebar) |
| Kimi Work | 切换到桌面端 Work 模式。在对话中提供本仓库 GitHub 链接，或上传本地 ZIP。安装后在输入框用 `/` 选择技能。[技能文档](https://www.kimi.com/resources/skill-development-skills-for-agents) | 在「插件」中启用「Kimi 浏览器扩展」，按指引在 Chrome 安装并连接。开始前确认目标是用户打开的 Chrome 标签页，会话内置浏览器是另一个入口。[扩展文档](https://www.kimi.com/help/kimi-webbridge/kimi-webbridge-introduction) |
| 豆包工作 | 在桌面端选择「插件·技能·伙伴 → 技能 → 添加 → 上传技能」，选择包含 `SKILL.md` 和 `references/` 的完整文件夹。[技能文档](https://www.doubao.com/work/docs/zh-cn/articles/081010973544) | 在「插件 → 添加 → 新建自定义连接器」选择 STDIO，按下文配置 Playwright MCP。在「本地电脑」模式连接后先核对目标 Chrome 标签页。官方文档尚未确认内置浏览器能直接接管外部 Chrome 标签页。[插件文档](https://www.doubao.com/work/docs/zh-cn/articles/705018132598) |
| 千问办公（QwenWork） | 在「扩展 → 技能 → 添加 → 上传技能」导入 ZIP，或通过技能页上传 `SKILL.md` 与辅助文件。大陆版桌面端的技能目录为 `~/.qwenworkcn/skills/`。[技能文档](https://docs.qwenwork.cn/features/skills) · [ZIP 导入说明](https://learn.qwenwork.cn/docs/features/skills.html) | 在「扩展 → 连接器」打开「浏览器」，按引导安装 Chrome 扩展。看到「扩展已连接」后，指定当前已打开的答题页。[连接器文档](https://docs.qwenwork.cn/features/connectors) |

这些入口依据各产品的公开文档整理。导入后可先用一页练习确认智能体能读取题目与勾选状态，并执行上下滚动和选项点击。如果当前版本只能使用隔离浏览器，或只能读取网页，可以先在对话中整理答案，由你手动勾选。

## 接入 Chrome

Skill 定义答题流程。Chrome 控制能力由智能体宿主或浏览器插件提供，安装 Skill 后需单独连接。默认使用你已经打开题目的 Chrome 标签页。

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
