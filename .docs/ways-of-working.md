# Agentic Ways of Working (WoW) Methodology

> **Version**: 1.0.0
> **Last Updated**: 2026-02-06
> **Purpose**: Define a comprehensive, model-agnostic methodology for autonomous multi-agent workflows across diverse project types.

---

## Table of Contents

1. [Philosophy](#philosophy)
2. [Core Principles](#core-principles)
3. [Workspace Architecture](#workspace-architecture)
4. [Session Lifecycle](#session-lifecycle)
5. [Agent Orchestration Model](#agent-orchestration-model)
6. [Agent Teams (Advanced Orchestration)](#agent-teams-advanced-orchestration)
7. [Project Types & Adaptive Behavior](#project-types--adaptive-behavior)
8. [Multi-Repository Management](#multi-repository-management)
9. [Task Decomposition Framework](#task-decomposition-framework)
10. [Quality Gates & Review Patterns](#quality-gates--review-patterns)
11. [Communication Protocol](#communication-protocol)
12. [Memory & Knowledge Management](#memory--knowledge-management)
13. [Autonomy Levels](#autonomy-levels)
14. [Error Recovery & Escalation](#error-recovery--escalation)
15. [Security & Safety](#security--safety)
16. [Common Failure Modes](#common-failure-modes)

---

## Philosophy

This methodology treats AI agents as skilled collaborators within a structured workspace. The core philosophy is:

- **Autonomous by default, supervised by choice** - Agents should be able to operate independently on well-defined tasks, escalating only when genuinely blocked or when the risk/impact warrants human input.
- **Structure enables freedom** - Clear conventions, personas, and protocols free agents to focus on the work rather than figuring out how to work.
- **Composable over monolithic** - Small, focused agents that compose well beat large, do-everything agents.
- **Context is king** - The right context at the right time is more valuable than the most powerful model. Invest in context management.
- **Ship incrementally** - Prefer many small, verified steps over large, risky leaps.

---

## Core Principles

### 1. Principle of Least Authority
Each agent should only have the tools, context, and permissions it needs for its specific task. Don't give a research agent write access. Don't give a code writer deployment access.

### 2. Principle of Explicit Context
Never assume context transfers between agents automatically. Each agent invocation should include everything that agent needs to succeed. Reference specific files, line numbers, and prior decisions.

### 3. Principle of Verified Progress
Every significant action should be verified. Code should compile. Tests should pass. Research should cite sources. Creative work should be reviewed against criteria.

### 4. Principle of Graceful Degradation
If a preferred model isn't available, the system should fall back gracefully. If an agent fails, the orchestrator should recover. If context is lost, there should be persistent artifacts to reconstruct from.

### 5. Principle of Transparent Reasoning
Agents should explain their decisions, especially when making architectural choices, trade-offs, or when deviating from the initial plan. No black-box decisions.

---

## Workspace Architecture

```
agentic-wow/                    # Root workspace
├── CLAUDE.md                   # Primary instruction file (source of truth)
├── AGENTS.md                   # Model-agnostic pointer → CLAUDE.md
├── GEMINI.md                   # Model-agnostic pointer → CLAUDE.md
├── .claude/
│   └── commands/               # Slash commands for common workflows
│       ├── start.md            # /start - Session initialization
│       ├── new-project.md      # /new-project - Create new project
│       ├── switch.md           # /switch - Switch active project
│       ├── plan.md             # /plan - Create implementation plan
│       ├── review.md           # /review - Code review workflow
│       ├── research.md         # /research - Deep research task
│       ├── ship.md             # /ship - Prepare for shipping
│       ├── status.md           # /status - Workspace status report
│       └── retro.md            # /retro - Session retrospective
├── .docs/
│   ├── ways-of-working.md      # This file - full methodology
│   ├── agent-catalog.md        # Complete agent persona catalog
│   └── project-templates/      # Templates for new project types
│       ├── software.md
│       ├── book.md
│       ├── video.md
│       └── general.md
├── agents/                     # Agent persona definitions
│   ├── _base.md                # Base agent behaviors
│   ├── orchestrator.md         # Meta-orchestration agent
│   ├── architect.md            # Software architect
│   ├── developer.md            # Implementation developer
│   ├── reviewer.md             # Code reviewer
│   ├── researcher.md           # Deep research agent
│   ├── planner.md              # Project/task planner
│   ├── writer.md               # Technical/creative writer
│   ├── tester.md               # QA and testing agent
│   ├── devops.md               # DevOps/infrastructure agent
│   ├── security.md             # Security auditor
│   ├── analyst.md              # Data/business analyst
│   ├── designer.md             # UX/system designer
│   ├── marketing.md            # Marketing strategist
│   └── product.md              # Product management agent
├── skills/                     # Reusable skill definitions
│   ├── git-workflow.md         # Git operations
│   ├── code-generation.md      # Code generation patterns
│   ├── testing.md              # Testing strategies
│   ├── documentation.md        # Documentation generation
│   ├── refactoring.md          # Refactoring patterns
│   ├── research.md             # Research methodology
│   ├── content-creation.md     # Content creation workflow
│   └── deployment.md           # Deployment procedures
├── repos/                      # Project repositories (git-ignored)
│   └── .gitkeep
└── .gitignore
```

---

## Session Lifecycle

### Phase 1: Initialization
When a session begins, the orchestrating agent MUST:

1. **Greet the user** with a brief, professional welcome
2. **Ask what project/repository to work on** - present known projects from `repos/` or offer to create new
3. **Load project context** - once a project is selected:
   - Read the project's `CLAUDE.md` (or equivalent)
   - Scan for `TODO.md`, `CHANGELOG.md`, open issues
   - Check git status for any in-progress work
   - Load relevant agent personas based on project type
4. **Establish session goals** - ask the user what they want to accomplish this session
5. **Create a session plan** - decompose goals into tasks with estimated complexity

### Phase 2: Active Work
During the work phase:

1. **Task execution** follows the Task Decomposition Framework (see below)
2. **Progress updates** are provided at natural breakpoints
3. **Decisions that affect architecture or user experience** are escalated
4. **Context is preserved** through task lists, memory files, and commit messages

### Phase 3: Session Wrap-Up
Before ending a session:

1. **Summarize what was accomplished**
2. **Note any incomplete work** and create TODO items
3. **Commit all work** with clear, descriptive messages
4. **Update project memory** with key decisions and learnings
5. **Suggest next steps** for the following session

---

## Agent Orchestration Model

### Hierarchy

```
User
  └── Orchestrator (Primary Agent)
        ├── Planner Agent (decomposes work)
        ├── Research Agent (gathers information)
        ├── Architect Agent (designs solutions)
        ├── Developer Agent (implements code)
        ├── Reviewer Agent (reviews quality)
        ├── Tester Agent (validates correctness)
        ├── Writer Agent (creates content/docs)
        ├── DevOps Agent (handles infrastructure)
        ├── Security Agent (audits safety)
        ├── Analyst Agent (analyzes data/metrics)
        ├── Designer Agent (UX/system design)
        ├── Marketing Agent (marketing strategy)
        └── Product Agent (product decisions)
```

### Orchestration Patterns

#### 1. Sequential Pipeline
For well-understood, linear workflows:
```
Plan → Research → Architect → Develop → Test → Review → Ship
```

#### 2. Parallel Fan-Out
For independent subtasks that can run concurrently:
```
Orchestrator → [Agent A, Agent B, Agent C] → Synthesize
```

#### 3. Iterative Refinement
For tasks requiring multiple passes:
```
Draft → Review → Revise → Review → Approve
```

#### 4. Event-Driven
For reactive workflows:
```
Monitor → Detect → Triage → Respond → Verify
```

### Agent Selection Criteria

| Factor | Choose Specialized Agent | Use General Agent |
|--------|-------------------------|-------------------|
| Task complexity | High | Low |
| Domain expertise needed | Deep | Shallow |
| Output quality bar | Critical | Flexible |
| Parallel execution | Yes | N/A |
| Context window pressure | High | Low |

### Model Selection Guidelines

| Task Type | Recommended Tier | Rationale |
|-----------|-----------------|-----------|
| Architecture decisions | Highest available (opus) | Requires deep reasoning |
| Complex code generation | Highest available (opus) | Quality-critical |
| Code review | High (sonnet/opus) | Needs nuanced judgment |
| Research synthesis | High (sonnet/opus) | Needs comprehension |
| Simple code changes | Medium (sonnet) | Well-defined, lower stakes |
| File operations | Low (haiku) | Mechanical, low complexity |
| Status checks | Low (haiku) | Simple data gathering |
| Formatting/linting | Low (haiku) | Rule-based |

---

## Agent Teams (Advanced Orchestration)

> **Status**: Experimental feature. Use for complex, multi-perspective work.

Agent Teams are a coordination model distinct from subagents. While subagents report back to the orchestrator and stop, Agent Team members communicate with each other, challenge findings, and self-coordinate.

### Subagents vs. Agent Teams

| Aspect | Subagents | Agent Teams |
|--------|-----------|-------------|
| Context | Own window; results return to caller | Own window; fully independent |
| Communication | Report back to main agent only | Teammates message each other directly |
| Coordination | Main agent manages | Shared task list, self-coordination |
| Best for | Focused tasks, result-only | Complex work requiring discussion |
| Token cost | Lower (~20K overhead each) | Higher (~5x subagent cost) |
| Session | Part of main session | Independent sessions |

### When to Use Agent Teams

- **Research & Review**: Parallel investigation of different aspects, teammates challenge each other's findings
- **New Module Development**: Each teammate owns a separate piece, coordinates on interfaces
- **Debugging**: Competing hypotheses explored in parallel
- **Cross-Layer Coordination**: Frontend + backend + database changes that need to coordinate
- **Architecture Design**: Multiple perspectives (security, performance, maintainability) on a design

### When NOT to Use Agent Teams

- Simple tasks a single agent can handle
- Tasks where the orchestrator can manage subagents effectively
- When token cost is a concern
- For sequential, dependent work (use pipeline instead)

### Team Patterns

1. **Leader Pattern**: Team lead coordinates, delegates, synthesizes. Best for structured work.
2. **Swarm Pattern**: All teammates are peers, self-assign from shared task list. Best for exploration.
3. **Pipeline Pattern**: Each teammate handles a stage, passes to the next. Best for transformation chains.
4. **Watchdog Pattern**: One teammate monitors others' output for quality/security. Best for critical work.

---

## Project Types & Adaptive Behavior

The methodology adapts based on project type. Each project's CLAUDE.md should declare its type.

### Software Projects
- **Primary agents**: Architect, Developer, Tester, Reviewer, DevOps
- **Workflow**: Plan → Branch → Implement → Test → Review → Merge
- **Quality gates**: Tests pass, linting clean, review approved
- **Artifacts**: Code, tests, documentation, changelogs

### Book / Written Content Projects
- **Primary agents**: Planner, Writer, Researcher, Reviewer (as Editor)
- **Workflow**: Outline → Research → Draft → Edit → Revise → Polish
- **Quality gates**: Consistency check, fact-check, style review
- **Artifacts**: Manuscripts, outlines, research notes, style guides

### Video Production Projects
- **Primary agents**: Planner, Writer (Script), Researcher, Designer
- **Workflow**: Concept → Script → Storyboard → Asset List → Production Notes
- **Quality gates**: Script review, brand alignment, technical feasibility
- **Artifacts**: Scripts, shot lists, storyboards, asset manifests

### Audio / Podcast Projects
- **Primary agents**: Planner, Writer (Script), Researcher, Analyst
- **Workflow**: Topic Research → Outline → Script → Show Notes → Distribution Plan
- **Quality gates**: Content accuracy, flow review, SEO optimization
- **Artifacts**: Scripts, show notes, transcripts, distribution checklists

### Marketing / Campaign Projects
- **Primary agents**: Marketing, Writer, Analyst, Designer, Researcher
- **Workflow**: Research → Strategy → Content Plan → Create → Review → Publish
- **Quality gates**: Brand alignment, audience fit, compliance check
- **Artifacts**: Strategies, content calendars, copy, analytics plans

### General / Mixed Projects
- **Primary agents**: Determined dynamically based on tasks
- **Workflow**: Adaptive based on task decomposition
- **Quality gates**: Defined per-task
- **Artifacts**: Varies

---

## Multi-Repository Management

### Repository Registration
When a new repository is added to the workspace:

1. Clone or create in `repos/` directory
2. The repo maintains its own `.git` (it's git-ignored from the workspace)
3. Create or verify a `CLAUDE.md` in the repo root with:
   - Project type declaration
   - Tech stack description
   - Coding conventions
   - Key architectural decisions
   - Active goals / roadmap items

### Cross-Repository Work
When work spans multiple repositories:

1. **Identify all affected repos** before starting
2. **Plan changes holistically** - design the interface/contract first
3. **Implement in dependency order** - start with the most-depended-on repo
4. **Test integration points** between repos
5. **Commit and push atomically** where possible (or document the required order)

### Repository Context Loading
When switching to a project:
```
1. Read repos/{project}/CLAUDE.md
2. Check repos/{project}/.claude/ for project-specific commands
3. Load repos/{project}/TODO.md or equivalent task tracking
4. Run git status to understand current state
5. Check for any .env.example or setup requirements
```

---

## Task Decomposition Framework

### Level 1: Epic (Session Goal)
- User's stated objective for the session
- May span multiple repos and agent types
- Example: "Add user authentication to the app"

### Level 2: Story (Coherent Unit of Work)
- A self-contained piece of work that delivers visible value
- Should be completable in one focused work block
- Example: "Implement JWT token generation and validation"

### Level 3: Task (Atomic Action)
- A single, well-defined action an agent can take
- Has clear inputs, outputs, and success criteria
- Example: "Create the TokenService class with generate() and validate() methods"

### Decomposition Rules

1. **No task should take more than ~15 minutes of agent work** - if it would, break it down further
2. **Every task should have verifiable success criteria** - how do we know it's done?
3. **Dependencies must be explicit** - which tasks block which?
4. **Parallel opportunities should be identified** - what can run concurrently?
5. **Risk should front-load** - do the uncertain/risky tasks first

### Specification Phase (for Non-Trivial Features)

Before implementation of any non-trivial feature, create a specification:

1. **Define the behavior** using Given/When/Then scenarios:
   ```
   Given: {precondition / initial state}
   When: {action / trigger}
   Then: {expected outcome / postcondition}
   ```

2. **Document constraints** - performance requirements, compatibility, security requirements
3. **Define edge cases** - what happens at boundaries, with empty input, with invalid input
4. **Set acceptance criteria** - measurable conditions that prove the feature works

The specification becomes the source of truth. The Reviewer validates against it. Tests are derived from it. This prevents spec drift — the gap between what was asked and what was built.

**When to skip specs**: Trivial changes where "you could describe the diff in one sentence." Bug fixes with clear reproduction steps. Configuration changes.

### Task Template
```
Task: [Clear, imperative description]
Agent: [Which agent persona handles this]
Inputs: [What context/files/data this task needs]
Outputs: [What artifacts this task produces]
Success Criteria: [How to verify completion]
Dependencies: [What must complete first]
Estimated Complexity: [Low / Medium / High]
```

---

## Mandatory Validation Pipeline (MVP)

> **This pipeline is NON-NEGOTIABLE.** Every code change passes through it. No exceptions unless the user explicitly requests a skip (which must be noted). This is what separates high-quality autonomous work from unreliable output.

### The Pipeline

After any agent completes a code change, the orchestrator MUST execute this pipeline before the work is considered "done":

```
Developer completes code
        │
        ▼
┌─────────────────────────────────────────┐
│  GATE 1: Self-Verification (Developer)  │
│  • Code compiles/runs without errors    │
│  • All existing tests still pass        │
│  • New tests written for new behavior   │
│  • Linting/formatting passes            │
│  • No secrets in changed files          │
└─────────────────┬───────────────────────┘
                  │ (if passes)
                  ▼
┌─────────────────────────────────────────────────────────┐
│  GATE 2: Parallel Validation Subagents (ALL MANDATORY)  │
│                                                         │
│  ┌──────────────────┐  ┌─────────────────────────────┐  │
│  │  Code Review      │  │  Security Review             │  │
│  │  (reviewer agent) │  │  (security-auditor agent)    │  │
│  │                   │  │                              │  │
│  │  Checks:          │  │  Checks:                     │  │
│  │  • Correctness    │  │  • OWASP Top 10              │  │
│  │  • Conventions    │  │  • Secret exposure            │  │
│  │  • Complexity     │  │  • Input validation           │  │
│  │  • Edge cases     │  │  • Auth/authz correctness     │  │
│  │  • Requirements   │  │  • Dependency vulnerabilities │  │
│  │    alignment      │  │  • Injection vectors          │  │
│  │                   │  │                              │  │
│  │  Output:          │  │  Output:                     │  │
│  │  APPROVE or       │  │  CLEAR or                    │  │
│  │  REQUEST CHANGES  │  │  FINDINGS (with severity)    │  │
│  └──────────────────┘  └─────────────────────────────┘  │
└─────────────────┬───────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  GATE 3: Conditional Validators         │
│  (invoked based on change type)         │
│                                         │
│  IF new feature:                        │
│    → Tester: test adequacy review       │
│  IF architecture change:                │
│    → Architect: alignment validation    │
│  IF public API change:                  │
│    → Breaking change detection          │
│  IF new dependencies:                   │
│    → Dependency audit (CVEs, licenses)  │
│  IF UI change:                          │
│    → Accessibility check (WCAG)         │
│  IF hot path / data processing:         │
│    → Performance review                 │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  RESOLUTION                             │
│                                         │
│  ALL "Request Changes" / "Findings"     │
│  (Critical/High) MUST be resolved       │
│  before work is marked complete.        │
│                                         │
│  Medium/Low findings: may be tracked    │
│  as follow-up TODOs with user consent.  │
│                                         │
│  After fixes: re-run failed gates.      │
│  Loop until all gates pass.             │
└─────────────────┬───────────────────────┘
                  │
                  ▼
         ✅ WORK COMPLETE
    (may now proceed to /ship)
```

### Gate 2 Detail: Code Review (ALWAYS MANDATORY)

The `reviewer` subagent MUST be invoked after every code change. The reviewer receives:
- All changed files (diff or full content)
- The original user requirement / task description
- The project's coding conventions

The reviewer MUST check and explicitly confirm:

**Correctness & Logic**
- [ ] Code does what the requirement asks (requirements alignment)
- [ ] Edge cases at boundaries are handled
- [ ] Error handling is appropriate (not excessive, not absent)
- [ ] State management is correct (no race conditions, stale data)

**Quality & Maintainability**
- [ ] Code is readable and follows project conventions
- [ ] No unnecessary complexity or over-engineering
- [ ] No dead code, unused imports, or leftover debug statements
- [ ] Functions/methods have single responsibility
- [ ] Naming is clear and consistent

**Testing**
- [ ] Tests cover the happy path
- [ ] Tests cover critical failure modes
- [ ] Tests are meaningful (not just asserting true === true)
- [ ] Existing tests were not weakened or deleted without justification

**Documentation**
- [ ] Public API changes are reflected in documentation
- [ ] No TODO/FIXME left without an associated issue

**Output**: `APPROVE` or `REQUEST CHANGES` with specific, actionable items.

### Gate 2 Detail: Security Review (ALWAYS MANDATORY)

The `security-auditor` subagent MUST be invoked after every code change. For non-sensitive code, a quick scan is sufficient. For sensitive code (auth, input, API, data, deps), a thorough review.

The security auditor MUST check:

**Input & Output**
- [ ] All external input is validated and sanitized
- [ ] No SQL/NoSQL/OS command injection vectors
- [ ] No XSS vectors (reflected, stored, DOM-based)
- [ ] Output encoding is appropriate

**Authentication & Authorization**
- [ ] Auth checks are present where required
- [ ] Authorization is enforced (not just authenticated ≠ authorized)
- [ ] Session management is secure
- [ ] No credential exposure in logs, errors, or responses

**Data Protection**
- [ ] Sensitive data is encrypted at rest and in transit
- [ ] No secrets hardcoded (API keys, passwords, tokens)
- [ ] PII handling follows data protection principles
- [ ] `.gitignore` covers all sensitive files

**Dependencies**
- [ ] No known CVEs in new/updated dependencies
- [ ] Dependencies are from trusted sources
- [ ] License compatibility is verified

**Output**: `CLEAR` or `FINDINGS` with severity (Critical/High/Medium/Low) and remediation.

### Gate 3 Detail: Conditional Validators

These run based on what type of change was made:

| Change Type | Validator | What It Checks |
|------------|-----------|----------------|
| New feature | Tester | Test coverage adequacy, missing scenarios |
| Architecture change | Architect | Alignment with system design, boundary integrity |
| Public API change | Reviewer (extended) | Backward compatibility, contract changes, consumer impact |
| New dependencies | Analyst | CVE database, license compatibility, necessity |
| UI change | Designer | WCAG accessibility, responsive behavior, UX consistency |
| Performance-sensitive | Analyst | Query efficiency, algorithmic complexity, resource usage |
| Database changes | Architect | Migration safety, backward compatibility, index impact |

### Validation Streamlining

For **trivial changes** (docs-only, comments, formatting), the pipeline is streamlined:
- Gate 1 (self-verification): Still required
- Gate 2 (review + security): Quick scan only, not full review
- Gate 3 (conditional): Skipped

The orchestrator determines change severity. When in doubt, run the full pipeline.

### Validation Status Tracking

Every completed piece of work must record its validation status:
```
Validated-By: reviewer (Approved), security-auditor (Clear)
Tests: All passing (X tests, Y new)
Conditional: [tester: adequate | architect: aligned | n/a]
```

This status goes into the commit message and any task tracking.

### Review Checklist (Content Projects)

For non-code projects (books, marketing, video scripts), a parallel review discipline applies:

- [ ] Accurate and well-researched (fact-check pass)
- [ ] Consistent voice and tone (style guide compliance)
- [ ] Proper structure and flow
- [ ] No factual errors or unsupported claims
- [ ] Target audience appropriate
- [ ] SEO considerations addressed (if applicable)
- [ ] Brand voice alignment (if applicable)

---

## Communication Protocol

### Agent-to-User Communication
- **Be concise** - lead with the most important information
- **Be actionable** - when presenting options, make clear recommendations
- **Be honest** - if uncertain, say so. If something failed, explain why
- **Avoid jargon** unless the user has demonstrated familiarity
- **Progress updates** at natural breakpoints, not after every micro-step

### Agent-to-Agent Communication (via Orchestrator)
When delegating to subagents:

1. **Context**: Provide all necessary background in the prompt
2. **Objective**: State exactly what the agent should accomplish
3. **Constraints**: List any restrictions, conventions, or boundaries
4. **Output format**: Specify how results should be structured
5. **Success criteria**: Define what "done" looks like

### Escalation Triggers
Escalate to the user when:
- A task is ambiguous and could go multiple valid directions
- An architectural decision with long-term consequences needs to be made
- A security concern is discovered
- Work would take significantly longer than expected
- A conflict between project requirements is detected
- The agent lacks sufficient context to proceed confidently

---

## Memory & Knowledge Management

### Workspace Memory (`.claude/` in workspace root)
- Persistent across sessions
- Stores workspace-level patterns, preferences, and learnings
- Updated by the orchestrator after each significant session

### Project Memory (`repos/{project}/.claude/`)
- Specific to each project
- Contains project-specific conventions, decisions, and context
- Updated during project work

### Session Memory (Task Lists)
- Ephemeral within a session
- Tracks current progress, decisions, and blockers
- Converted to persistent artifacts during session wrap-up

### Knowledge Artifacts
- **Decision Records**: Why was X chosen over Y?
- **Pattern Library**: Reusable solutions discovered during work
- **Mistake Log**: What went wrong and how to avoid it
- **Convention Registry**: Project-specific coding/writing conventions

### Context Externalization Pattern

For complex, multi-phase work, externalize state to files between phases rather than fighting the context window:

```
Phase 1: Plan    → save plan.md         → /clear
Phase 2: Implement → save progress.json → /clear
Phase 3: Test    → save test-results.md → /clear
Phase 4: Review  → save review.md       → /clear
Phase 5: Ship    → commit and push
```

Each phase starts with clean context loaded from the artifacts of previous phases.

**Key practices:**
- Use JSON over Markdown for agent-maintained state files (more resilient to corruption)
- Git commits serve as a natural progress log between phases
- The initializer + coding agent pattern: one agent sets up the environment, subsequent sessions pick up from persistent artifacts
- MEMORY.md files persist across sessions (first 200 lines loaded into system prompt)

### Context Budgeting

Treat the context window as a budget:
- ~50 instructions from system prompt (Claude Code built-in)
- CLAUDE.md content (target: under 200 lines)
- Skills descriptions (loaded at session start, ~15K char budget)
- Conversation history (managed by auto-compaction at 95%)
- Tool outputs (can be verbose — use subagents to contain)

**Priority for dropping content when context fills:**
1. Old tool outputs (lowest value)
2. Completed task details (already committed)
3. Research that has been synthesized
4. Never drop: current task context, user requirements, safety rules

---

## Autonomy Levels

The user can set the autonomy level for each session or project:

### Level 1: Supervised
- Agent proposes every action before executing
- Human approves each step
- Best for: Learning, sensitive operations, new projects

### Level 2: Guided (Default)
- Agent executes routine operations autonomously
- Pauses for architectural decisions, risky operations
- Best for: Active development with human oversight

### Level 3: Autonomous
- Agent executes all operations independently
- Only pauses for explicit ambiguity or blockers
- Reports results at the end
- Best for: Well-defined tasks, trusted projects, batch operations

### Level 4: Full Auto
- Agent executes, commits, and pushes autonomously
- Handles all decisions within established conventions
- Only contacts human for critical blockers
- Best for: CI/CD-like workflows, maintenance tasks

---

## Error Recovery & Escalation

### Recovery Strategies

1. **Retry with adjustment** - If an approach fails, try a modified version
2. **Alternative approach** - Switch to a fundamentally different strategy
3. **Scope reduction** - Accomplish a smaller version of the goal
4. **Context enrichment** - Gather more information before retrying
5. **Human escalation** - Ask the user for guidance

### Recovery Priority Order
```
1. Can I fix this automatically? → Fix it
2. Can I work around it? → Document the workaround
3. Can I reduce scope to still deliver value? → Do so
4. Do I need more context? → Research or ask
5. Am I truly blocked? → Escalate with full context
```

### Escalation Template
When escalating to the user, always provide:
- **What** you were trying to do
- **What** went wrong (with specific error details)
- **What** you've already tried
- **Options** for how to proceed (with your recommendation)

---

## Security & Safety

### Non-Negotiable Rules
1. **Never commit secrets** - API keys, tokens, passwords, certificates
2. **Never force-push to main** - Always use branches
3. **Never delete without confirmation** - Branches, files, data
4. **Never bypass safety checks** - No `--no-verify`, no skipping tests
5. **Never run destructive commands** - No `rm -rf`, `DROP TABLE`, etc. without explicit user approval
6. **Never expose internal paths** - Sanitize system paths in outputs
7. **Never execute untrusted code** - Validate external scripts before running

### Data Handling
- Treat all `.env` files as sensitive
- Never log or display credentials, even partially
- Use environment variables for configuration, not hardcoded values
- Respect `.gitignore` patterns

### Branch Protection
- All work on feature branches, never directly on main/master
- Branch naming convention: `{type}/{description}` (e.g., `feat/add-auth`, `fix/login-bug`)
- Commits should be atomic and well-described
- PRs should have clear descriptions and test plans

---

## Common Failure Modes

Understanding and preventing these failure modes is as important as following the positive practices above.

### 1. Over-Building (One-Shotting)
**Symptom**: Agent tries to implement too much at once, runs out of context mid-implementation, leaves features half-built.
**Prevention**: Implement one feature per work block. Verify before moving to the next. Use incremental commits.

### 2. Context Pollution
**Symptom**: Mixing unrelated tasks in one session, or accumulating failed approaches through repeated corrections.
**Prevention**: Use `/clear` between unrelated tasks. After two failed correction attempts, start fresh with a better prompt.

### 3. Test Evasion
**Symptom**: Agent disables tests, adds placeholder TODOs, weakens assertions, or claims success without running verification.
**Prevention**: Use hooks to enforce test execution after every edit. Use a separate agent for code review (fresh context catches what biased context misses).

### 4. Hallucination & Spec Drift
**Symptom**: Agent generates plausible-looking code that doesn't actually meet the requirements. Dangerous because it "looks right."
**Prevention**: Always verify against the original specification. Require explicit requirements-alignment confirmation in every review.

### 5. Correction Spiral
**Symptom**: Repeated failed fixes pollute context with noise, making each subsequent attempt worse.
**Prevention**: After two failed corrections, `/clear` context and write a focused prompt that includes the specific error and the correct approach.

### 6. Infinite Exploration
**Symptom**: Agent reads hundreds of files trying to understand the codebase, filling context without producing output.
**Prevention**: Scope investigations narrowly. Delegate exploration to subagents. Set explicit boundaries ("look at files X, Y, Z only").

### 7. Over-Specified Instructions
**Symptom**: CLAUDE.md or agent prompts are so long that the agent ignores important rules buried in the noise.
**Prevention**: Keep CLAUDE.md under 200 lines. Use Skills for domain-specific knowledge (loaded on-demand). Use Hooks for deterministic enforcement. For each instruction, ask: "Would removing this cause a mistake?"

### 8. Set and Forget
**Symptom**: Agent configurations and CLAUDE.md files are never updated based on observed behavior, leading to persistent failure patterns.
**Prevention**: Treat CLAUDE.md and agent configurations as living documents. Run `/retro` after sessions. Update configs when you observe repeated mistakes.

---

## Appendix: Quick Reference

### Starting a Session
```
1. "What project would you like to work on?"
2. Load project context
3. "What would you like to accomplish today?"
4. Decompose into tasks
5. Begin execution
```

### Agent Invocation Template
```
Agent: {persona}
Model: {recommended tier}
Task: {clear description}
Context: {relevant files, decisions, constraints}
Output: {expected deliverable}
```

### Commit Message Convention
```
{type}({scope}): {description}

{body - what and why}

Co-Authored-By: {agent} <noreply@ai-agent.dev>
```

Types: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `style`, `perf`, `ci`
