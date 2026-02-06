# Agent & Skill Evaluations

Evaluation-driven development: build evaluations BEFORE implementing agents or skills (like TDD for agents).

## Structure

```
.evals/
├── README.md           # This file
├── agents/             # Agent-specific evaluation cases
│   ├── reviewer.md     # Reviewer agent eval cases
│   └── security-auditor.md  # Security auditor eval cases
└── skills/             # Skill-specific evaluation cases
    └── ship.md         # Ship skill eval cases
```

## How to Use

1. Before modifying an agent or skill, read its eval cases
2. After modification, manually verify the agent/skill against each case
3. Document any new edge cases discovered during testing
4. Gate on evals — don't ship agents/skills that fail evaluations

## Evaluation Cadence

- **On every change** to an agent/skill definition
- **Monthly** as part of `/review-wow`
- **After model updates** — new model versions may change behavior

## Adding New Evaluations

Each eval file contains test cases in this format:

```markdown
### Case: {descriptive name}
**Input**: {what to give the agent/skill}
**Expected**: {what the agent/skill should produce}
**Model tiers**: {which tiers this should work on}
**Pass criteria**: {how to judge pass/fail}
```
