---
name: recap
description: Recap / Review the current conversation after repeated errors or struggles, analyze
  what both AI and the user did wrong and why, then distill lessons into
  general reusable rules and save them to the global memory file (CLAUDE.md or AGENTS.md)
---

# recap

Review the conversation, extract lessons from mistakes, and persist them as general rules in the global memory file so they are automatically loaded in every future session.

## Where to save

Append to the `## Lessons Learned` section of the **global memory file**. If the section does not exist, create it.

| Platform | macOS / Linux | Windows |
|----------|--------------|---------|
| Claude Code | `~/.claude/CLAUDE.md` | `%USERPROFILE%\.claude\CLAUDE.md` |
| Codex CLI | `~/.codex/AGENTS.md` | `%USERPROFILE%\.codex\AGENTS.md` |

## Lesson format

Only save the **general rule** — no process, no blame, no solution steps. Keep each lesson to 2 lines max.

```markdown
## Lessons Learned

- **RECAP-YYYY-MM-DD-NNN** `<tags>`: <One actionable rule sentence>
```

Example:

```markdown
## Lessons Learned

- **RECAP-2026-04-08-001** `presentation, layout`: Lock hard constraints (fullscreen? one-screen-per-page? scrollable?) before redesigning any presentation-style HTML.
- **RECAP-2026-04-08-002** `layout, hierarchy`: When user says "single column" or "don't split into two parts", also merge info hierarchy into one main content area — not just CSS grid.
- **RECAP-2026-04-08-003** `presentation, density`: To fit a presentation page in one screen, compress copy length, component count and layout scale together — not just shrink spacing/font.
```

## Workflow

1. **Scan** — Find problems that took multiple attempts to solve.
2. **Distill** — For each problem, extract one general reusable rule (not a specific fix).
3. **Read** the global memory file to avoid duplicates and determine IDs.
4. **Append** directly — do NOT ask for confirmation.
5. **Report** — Tell the user what was saved:

   *"📝 Saved N rules to `<path>`:"*
   - *`RECAP-ID` `tags`: rule*

## Rules

1. **Concise** — One sentence per rule. No process descriptions, no root cause analysis, no solution steps in the saved file. The saved content is a **checklist of rules**, not a post-mortem.
2. **General** — Rules must be transferable across projects. Do not reference specific file names, variable names, or one-time fixes.
3. **Save directly** — Never ask for confirmation. Always report what was saved.
4. **Append only** — Never delete or overwrite existing lessons.
5. **Read before write** — Always read the file first.
6. **Unique IDs** — `RECAP-YYYY-MM-DD-NNN`, NNN increments per day.
7. **Cross-platform** — On Windows use `%USERPROFILE%` instead of `~`.
