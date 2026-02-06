---
name: review-wow
description: "Perform a comprehensive review of the agentic ways-of-working methodology - identifies gaps, inconsistencies, and improvements by researching frontier model provider best practices and industry experts"
user-invocable: true
---

# Review Ways of Working

Perform a comprehensive review of the agentic ways-of-working methodology itself. This is a meta-skill for continuously improving how we work.

## Purpose

The agentic workflow landscape evolves rapidly. This skill ensures our methodology stays current, internally consistent, and aligned with best practices from frontier model providers and industry experts. Run this regularly (monthly or after major agentic tooling updates).

## Instructions

### Phase 1: Parallel Investigation

Launch **3 subagents in parallel**, each with a distinct review focus. Every subagent MUST read the actual files listed below -- do not guess at contents or rely on assumptions.

#### Files to Read (provide these paths to ALL subagents)

**Core configuration:**
- `A:/A-Dev/agentic-wow/CLAUDE.md`
- `A:/A-Dev/agentic-wow/AGENTS.md`
- `A:/A-Dev/agentic-wow/GEMINI.md`
- `A:/A-Dev/agentic-wow/.claude/settings.json`

**Methodology:**
- `A:/A-Dev/agentic-wow/.docs/ways-of-working.md`
- `A:/A-Dev/agentic-wow/.docs/agent-catalog.md`

**Subagent definitions (read ALL):**
- `A:/A-Dev/agentic-wow/.claude/agents/*.md`

**Skills (read ALL):**
- `A:/A-Dev/agentic-wow/.claude/skills/*/SKILL.md`

**Rules (read ALL):**
- `A:/A-Dev/agentic-wow/.claude/rules/*.md`

**Agent persona documentation (read ALL):**
- `A:/A-Dev/agentic-wow/agents/*.md`

**Legacy skill references (read ALL):**
- `A:/A-Dev/agentic-wow/skills/*.md`

**Project templates (read ALL):**
- `A:/A-Dev/agentic-wow/.docs/project-templates/*.md`

---

#### Subagent 1: Internal Consistency Audit (reviewer subagent)

**Task:** Read every file listed above and audit for internal consistency across the entire workspace.

**Check for:**
- **Cross-reference consistency**: Do file references in one document point to files that actually exist? Are paths correct?
- **Naming alignment**: Are agent names, skill names, and role references consistent across CLAUDE.md, .claude/agents/, agents/, skills/, and .docs/?
- **Content duplication**: Is the same information maintained in multiple places? If so, do the copies agree? Flag any divergence.
- **Stale references**: Are there references to files, tools, features, or workflows that no longer exist or have been renamed?
- **Broken links**: Do all internal document references resolve to real files?
- **Table of Contents accuracy**: Do TOC entries in .docs/ways-of-working.md and .docs/agent-catalog.md match the actual section headings?
- **Contradictions**: Do any two files give conflicting instructions about the same topic (e.g., model tier assignments, validation requirements, git conventions)?
- **YAML frontmatter validity**: Do all .claude/agents/*.md and .claude/skills/*/SKILL.md files have valid, complete frontmatter?

**Output format:**
```
## Internal Consistency Audit

### Critical Issues (broken references, contradictions)
- {file}: {issue}

### Inconsistencies (naming, duplication divergence)
- {file A} vs {file B}: {discrepancy}

### Stale Content
- {file}: {what is stale and why}

### All Clear
- {areas that are well-maintained}
```

---

#### Subagent 2: Workflow Gap Analysis (reviewer subagent)

**Task:** Read every file listed above, then mentally walk through each end-to-end workflow and identify gaps.

**Workflows to trace:**
1. **Session start to first task**: User opens a session -> /start -> project selection -> context loading -> first meaningful work. Is the handoff smooth? Are there missing steps?
2. **Planning to implementation**: /plan -> task decomposition -> agent assignment -> parallel execution -> assembly. Are handoffs between agents well-defined?
3. **Implementation to validation**: Code written -> self-verification -> reviewer subagent -> security-auditor subagent -> approval. Is the pipeline complete? Can steps be skipped accidentally?
4. **Validation to shipping**: Approved code -> /ship -> quality gates -> commit -> push/PR. Are there gaps between validation and commit?
5. **Bug fix workflow**: Bug reported -> investigation -> fix -> regression test -> validation. Is there a clear path?
6. **Content/non-code projects**: Book writing, video production, marketing campaigns. Do the workflows support non-software projects adequately?
7. **Multi-project workflow**: Switching between projects, cross-project dependencies. Is context properly managed?
8. **Error recovery**: What happens when a subagent fails? When tests fail? When validation is rejected? Are recovery paths documented?
9. **Onboarding**: A new user or agent encountering this workspace for the first time. Is the documentation self-explanatory? What would confuse them?

**Check for:**
- Missing handoffs between agents or workflow stages
- Error recovery holes (what happens when things go wrong?)
- Implicit assumptions that are not documented
- Workflows that are described but have no supporting skill or command
- Onboarding friction (what would a newcomer struggle with?)
- Content project workflow gaps (non-code projects being second-class)
- Context management gaps (when should /clear or /compact be used and is this documented clearly?)

**Output format:**
```
## Workflow Gap Analysis

### Missing Handoffs
- {workflow}: {where the gap is} -> {suggested fix}

### Error Recovery Holes
- {scenario}: {what is missing}

### Onboarding Issues
- {what would confuse a newcomer}

### Content Project Gaps
- {what non-code projects are missing}

### Strengths
- {workflows that are well-designed}
```

---

#### Subagent 3: Best Practices Research (researcher subagent)

**Task:** Search the web for the latest best practices on agentic workflows, then compare against our current methodology.

**Research topics (search for EACH of these):**
1. **Anthropic's latest guidance** on Claude Code, multi-agent patterns, CLAUDE.md best practices, subagent orchestration, and context management
2. **OpenAI's latest guidance** on agentic workflows, Codex, agent orchestration patterns, and multi-agent systems
3. **Google's latest guidance** on agentic workflows, Gemini agent patterns, and AGENTS.md conventions
4. **Industry expert recommendations** on agentic coding workflows (blog posts, conference talks, research papers from 2024-2025)
5. **Multi-agent orchestration patterns** - delegation, fan-out/fan-in, chain-of-thought, validation pipelines
6. **Context management strategies** - how leading teams manage context windows, when to fork vs chain agents
7. **Validation and quality patterns** - automated review, security scanning, test-driven agentic development
8. **Memory and persistence patterns** - how to maintain state across sessions, project memory best practices

**For each topic, compare against our current methodology:**
- What are we already doing well?
- What are we missing?
- What are we doing that contradicts current best practices?
- What new patterns or techniques should we consider adopting?

**Output format:**
```
## Best Practices Research

### Our Methodology vs. Industry Best Practices

#### Aligned (we're doing this well)
- {practice}: {evidence from sources}

#### Gaps (we should adopt)
- {practice}: {what it is, why it matters, source}

#### Contradictions (we should reconsider)
- {our practice} vs {recommended practice}: {source and reasoning}

#### Emerging Patterns (worth watching)
- {pattern}: {description, maturity level}

### Sources
- {URL or reference}: {key takeaway}
```

---

### Phase 2: Synthesis

After all 3 subagents complete, synthesize their findings into a single prioritized report.

**Report structure:**

```
# Ways of Working Review Report

## Date: {today's date}

## MUST FIX (blocking issues)
Issues that could cause incorrect behavior, broken workflows, or misleading guidance.
- {issue}: {source subagent} - {recommended action}

## SHOULD FIX (significant improvements)
Issues that meaningfully reduce quality, efficiency, or clarity.
- {issue}: {source subagent} - {recommended action}

## NICE TO HAVE (incremental improvements)
Polish, optimization, and forward-looking enhancements.
- {issue}: {source subagent} - {recommended action}

## DOING WELL (validation of current practices)
What we should keep doing -- important for morale and preventing regression.
- {practice}: {why it works well}
```

**Deduplication rules:**
- If multiple subagents flag the same issue, merge them into one item with combined evidence
- Prioritize by impact: broken functionality > inconsistency > missing feature > polish
- For best practices gaps, classify based on how established the practice is (well-established = SHOULD FIX, emerging = NICE TO HAVE)

### Phase 3: User Decision

1. Present the synthesized report to the user
2. Ask which items they want to implement now
3. For approved items, create a prioritized task list
4. Begin execution, using appropriate subagents for each task
5. After implementation, re-run relevant consistency checks to verify fixes
