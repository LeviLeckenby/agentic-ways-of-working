# Agentic Ways of Working - Workspace Instructions

> **This is the source of truth** for all AI agents operating in this workspace.
> All other instruction files (AGENTS.md, GEMINI.md) point here.

---

## Reference Documentation

> CLAUDE.md is loaded automatically every session. The documents below are loaded **on-demand when needed**, not at session start.

- **`.docs/ways-of-working.md`** - Complete methodology, principles, and protocols
- **`.docs/agent-catalog.md`** - All available agent personas and when to use them

---

## On Session Start

**If the user's first message does not specify a clear task**, begin with these steps. If a clear task is given, acknowledge it and begin work directly.

1. **Greet the user** briefly and professionally
2. **List available projects** by scanning the `repos/` directory:
   - For each directory in `repos/`, read its `CLAUDE.md` (if it exists) to get the project name and description
   - Present the list to the user
3. **Ask the user what they want to work on:**
   - Select an existing project
   - Create a new project (use `/new-project` skill)
   - Work on the workspace itself (agents, methodology, skills)
4. **Once a project is selected:**
   - Read `repos/{project}/CLAUDE.md` for project-specific instructions
   - The project's CLAUDE.md takes precedence for project-specific conventions
   - Check `git status` in the project directory
   - Look for TODO.md, in-progress branches, or recent activity
   - Summarize the project state
5. **Ask what the user wants to accomplish this session**
6. **Create a plan and begin work** following the ways-of-working methodology

---

## Core Operating Principles

1. **Autonomous by default** - Execute routine tasks without asking. Escalate architectural decisions, risky operations, and genuine ambiguity.
2. **Context is everything** - When delegating to subagents, provide ALL necessary context. Don't assume context transfers automatically.
3. **Validate everything (NON-NEGOTIABLE)** - Every code change MUST go through the Mandatory Validation Pipeline. This is the single most important discipline.
4. **Use the right agent** - Match the task to the specialist. Use subagents for parallel work and to protect context windows.
5. **Use the right model** - Tier 1 (opus) for complex reasoning, Tier 2 (sonnet) for standard work, Tier 3 (haiku) for simple operations.
6. **Ship incrementally** - Many small, verified steps beat large, risky leaps.
7. **Be safe** - Never commit secrets, never force-push to main, never delete without confirmation, never bypass safety checks.

---

## Subagent Usage

When delegating, always provide: clear task, all relevant file paths/context, success criteria, constraints.

### Agent Selection
| Task | Subagent | Model |
|------|----------|-------|
| Research | `researcher` | haiku/sonnet |
| Code implementation | `developer` | sonnet/opus |
| Code review | `reviewer` | sonnet/opus |
| Architecture | `architect` | opus |
| Planning | `planner` | sonnet/opus |
| Writing | `writer` | sonnet/opus |
| Testing | `tester` | sonnet |
| Security | `security-auditor` | opus |
| Marketing | `marketing-strategist` | sonnet/opus |
| Product | `product-manager` | sonnet/opus |
| DevOps | `devops` | sonnet |
| Analysis | `analyst` | sonnet |
| Design | `designer` | sonnet/opus |
| Orchestration | `orchestrator` | opus |

Always look for parallel execution opportunities. Subagents cannot spawn other subagents (one level only).

---

## Mandatory Validation Pipeline (NON-NEGOTIABLE)

Every code change MUST pass through this pipeline. See `.docs/ways-of-working.md` for the full pipeline with detailed checklists.

**Summary — after every code change:**
1. **Self-Verification** - Code compiles, tests pass, linting clean, no secrets
2. **Code Review** (`reviewer` subagent) - Must output `APPROVE` or `REQUEST CHANGES`
3. **Security Review** (`security-auditor` subagent) - Must output `CLEAR` or `FINDINGS`
4. **Conditional Validators** - Tester (new features), Architect (structural changes), Accessibility (UI changes), etc.

**Resolution**: ALL Critical/High findings must be resolved. Loop until all gates pass.

**Commit messages** must include: `Validated-By: reviewer (Approved), security-auditor (Clear)`

Validation may be streamlined (NOT skipped) only for docs-only, formatting, or comment changes.

---

## Context Management

Context is the fundamental constraint. Manage it aggressively:
- `/clear` between unrelated tasks
- `/compact` when context is large but you need continuity
- Delegate research to subagents to protect main context
- For multi-phase work, externalize state to files between phases (see ways-of-working.md)
- After two failed corrections, `/clear` and write a better prompt

---

## Git & Version Control

Follow `skills/git-workflow.md` for all operations:
- Branch from main: `{type}/{description}`
- Conventional commits: `{type}({scope}): {description}`
- Never commit directly to main
- Never force-push to main
- Always use `--force-with-lease` instead of `--force`

---

## Project-Specific Overrides

When working in `repos/{project}/`, that project's `CLAUDE.md` extends (not replaces) this file. Project CLAUDE.md takes precedence for project-specific concerns; this file takes precedence for workspace-level concerns (safety, methodology, agent usage).

---

## Available Skills

Use these for common workflows:
- `/start` - Initialize a new session
- `/new-project` - Create a new project
- `/switch` - Switch to a different project
- `/plan {goal}` - Create an implementation plan
- `/review {target}` - Review code or content
- `/research {topic}` - Conduct deep research
- `/fix {bug}` - Diagnose and fix a bug
- `/test` - Run and analyze tests
- `/spec {feature}` - Create a Given/When/Then specification before implementation
- `/ship` - Prepare and ship code changes
- `/publish` - Prepare and publish content (books, video, audio, marketing)
- `/status` - Get workspace/project status
- `/retro` - Run a session retrospective
- `/review-wow` - Review the methodology itself (run regularly)

> **Note**: Skills (`.claude/skills/`) are the current standard. Legacy commands (`.claude/commands/`) are retained for backward compatibility with older Claude Code versions. Skills add YAML frontmatter for richer configuration (isolated context, tool restrictions, argument hints).

---

## Workspace Structure

```
.                               # You are here
├── CLAUDE.md                   # This file (source of truth)
├── AGENTS.md                   # Points here (for Cursor/Windsurf/etc.)
├── GEMINI.md                   # Points here (for Gemini-based tools)
├── .claude/
│   ├── settings.json           # Hooks and permissions
│   ├── skills/                 # Skill definitions (14 slash commands)
│   ├── agents/                 # Subagent definitions (14 agents)
│   └── rules/                  # Modular rules (glob-scoped)
├── .docs/
│   ├── ways-of-working.md      # Full methodology
│   ├── agent-catalog.md        # Agent persona catalog
│   └── project-templates/      # Templates (software, book, video, audio, marketing, general)
├── .evals/                     # Agent and skill evaluation test cases
├── agents/                     # Detailed agent persona documentation
├── skills/                     # Reusable skill reference documents
└── repos/                      # Project repositories (git-ignored)
```
