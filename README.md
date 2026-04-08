# 🧠 AI Recap Skill

> **让 AI 从错误中提炼经验，写入全局记忆，不再重复犯同一个错误。**

和 AI 结对编程踩完坑后，一句 `/recap`，AI 回顾对话中的反复试错，分析你和 AI 各自犯了什么错、为什么犯错，提炼出通用经验规则，直接写入全局记忆文件（如 `CLAUDE.md` `AGENTS.md`）。下次新对话启动时，这些经验自动生效,避免同样的坑再踩一遍。

| 痛点 | 解法 |
|------|------|
| AI 反复在同一类问题上犯错 | `/recap` 提炼通用经验 → 写入全局记忆 → 以后自动规避 |
| 踩完坑后教训只留在当次对话，下次还是从零开始 | 教训写入全局配置文件，跨项目、跨对话持久生效 |
| 不知道问题出在 AI 还是自己 | recap 同时分析 AI 和用户双方的错误与根因 |
| 换了项目，经验清零 | 全局记忆不跟项目走，换 repo 教训不丢 |

## 安装

### 方式一：对话安装（推荐 ⭐）

打开你的 AI 编程工具（Claude Code、Codex 等），直接说：

```
安装这个skill https://github.com/realrxen/recap.git
```

AI 会自动克隆仓库，将 `recap` 文件夹移动到对应的 skills 目录。

### 方式二：手动安装

**macOS / Linux：**

```bash
# 克隆仓库到本地
git clone https://github.com/realrxen/recap.git

# Claude Code
cp -r recap ~/.claude/skills/recap

# Codex CLI
cp -r recap ~/.codex/skills/recap
```

**Windows：**

```powershell
# 克隆仓库到本地
git clone https://github.com/realrxen/recap.git

# 下载后手动移动到对应Agent的skills文件夹内即可 例如:
C:\Users\xxx\.claude\skills\
```


## 验证

### 触发方式

只有用户才能触发recap，AI **不会**自动触发。

| 触发方式 | 示例 |
|---------|------|
| 指令触发 | `/recap`、`$recap` |
| 自然语言触发 | "复盘"、"总结"、"总结经验"、"总结教训"、"recap" 等 |

```bash
# Claude Code
/recap

# Codex CLI
$recap
```

### 使用示例

```
You: 基于 TDesign Chat 的 Thinking 组件，参考https://tdesign.tencent.com/chat/components/chat-thinking
帮我写一个 demo，实现流式输出 Agent 的思考过程

Claude and You: [沟通多次，试了很多方法，调试了 N 轮后才搞定]
Claude and You: [沟通多次，试了很多方法，调试了 N 轮后才搞定]

You: /recap

Claude: 📝 复盘完成，已保存 2 条教训到 ~/.claude/CLAUDE.md：
        1. RECAP-2026-04-08-001: 用户提供的链接多次尝试后无法读取到有效内容,应该告知用户
           → 通用经验：用户提供的链接多次尝试后无法读取到有效内容,应该告知用户,不能通过猜测写代码。

        2. RECAP-2026-04-08-002: SSE 流式数据需要逐 chunk 拼接而非覆盖
           → 通用经验：处理流式数据时，默认使用追加（append）模式而非替换（replace）模式。                
```

### 配合 `/resume` 获取历史经验

> 在 Claude Code 或 Codex 中`/resume` 可以恢复一个已结束的历史对话。恢复会话后再调用 `/recap`，即可从之前的对话中提取教训。适合回顾昨天或上周的踩坑经历。

```
You: /resume

Claude: [显示历史对话列表]

You: [通过⬆️⬇️浏览,回车选择]

You: /recap

Claude: 📝 复盘完成，已保存 1 条教训到 ~/.claude/CLAUDE.md：

        1. RECAP-2026-04-07-001: API 调用需要重试机制
           → 通用经验：对外部 API 调用默认添加超时和重试参数，不要假设网络总是稳定的。
```


## 经验教训保存位置

经验教训保存到 AI 工具的**全局配置文件**中，AI 每次启动自动加载：

| AI 工具 | macOS / Linux | Windows |
|---------|--------------|---------|
| Claude Code | `~/.claude/CLAUDE.md` | `%USERPROFILE%\.claude\CLAUDE.md` |
| Codex CLI | `~/.codex/AGENTS.md` | `%USERPROFILE%\.codex\AGENTS.md` |

- ✅ 跨项目生效，不跟任何 repo 绑定
- ✅ 纯 Markdown 文本，可手动编辑、版本控制、分享给团队


## License

MIT