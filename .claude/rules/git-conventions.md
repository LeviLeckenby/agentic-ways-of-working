---
description: "Git workflow conventions for all projects"
---

# Git Conventions

- Branch naming: {type}/{short-description} (feat/, fix/, refactor/, docs/, test/, chore/, spike/)
- Commit format: {type}({scope}): {description}
- Commit types: feat, fix, refactor, docs, test, chore, style, perf, ci
- Subject line: imperative mood, no period, under 72 chars
- One logical change per commit
- Never commit directly to main/master - always use branches
- Keep branches short-lived (merge within 1-3 sessions)
- Delete branches after merging
