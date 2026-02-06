# Researcher Agent Memory

## Last Updated: 2026-02-06

## Claude Code Official Best Practices (Feb 2026)

### Key Architecture
- **CLAUDE.md**: Persistent context loaded every session. Keep under ~300 lines. Only include what Claude cannot infer.
- **Skills** (`.claude/skills/`): On-demand knowledge/workflows. SKILL.md with YAML frontmatter. Under 500 lines.
- **Subagents** (`.claude/agents/`): Isolated context, own tools/model/permissions. Cannot spawn sub-subagents.
- **Agent Teams**: Multiple independent sessions with shared tasks + messaging. 5x token burn vs single.
- **Hooks**: Deterministic scripts at lifecycle points. Zero LLM overhead.
- **MCP**: External service connections.

### Workflow Pattern
Official: Explore -> Plan -> Implement -> Commit (with Plan Mode via Ctrl+G)

### Critical Insights
- Context window is THE constraint. Performance degrades as it fills. Compaction at 95%.
- "Give Claude a way to verify its work" = single highest-leverage thing
- CLAUDE.md: "For each line, ask: Would removing this cause Claude to make mistakes? If not, cut it."
- ~150-200 instructions is the adherence limit for frontier LLMs
- Emphasis markers ("IMPORTANT", "YOU MUST") improve adherence
- Use JSON over Markdown for agent-maintained state (more resilient to corruption)
- Writer/Reviewer pattern: one Claude writes, fresh context reviews (avoids bias)

## State of the Art Research (Feb 2026)

### Context Engineering (4 strategies)
1. **Write**: scratchpads (within session), memories (across sessions)
2. **Select**: RAG/retrieval on demand, tool descriptions via RAG
3. **Compress**: summarize at 95% capacity, trim old messages, post-process tool outputs
4. **Isolate**: sub-agents with separate windows, sandboxing, selective state schemas

### Spec-Driven Development
- Major 2025-2026 pattern (Thoughtworks, GitHub Spec Kit, AWS Kiro)
- Separate planning/spec from implementation; specs as source of truth
- Use Given/When/Then, domain language, semi-structured inputs
- "Writing specifications is the new superpower" -- Sean Grove, OpenAI

### Multi-Agent Orchestration
- Hub-and-spoke for compliance; mesh for resilience; hybrid recommended
- Single-agent with strong prompts can match multi-agent in many cases
- Agent Teams patterns: leader, swarm, pipeline, watchdog
- Protocols: MCP, A2A (Google, 50+ companies), ACP, ANP

### Parallel Work Pattern
- Git worktrees = standard for parallel AI agents on same codebase
- Each agent: isolated workspace, branch, chat history, terminal

### Long-Running Agent Harness (Anthropic)
- Two-agent: initializer (first session) + coding agent (subsequent)
- Structured JSON feature list with pass/fail status
- Each session: read progress, run baseline tests, fix bugs, implement one feature

### Key Failure Modes
- Over-building (one-shotting instead of incremental)
- Context pollution (mixing unrelated tasks)
- Models disabling tests / adding placeholder TODOs
- "Set and forget" mentality; agents need continuous refinement

### Skill Authoring (Anthropic Official)
- Description: third person, specific, include trigger conditions
- Progressive disclosure: SKILL.md overview -> reference files one level deep
- Feedback loops: validate -> fix -> repeat
- Build evaluations BEFORE writing Skills (evaluation-driven development)
- Test across model tiers (Haiku, Sonnet, Opus)

### File References
- See `claude-code-features.md` for detailed feature comparison
- See `anthropic-internal-practices.md` for team-specific details
