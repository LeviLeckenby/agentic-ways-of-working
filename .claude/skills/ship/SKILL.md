---
name: ship
description: "Prepare validated changes for shipping - enforces quality gates before commit/push/PR"
user-invocable: true
---

# Ship

Prepare validated changes for shipping - enforce quality gates, create commits, and optionally push/create PR.

## Arguments
$ARGUMENTS - Optional: specific scope or PR details

## Instructions

### 0. Validation Pipeline Check (BLOCKING)
Before ANYTHING else, verify the Mandatory Validation Pipeline has been completed:
- Has the `reviewer` subagent approved the changes? If not, invoke it now.
- Has the `security-auditor` subagent cleared the changes? If not, invoke it now.
- Were conditional validators run (tester, architect, etc.) as needed? If not, invoke them.
- Are ALL Critical/High findings resolved?

**If validation has NOT been completed, RUN IT NOW before proceeding.** Do not skip this step. Do not allow the user to skip this step without explicitly acknowledging the risk.

### 1. Pre-flight checks
- Run `git status` to see all changes
- Run `git diff` to review what's being shipped
- Check for any uncommitted work that shouldn't be included
- Verify no secrets or sensitive files are staged (.env, keys, tokens, credentials)

### 2. Automated quality gates (run in parallel)
- Run the project's test suite → ALL must pass (BLOCKING)
- Run linting/formatting → must be clean (BLOCKING)
- Run type checking if applicable → must pass (BLOCKING)
- Scan for TODO/FIXME items in changed files → report but don't block

### 3. If ANY gate fails
- Report what failed and why with specific details
- Offer to fix issues automatically
- After fixes, re-run the failed gate(s). If the fix was substantial, re-run ALL gates.
- Do NOT proceed to commit until all gates pass

### 4. Compose commit
- Stage appropriate files (NEVER stage .env, credentials, keys, etc.)
- Create a well-formed commit message following conventions:
  ```
  {type}({scope}): {description}

  {body explaining what and why}

  Validated-By: reviewer (Approved), security-auditor (Clear)
  Tests: All passing ({count} tests)
  ```
- Ask the user if they want to:
  a. Just commit locally
  b. Push to remote
  c. Create a pull request

### 5. If creating a PR
- Use the standard PR template with:
  - Summary of changes (what and why)
  - Validation status (review approved, security cleared)
  - Test plan / verification steps
  - Any known limitations or follow-up items
- Link to any related issues

### 6. Post-ship
- Update any TODO tracking
- Summarize what was shipped with validation status
- Note any Medium/Low security findings tracked for follow-up
