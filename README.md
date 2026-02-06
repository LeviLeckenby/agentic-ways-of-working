# Agentic Ways of Working

> A comprehensive, model-agnostic methodology for autonomous multi-agent AI workflows. Works with Claude Code, Cursor, Windsurf, Gemini, and any AI coding tool.

---

## What This Is

**Agentic Ways of Working** is a production-ready framework for building sophisticated AI agent systems that can work autonomously across software, creative, and business projects. It provides:

- **Structured agent orchestration** with 14 specialized personas
- **Mandatory validation pipeline** ensuring every code change is reviewed and security-checked
- **Model-agnostic design** that works with any AI tool (Claude, Gemini, Cursor, etc.)
- **Multi-project workspace** with git-based project isolation
- **Comprehensive skills library** for common workflows
- **Deterministic enforcement** via hooks and path-scoped rules

This isn't just documentation. It's a working system with enforced quality gates, persistent agent memory, and battle-tested patterns for complex multi-agent workflows.

---

## What's Included

### Core Infrastructure
- **CLAUDE.md** (156 lines) - Source of truth for all agents
- **14 subagent definitions** with YAML frontmatter for Claude Code
- **15 detailed agent personas** (orchestrator, architect, developer, reviewer, researcher, planner, writer, tester, devops, security, analyst, designer, marketing, product, and base)
- **8 reusable skill reference docs** (git-workflow, code-generation, testing, documentation, refactoring, research, content-creation, deployment)

### Advanced Features
- **14 skills** with full implementations (start, new-project, switch, plan, spec, review, research, fix, test, ship, publish, status, retro, review-wow)
- **7 modular rules** with glob-based path scoping (safety, validation, git-conventions, code-quality, testing, content-quality, context-management)
- **Validation hooks** for deterministic enforcement (pre-tool destructive command blocker, post-response code validation gate)
- **Agent Teams** support for advanced parallel orchestration
- **Persistent agent memory** scoped to projects
- **Evaluation suite** (`.evals/`) for agent and skill quality verification

### Project Support
- **6 project templates** (software, book, video, audio, marketing, general)
- **Multi-repository management** (each project is a separate git repo)
- **Model tier selection** (Tier 1/opus for complex, Tier 2/sonnet for standard, Tier 3/haiku for simple)

### Quality & Safety
- **Mandatory Validation Pipeline** - Every code change passes through code review and security audit gates before completion
- **Security-first git workflow** - Blocks force-push to main, destructive commands without confirmation
- **Context management** - Explicit patterns for managing the fundamental constraint of agent work

---

## Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/LeviLeckenby/agentic-ways-of-working.git
cd agentic-ways-of-working
```

### 2. Open with Your AI Tool
- **Claude Code**: Open the directory. Claude reads `CLAUDE.md` automatically.
- **Cursor/Windsurf**: Open the directory. The AI reads `AGENTS.md`, which points to `CLAUDE.md`.
- **Gemini-based tools**: Open the directory. The AI reads `GEMINI.md`, which points to `CLAUDE.md`.

### 3. Initialize a Session
In your AI tool's chat interface, type the `/start` slash command to begin:
```
/start
```

The agent will:
- Greet you
- List available projects in `repos/`
- Ask what you want to work on
- Initialize the session with context

### 4. Create a New Project
Use the `/new-project` skill:
```
/new-project
```

The agent will:
- Ask for project type (software, book, video, audio, marketing, general)
- Ask for project name and description
- Create the project structure in `repos/{project-name}/`
- Initialize a git repository
- Set up the project's `CLAUDE.md` from the appropriate template

### 5. Start Working
The agent follows the methodology automatically:
- **Plan** tasks with `/plan {goal}`
- **Research** topics with `/research {topic}`
- **Review** code with `/review {target}`
- **Ship** changes with `/ship`
- **Check status** with `/status`
- **Run retrospectives** with `/retro`

---

## Workspace Structure

```
agentic-ways-of-working/
├── CLAUDE.md                   # Source of truth (156 lines)
├── AGENTS.md                   # Model-agnostic pointer → CLAUDE.md
├── GEMINI.md                   # Model-agnostic pointer → CLAUDE.md
├── README.md                   # This file
├── .claude/
│   ├── settings.json           # Hooks, permissions, agent teams config
│   ├── commands/               # Legacy slash commands (9 commands)
│   ├── skills/                 # Modern skill definitions (14 skills)
│   ├── agents/                 # Subagent definitions (14 agents, YAML frontmatter)
│   └── rules/                  # Modular rules (7 rules, glob-scoped)
├── .docs/
│   ├── ways-of-working.md      # Full methodology (~834 lines)
│   ├── agent-catalog.md        # Agent persona catalog
│   └── project-templates/      # Templates (6 types)
├── .evals/                     # Agent and skill evaluation test cases
├── agents/                     # Detailed agent persona docs (15 files)
├── skills/                     # Reusable skill reference (8 files)
└── repos/                      # Your projects (git-ignored, each has own repo)
```

---

## Available Skills

| Skill | Description |
|-------|-------------|
| `/start` | Initialize a new session, list projects, set context |
| `/new-project` | Create a new project with template-based scaffolding |
| `/switch` | Switch to a different project |
| `/plan {goal}` | Create a decomposed implementation plan |
| `/spec {feature}` | Create a Given/When/Then specification before implementation |
| `/review {target}` | Review code or content against quality criteria |
| `/research {topic}` | Conduct deep research with source citation |
| `/fix {bug}` | Diagnose and fix a bug with root cause analysis |
| `/test` | Run tests, analyze failures, write new tests |
| `/ship` | Prepare code changes for shipping (tests, validation, commit, PR) |
| `/publish` | Prepare content for publishing (editorial review, fact-check, quality gates) |
| `/status` | Get workspace/project status report |
| `/retro` | Run a session retrospective and capture learnings |
| `/review-wow` | Review the methodology itself for gaps and improvements |

Skills are implemented as subdirectories in `.claude/skills/`, each with a `SKILL.md` file.

---

## Key Concepts

### Agent Personas
Specialized roles with focused responsibilities:
- **Orchestrator** - Coordinates multi-agent workflows
- **Architect** - System design and architectural decisions
- **Developer** - Code implementation
- **Reviewer** - Code and content review
- **Researcher** - Deep research and analysis
- **Planner** - Task decomposition and planning
- **Writer** - Technical and creative writing
- **Tester** - QA and testing
- **DevOps** - Infrastructure and CI/CD
- **Security Auditor** - Security review and threat analysis
- **Analyst** - Data and business analysis
- **Designer** - UX and system design
- **Marketing Strategist** - Marketing strategy and content
- **Product Manager** - Product management and roadmapping

### Mandatory Validation Pipeline

**NON-NEGOTIABLE**: Every code change must pass through this pipeline before being considered complete.

1. **Self-Verification** - Code compiles, tests pass, linting clean, no secrets
2. **Code Review** (`reviewer` subagent) - Must output `APPROVE` or `REQUEST CHANGES`
3. **Security Review** (`security-auditor` subagent) - Must output `CLEAR` or `FINDINGS`
4. **Conditional Validators** - Tester (new features), Architect (structural changes), etc.

Resolution loop: ALL Critical/High findings must be resolved. If `REQUEST CHANGES` or `FINDINGS`, fix and re-submit.

Commit messages include: `Validated-By: reviewer (Approved), security-auditor (Clear)`

### Skills vs Commands vs Rules

- **Skills** (`.claude/skills/`) - Multi-step workflows with full implementations (modern approach)
- **Commands** (`.claude/commands/`) - Simpler single-file slash commands (legacy, still supported)
- **Rules** (`.claude/rules/`) - Path-scoped enforcement rules applied automatically

### Agent Teams vs Subagents

- **Subagents** - Single-level delegation for focused tasks (e.g., delegate code review to `reviewer`)
- **Agent Teams** - Advanced orchestration with parallel coordination (enabled via `settings.json`)

### Context Management

Context is the fundamental constraint. The methodology includes:
- `/clear` between unrelated tasks to reset context
- `/compact` when context is large but continuity is needed
- Delegation to subagents to protect main context
- Externalizing state to files between phases
- After two failed corrections: `/clear` and write a better prompt

---

## Project Types

The methodology supports 6 project types with specialized templates:

1. **Software** - Full-stack development with testing, CI/CD, deployment
2. **Book** - Long-form writing with chapters, editing, publishing
3. **Video** - Video production with scripting, editing, rendering
4. **Audio** - Audio production with recording, editing, mastering
5. **Marketing** - Marketing campaigns with strategy, content, analytics
6. **General** - Flexible template for any other project type

Each template provides project-specific agent guidance, workflow patterns, and quality criteria.

---

## Model Agnostic

This methodology is designed to work with any AI model and any AI coding tool:

- **CLAUDE.md** is the source of truth
- **AGENTS.md** points to CLAUDE.md (for Cursor, Windsurf, etc.)
- **GEMINI.md** points to CLAUDE.md (for Gemini-based tools)

Model tier guidance:
- **Tier 1** (Claude Opus, Gemini Pro) - Complex reasoning, architecture, security
- **Tier 2** (Claude Sonnet, Gemini Flash) - Standard implementation, review
- **Tier 3** (Claude Haiku) - Simple tasks, research, formatting

---

## Contributing

Contributions are welcome. This is an open methodology designed to evolve.

### How to Contribute
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Make your changes
4. Run the validation pipeline (if code changes)
5. Commit with conventional commits (`feat:`, `fix:`, `docs:`, etc.)
6. Push and create a pull request

### What to Contribute
- New agent personas
- New skills or commands
- New project templates
- Improvements to existing patterns
- Bug fixes
- Documentation improvements

### Guidelines
- Follow the existing file structure and naming conventions
- Document new agents in both `.claude/agents/` (YAML frontmatter) and `agents/` (detailed docs)
- Skills should be in `.claude/skills/{skill-name}/SKILL.md` format
- Update `.docs/ways-of-working.md` if adding new concepts
- Keep CLAUDE.md concise (under 200 lines if possible)

---

## License

MIT License - see LICENSE file for details.

---

## Resources

- **Repository**: https://github.com/LeviLeckenby/agentic-ways-of-working
- **Full Methodology**: `.docs/ways-of-working.md`
- **Agent Catalog**: `.docs/agent-catalog.md`
- **Issues**: https://github.com/LeviLeckenby/agentic-ways-of-working/issues

---

**Built with Claude Code and the Agentic Ways of Working methodology.**
