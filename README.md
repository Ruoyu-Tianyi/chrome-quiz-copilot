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

## 接入 Chrome

Skill 定义答题流程。Chrome 控制能力由智能体宿主或浏览器插件提供，安装 Skill 后需单独连接。默认使用你已经打开题目的 Chrome 标签页。

1. **已有原生 Chrome 集成。** 优先使用宿主已有的连接，例如 [Codex 桌面端的 Chrome 扩展](https://learn.chatgpt.com/docs/chrome-extension) 或 [Claude Code 的 Chrome 集成](https://code.claude.com/docs/en/chrome)。
2. **只有本地 MCP 支持。** 安装 [Microsoft Playwright 浏览器扩展](https://github.com/microsoft/playwright/blob/main/packages/extension/README.md)，并按宿主的设置方式添加 Playwright MCP。运行端需要 Node.js 和 `npx`。下面是常见的 JSON 写法，配置位置和外层结构以宿主文档为准。

   ```json
   {
     "mcpServers": {
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--extension"]
       }
     }
   }
   ```

3. **开始前确认连接。** 在同一个 Chrome 用户配置中打开答题页。若扩展弹出连接提示，由你确认目标标签页。只提供隔离浏览器或无法接入本机 Chrome 的环境，可以在对话中整理题目和答案。

上表描述的是 Skill 的发现位置。实际操作还取决于该宿主能否连接本机 Chrome 并在目标网页读取、滚动和点击选项。

## 文件

- [SKILL.md](SKILL.md) · 智能体入口，包含答题、重填、核对和交接规则。
- [长试卷与控件定位](references/long-quiz.md) · 按需处理页面截断、重复选项和批量点击中断。
- [MIT 许可证](LICENSE) · 可复制、修改和再分发。
