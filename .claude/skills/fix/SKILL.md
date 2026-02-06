---
name: fix
description: "Diagnose and fix a bug - investigates root cause, implements fix, runs tests, validates through the pipeline"
user-invocable: true
argument-hint: "[bug description]"
---

# Fix

Diagnose and fix a bug by investigating the root cause, implementing a minimal fix, adding regression tests, and validating through the Mandatory Validation Pipeline.

## Arguments
$ARGUMENTS - Description of the bug (symptoms, error messages, reproduction steps)

## Instructions

### 1. Parse the Bug Report

Extract the bug description from: $ARGUMENTS

If no description is provided or it is too vague to act on, ask the user for:
- **Symptoms**: What is happening? (error messages, incorrect output, crash)
- **Reproduction steps**: How do you trigger the bug?
- **Expected behavior**: What should happen instead?
- **Actual behavior**: What happens now?
- **Environment**: Any relevant context (OS, runtime version, branch)

### 2. Investigation Phase

Investigate to find the **root cause**, not just the symptom.

1. **Search for relevant code** using Grep and Glob:
   - Search for error messages, function names, or keywords from the bug description
   - Search for related test files to understand expected behavior
   - Search for recent changes to affected files (`git log --oneline -10 -- {file}`)
2. **Read the affected files** completely to understand the surrounding context:
   - Read the function/module where the bug manifests
   - Read the callers and callees to understand data flow
   - Read existing tests to see what is already covered
3. **Identify the root cause**:
   - Trace the execution path that triggers the bug
   - Determine whether the issue is in logic, data handling, state management, or external interaction
   - Distinguish between the symptom (what the user sees) and the cause (why it happens)
4. **If unclear**, ask the user targeted clarifying questions rather than guessing

### 3. Fix Phase

Implement the **minimal fix** that addresses the root cause.

- Fix the bug, not the entire file. Do not refactor surrounding code.
- Do not add features. Do not "improve" adjacent code. Just fix the bug.
- If the fix requires touching multiple files, change only what is necessary.
- Add a brief code comment explaining the fix if the root cause is non-obvious.

### 4. Regression Test

Add or update tests to cover the bug scenario so it cannot recur.

- Write a test that **fails without the fix** and **passes with the fix**
- Follow the project's existing test patterns and conventions
- Use AAA structure (Arrange-Act-Assert)
- The test should be named to describe the bug scenario (e.g., `test_handles_empty_input_without_crash`)
- If no test framework exists, note this and suggest one appropriate for the project

### 5. Validation Phase (MANDATORY)

This phase is non-negotiable. Do not skip it.

1. **Run the project's full test suite** -- ALL tests must pass, not just the new one
2. **Run linting/formatting** if the project has it configured
3. **Self-verify** that the fix addresses the original bug description
4. **Invoke the Mandatory Validation Pipeline**:
   - Hand off to the **reviewer** subagent with: changed files, original bug description, and the root cause explanation
   - Hand off to the **security-auditor** subagent if the fix touches: input handling, authentication, data storage, API endpoints, or dependency versions
5. **If validation fails**: fix the issues raised, re-run tests, and re-submit for validation. Loop until approved.

### 6. Report

Present the fix summary to the user:

```
## Bug Fix Report

### Root Cause
{What was actually wrong and why}

### Changes Made
- {file}: {what was changed and why}

### Regression Test
- {test file}: {test name} - {what it verifies}

### Validation Status
- Tests: {pass/fail, count}
- Reviewer: {Approved / Request Changes}
- Security: {Clear / Findings} (if applicable)

### Notes
{Any caveats, related issues discovered, or follow-up recommendations}
```
