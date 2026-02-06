# Reviewer Agent Evaluations

Test cases for the `reviewer` subagent (`.claude/agents/reviewer.md`).

## Core Behavior Tests

### Case: Outputs correct format
**Input**: Any code change for review
**Expected**: Output contains exactly `APPROVE` or `REQUEST CHANGES` (not variations like "approved" or "changes requested")
**Model tiers**: haiku, sonnet, opus
**Pass criteria**: The exact string `APPROVE` or `REQUEST CHANGES` appears in the output

### Case: Catches obvious bug
**Input**: A function that has an off-by-one error in a loop boundary
**Expected**: `REQUEST CHANGES` with specific identification of the off-by-one error
**Model tiers**: sonnet, opus
**Pass criteria**: The error is identified and the fix is actionable

### Case: Doesn't over-review trivial changes
**Input**: A documentation-only change (fixing a typo in a README)
**Expected**: `APPROVE` without requesting unnecessary code changes
**Model tiers**: haiku, sonnet, opus
**Pass criteria**: Approval without scope creep

### Case: Validates against requirements
**Input**: Code that compiles and passes tests but doesn't match the stated requirement
**Expected**: `REQUEST CHANGES` citing the requirement mismatch
**Model tiers**: sonnet, opus
**Pass criteria**: The requirement gap is identified specifically

### Case: Detects dead code
**Input**: Code change that includes an unused import and an unreachable code path
**Expected**: `REQUEST CHANGES` mentioning the dead code
**Model tiers**: sonnet, opus
**Pass criteria**: Both the unused import and unreachable path are flagged
