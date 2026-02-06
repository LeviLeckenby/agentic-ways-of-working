# Reviewer Agent Memory

## Workspace Architecture (Updated 2026-02-06)
- CLAUDE.md is 156 lines (well within 200-line ideal)
- ways-of-working.md is 855 lines (comprehensive methodology)
- Two agent layers: `.claude/agents/` (14 subagents) vs `agents/` (14 personas + _base.md)
- Naming mismatches across layers: security-auditor vs security, marketing-strategist vs marketing, product-manager vs product
- Both orchestrator and designer now exist in .claude/agents/
- `.claude/commands/` and `.claude/skills/` contain identical content (full duplication)
- `.claude/rules/` has 7 glob-scoped rule files
- 6 project templates exist (software, book, video, audio, marketing, general)
- `skills/` (root) has 8 reference docs distinct from `.claude/skills/`

## Key Findings (2026-02-06 Full Workspace Audit)
- See `workflow-gaps-analysis.md` for detailed 19-finding analysis
- Top issues: commands/skills duplication, no README, missing /fix and /test skills, undefined fix-resubmit loop, no subagent failure recovery
- Content project validation is code-centric (pipeline doesn't adapt for non-code)
- Stop hook is a blunt instrument (fires on every response, subjective self-assessment)
- ways-of-working.md structure diagram is outdated (doesn't show skills, agents, rules, settings.json)
- Autonomy levels and Agent Teams are documented but not actionable
- "skills" vs "commands" terminology inconsistency throughout

## Review Patterns
- Always cross-check consistency between CLAUDE.md, ways-of-working.md, agent definitions, and slash commands
- Check naming consistency across the two agent layers
- Verify all cross-references resolve correctly
- Check for commands/skills duplication when either is modified
- Verify ways-of-working.md structure diagram matches reality after structural changes
