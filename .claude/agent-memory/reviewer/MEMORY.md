# Reviewer Agent Memory

## Workspace Architecture
- CLAUDE.md is 248 lines (slightly over the 200-line ideal, within 300-line limit)
- ways-of-working.md is 698 lines (comprehensive methodology)
- agent-definitions.yaml is 2041 lines (47 agents defined)
- Two agent layers: `.claude/agents/` (12 subagents) vs `agents/` (15 personas + 2 YAML)
- Naming mismatches between layers: security-auditor vs security, marketing-strategist vs marketing, product-manager vs product
- Missing subagents: orchestrator, designer (exist in agents/ but not .claude/agents/)

## Key Review Findings (2026-02-06 Full Workspace Audit)
- Three-layer redundancy: .claude/agents/, agents/, agent-definitions.yaml all define overlapping agents
- CLAUDE.md references `security` persona but subagent is `security-auditor`
- ways-of-working.md duplicates ~40% of CLAUDE.md content (validation pipeline, session lifecycle)
- No audio project template despite audio being a supported project type
- No /debug, /test, /fix slash commands
- Orchestrator agent has no .claude/agents/ subagent (exists only in agents/)
- Designer agent has no .claude/agents/ subagent
- agent-catalog.md uses relative links (../../agents/) that may break
- Co-Authored-By in commit convention is hardcoded to Anthropic (not model-agnostic)
- No guidance on how non-Claude tools should handle .claude/agents/ YAML frontmatter

## Review Patterns
- Always cross-check consistency between CLAUDE.md, ways-of-working.md, agent definitions, and slash commands
- Check naming consistency across the two agent layers
- Verify all cross-references resolve correctly
