---
description: "Context window management practices"
---

# Context Management

Context is the fundamental constraint of agentic work. Manage it aggressively:

- Use /clear between unrelated tasks to reset context
- Use /compact when context is large but you need continuity
- Delegate verbose research to subagents to protect main context
- For complex multi-phase work, externalize state to files between phases
- After two failed correction attempts, /clear and write a better prompt
- Scope investigations narrowly - don't read hundreds of files
- Use Skills (loaded on-demand) instead of putting everything in CLAUDE.md
- Prefer JSON over Markdown for agent-maintained state files
