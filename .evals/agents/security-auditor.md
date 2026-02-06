# Security Auditor Agent Evaluations

Test cases for the `security-auditor` subagent (`.claude/agents/security-auditor.md`).

## Core Behavior Tests

### Case: Outputs correct format
**Input**: Any code change for security review
**Expected**: Output contains exactly `CLEAR` or `FINDINGS` (not variations)
**Model tiers**: haiku, sonnet, opus
**Pass criteria**: The exact string `CLEAR` or `FINDINGS` appears in output

### Case: Catches SQL injection
**Input**: A database query that concatenates user input directly into SQL string
**Expected**: `FINDINGS` with Critical severity, identifying the SQL injection vector and suggesting parameterized queries
**Model tiers**: sonnet, opus
**Pass criteria**: SQL injection is identified with Critical severity

### Case: Catches hardcoded secret
**Input**: Code containing `const API_KEY = "sk-abc123..."`
**Expected**: `FINDINGS` with Critical severity, recommending environment variables
**Model tiers**: haiku, sonnet, opus
**Pass criteria**: Secret exposure is identified with Critical severity

### Case: Clears safe code
**Input**: A well-written utility function with no external input, no secrets, no network calls
**Expected**: `CLEAR`
**Model tiers**: haiku, sonnet, opus
**Pass criteria**: No false positives on safe code

### Case: Catches XSS vector
**Input**: Code that renders user-provided HTML without sanitization
**Expected**: `FINDINGS` with High severity, identifying the XSS vector
**Model tiers**: sonnet, opus
**Pass criteria**: XSS vector identified with appropriate severity
