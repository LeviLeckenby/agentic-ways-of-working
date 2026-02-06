# Developer Agent Memory

## Project: agentic-wow
- Workspace at `A:/A-Dev/agentic-wow`
- Documentation-heavy project (methodology, agent definitions, skills)
- Primary docs file: `.docs/ways-of-working.md` (now ~834 lines after additions)
- No code to compile/test; validation is structural correctness of markdown

## Key File Locations
- `.docs/ways-of-working.md` - Full methodology (source of truth for WoW)
- `CLAUDE.md` - Workspace instructions (source of truth for agents)
- `.claude/agents/` - Subagent definitions (YAML frontmatter)
- `agents/` - Detailed agent persona docs
- `skills/` - Reusable skill definitions

## Lessons Learned
- When editing large markdown docs, read the FULL file first to understand structure
- Identify all insertion points before making any edits (order matters for line stability)
- Edit from top-to-bottom when inserting at multiple points to avoid line number drift issues
- Always update the Table of Contents when adding new sections
- Verify the final file by re-reading key transition points after all edits
