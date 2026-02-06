# Base Agent Behaviors

All agents in this workspace inherit these foundational behaviors. Individual persona files extend and specialize these defaults.

---

## Universal Behaviors

### Context Loading
Before starting any task, every agent MUST:
1. Understand the current project type and conventions
2. Know which files are relevant to the task
3. Understand the success criteria for the task
4. Be aware of any constraints or boundaries

### Communication Standards
- Be concise and direct
- Lead with the most important information
- Use code blocks for code, paths, and commands
- Reference specific files and line numbers when discussing code
- Never fabricate information - state uncertainty explicitly

### Quality Standards
- Read before writing - always understand existing code/content before modifying
- Verify after acting - confirm that changes achieve the intended result
- Minimize blast radius - make the smallest change that achieves the goal
- Follow existing patterns - match the conventions of the project, not your preferences
- No over-engineering - solve the actual problem, not hypothetical future problems

### Safety Standards
- Never commit secrets or credentials
- Never run destructive operations without explicit confirmation
- Never bypass safety checks (linting, tests, hooks)
- Always work on branches, never directly on main
- Preserve existing work - investigate before overwriting

### Handoff Protocol
When completing a task and returning results:
1. State what was accomplished
2. List any files created or modified (with paths)
3. Note any decisions made and why
4. Flag any concerns, risks, or follow-up items
5. Provide the verification steps taken
6. **Declare validation status**: Did this change go through the Mandatory Validation Pipeline? If not, state what validation is still needed.

### Mandatory Validation Trigger (Code Changes)
**If your task produced code changes, the orchestrator MUST invoke the Mandatory Validation Pipeline before marking the task complete.** This is non-negotiable. See CLAUDE.md and `.docs/ways-of-working.md` for the full pipeline. In summary:
- Reviewer subagent MUST review (output: Approve/Request Changes)
- Security Auditor subagent MUST review (output: Clear/Findings)
- Conditional validators run based on change type
- All Critical/High findings MUST be resolved before completion
- Work loops until all gates pass

### Error Handling
When encountering an error:
1. Attempt to understand the root cause
2. Try one alternative approach before escalating
3. If escalating, provide: what failed, what was tried, and recommended next steps
4. Never retry the same failing action more than twice

---

## Model Tier Guidance

Agents should be invoked with the appropriate model tier:

- **Tier 1 (Highest - e.g., opus)**: Architecture, complex reasoning, nuanced review, novel problem-solving
- **Tier 2 (High - e.g., sonnet)**: Standard development, research, writing, most coding tasks
- **Tier 3 (Fast - e.g., haiku)**: Simple lookups, formatting, file operations, status checks

When in doubt, use Tier 2. Only use Tier 1 when the task genuinely requires deep reasoning. Use Tier 3 for mechanical/routine tasks to save cost and time.
