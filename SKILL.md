---
name: recap
description: >
  Review the current conversation after repeated errors or struggles, analyze
  what both AI and the user did wrong and why, then distill lessons into
  general reusable rules and save them to the global memory file (CLAUDE.md
  or AGENTS.md). Use when the user says "recap", "复盘", "总结", "总结经验",
  "总结教训", or similar phrases. Only activated by the user, never
  auto-triggered.
---

# Recap Skill

Review the conversation, extract lessons from mistakes, and persist them as general rules in the global memory file so they are automatically loaded in every future session.

## Core purpose

When the user triggers recap, review the current conversation — especially cases where **multiple attempts or errors occurred before the problem was solved**. Analyze:

1. **What the AI did wrong** — Where did the AI make incorrect assumptions, miss key information, or choose the wrong approach?
2. **What the user did wrong** — Where did the user provide incomplete/inaccurate info, or fail to correct direction in time? (Write "None" if not applicable)
3. **Why it went wrong** — Root cause: missing context, unfamiliarity with framework conventions, assumptions, poor communication, etc.
4. **General rule** — Abstract the lesson into a reusable rule that applies across different projects and scenarios in the future.

## Where to save lessons

Save lessons to the **global memory file** so they are loaded automatically on every future session.

| Platform | macOS / Linux | Windows |
|----------|--------------|---------|
| Claude Code | `~/.claude/CLAUDE.md` | `%USERPROFILE%\.claude\CLAUDE.md` |
| Codex CLI | `~/.codex/AGENTS.md` | `%USERPROFILE%\.codex\AGENTS.md` |

## Lesson format

Append to the `## Lessons Learned` section. If it does not exist, create it. Never overwrite other content.

```markdown
## Lessons Learned

### RECAP-YYYY-MM-DD-NNN | <category> | <short_title>
- **AI mistake**: What the AI did wrong, at which step it went off track
- **User mistake**: What info the user failed to provide or provided incorrectly (write "None" if N/A)
- **Root cause**: Why this mistake happened
- **General rule**: One actionable sentence — a reusable guideline for future behavior
- **Solution**: How it was ultimately resolved
- **Tags**: comma, separated, tags
```

Categories: `framework-convention` · `api-integration` · `data-format` · `env-config` · `debugging` · `prompting` · `general`

## Workflow

1. **Scan the conversation** — Identify all problems that required multiple attempts or errors before being solved.
2. **Analyze each problem** — Structure the analysis per the lesson format: AI mistake, user mistake, root cause, general rule.
3. **Read the global memory file** — Check existing lessons to avoid duplicates, determine the next ID.
4. **Save directly** — Append lessons to the global memory file. **Do NOT ask the user for confirmation.**
5. **Report to user** — Tell the user what was saved, in this format:

   *"📝 Recap complete. Saved N lessons to `<file_path>`:"*
   - *RECAP-YYYY-MM-DD-NNN: `<short_title>` — `<general_rule>`*
   - *...*

   The user must clearly see what was written and the general rules extracted.

## Rules

1. **Never ask for confirmation** — Save directly, but always report what was saved.
2. **Never delete** existing lessons — only append.
3. **Read before write** — Always read the file first to avoid overwriting.
4. **Unique IDs** — `RECAP-YYYY-MM-DD-NNN`, NNN increments per day.
5. **Concise** — Each field 1–2 sentences, not paragraphs. General rule must be one actionable sentence.
6. **Cross-platform** — On Windows use `%USERPROFILE%` instead of `~`.
7. **Focus on general rules** — The core value of each lesson is the **General rule** field. It must be transferable and reusable across projects, not a fix specific to the current issue only.
