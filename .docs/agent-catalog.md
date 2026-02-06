# Agent Catalog

> Complete reference of all available agent personas in the workspace.

---

## Quick Reference

| Agent | Role | Model Tier | Primary Use |
|-------|------|------------|-------------|
| [Orchestrator](../agents/orchestrator.md) | Session management & delegation | Tier 1 (opus) | Coordinating all work |
| [Architect](../agents/architect.md) | System & software design | Tier 1 (opus) | Design decisions |
| [Developer](../agents/developer.md) | Code implementation | Tier 1-2 | Writing code |
| [Reviewer](../agents/reviewer.md) | Quality review | Tier 1-2 | Code & content review |
| [Researcher](../agents/researcher.md) | Information gathering | Tier 1-2 | Research tasks |
| [Planner](../agents/planner.md) | Task decomposition | Tier 1-2 | Planning & organizing |
| [Writer](../agents/writer.md) | Content creation | Tier 1-2 | Writing & documentation |
| [Tester](../agents/tester.md) | Quality assurance | Tier 2 (sonnet) | Test design & execution |
| [DevOps](../agents/devops.md) | Infrastructure & CI/CD | Tier 2 (sonnet) | Deployment & ops |
| [Security](../agents/security.md) | Security auditing | Tier 1 (opus) | Security review |
| [Analyst](../agents/analyst.md) | Data & business analysis | Tier 2 (sonnet) | Analysis & reporting |
| [Designer](../agents/designer.md) | UX & system design | Tier 1-2 | Design specifications |
| [Marketing](../agents/marketing.md) | Marketing strategy | Tier 2 (sonnet) | Marketing tasks |
| [Product](../agents/product.md) | Product management | Tier 1-2 | Requirements & prioritization |

> **Note on naming**: The Quick Reference above links to detailed persona docs in `agents/` which use short names (e.g., `security.md`, `marketing.md`, `product.md`). When invoking subagents via `.claude/agents/`, use the full compound names: `security-auditor`, `marketing-strategist`, `product-manager`.

---

## Agent Selection by Project Type

### Software Projects
| Phase | Primary Agent | Supporting Agents |
|-------|--------------|-------------------|
| Planning | Planner | Architect, Product |
| Design | Architect | Designer, Security |
| Implementation | Developer | Tester |
| Testing | Tester | Developer, Security |
| Review | Reviewer | Security, Architect |
| Deployment | DevOps | Developer |
| Documentation | Writer | Developer |

### Book / Content Projects
| Phase | Primary Agent | Supporting Agents |
|-------|--------------|-------------------|
| Planning | Planner | Writer, Product |
| Research | Researcher | Analyst |
| Writing | Writer | Researcher |
| Editing | Reviewer | Writer |
| Publishing | DevOps (technical) | Marketing |
| Promotion | Marketing | Writer, Analyst |

### Video / Audio Projects
| Phase | Primary Agent | Supporting Agents |
|-------|--------------|-------------------|
| Planning | Planner | Writer, Researcher |
| Research | Researcher | Analyst |
| Scripting | Writer | Researcher, Designer |
| Production | Planner | Designer |
| Post-Production | Writer (notes) | Reviewer |
| Distribution | Marketing | Analyst |

### Marketing / Campaign Projects
| Phase | Primary Agent | Supporting Agents |
|-------|--------------|-------------------|
| Strategy | Marketing | Researcher, Analyst |
| Planning | Planner | Marketing, Product |
| Content | Writer | Marketing, Designer |
| Execution | Developer (if technical) | Marketing |
| Analysis | Analyst | Marketing |

---

## Agent Interaction Patterns

### Independent Work
Agent works alone, returns results.
```
Orchestrator → Agent → Result
```
Best for: Research, analysis, initial drafts, code implementation

### Sequential Handoff
Output of one agent feeds into the next.
```
Researcher → Architect → Developer → Tester → Reviewer
```
Best for: Feature development, content creation pipelines

### Parallel Fan-Out
Multiple agents work simultaneously on independent tasks.
```
Orchestrator → [Researcher A, Researcher B, Developer C] → Synthesize
```
Best for: Multi-faceted research, independent feature work

### Review Loop
Work cycles between creator and reviewer until approved.
```
Developer ⇄ Reviewer (until approved)
```
Best for: Code review, content editing, design validation

### Collaborative Design
Multiple agents contribute perspectives to a design.
```
Product → Architect + Designer + Security → Synthesized Design
```
Best for: Architecture decisions, UX design, security-critical features

---

## Model Tier Recommendations

### Tier 1 (Highest - opus class)
Use for tasks requiring:
- Novel problem-solving or creative solutions
- Complex architectural reasoning
- Nuanced judgment calls
- Security analysis
- Multi-step strategic planning

### Tier 2 (Standard - sonnet class)
Use for tasks requiring:
- Standard code implementation
- Research and information synthesis
- Content writing and editing
- Test case design
- Configuration and tooling

### Tier 3 (Fast - haiku class)
Use for tasks requiring:
- File searching and reading
- Simple transformations
- Status checks and reporting
- Formatting and linting
- Mechanical, well-defined operations

---

## Creating Custom Agents

If a project needs a specialized agent not in this catalog:

1. Create a new file in `agents/{name}.md`
2. Follow the structure of existing agent files:
   - Identity section (who is this agent?)
   - Responsibilities (what does it do?)
   - Methodology (how does it work?)
   - Output format (what does it produce?)
   - When to invoke (trigger conditions)
3. Add the agent to this catalog
4. Reference it from the project's CLAUDE.md if project-specific

---

## Agent Memory

All subagent definitions in `.claude/agents/` include `memory: project` in their YAML frontmatter. This enables persistent memory scoped to the current project — agents retain learnings, patterns, and context across sessions within the same project directory.

When creating custom agents, include `memory: project` in the YAML frontmatter to enable this capability.
