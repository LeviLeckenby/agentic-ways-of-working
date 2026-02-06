---
description: "Mandatory Validation Pipeline rules for code changes"
---

# Validation Pipeline

Every code change MUST pass through the Mandatory Validation Pipeline before being considered complete:

1. **Self-Verification (Developer)**: Code compiles, tests pass, linting clean, no secrets
2. **Code Review (reviewer subagent - MANDATORY)**: Must output APPROVE or REQUEST CHANGES
3. **Security Review (security-auditor subagent - MANDATORY)**: Must output CLEAR or FINDINGS
4. **Conditional Validators**: Tester (new features), Architect (structural changes), Breaking change detection (API changes), Dependency audit (new deps), Accessibility check (UI changes), Performance review (hot paths)

Resolution: ALL Critical/High findings must be resolved. Medium/Low may be tracked with user consent.

Commit messages must include: `Validated-By: reviewer (Approved), security-auditor (Clear)`
