# Review

Perform a thorough review of recent changes or specified files.

## Arguments
$ARGUMENTS - What to review (files, PR, feature, etc.)

## Instructions

1. Invoke the **Reviewer Agent** (see `agents/reviewer.md`) mindset
2. Determine the scope of review from: $ARGUMENTS
   - If no specific target: review all uncommitted changes (git diff)
   - If a file/directory specified: review those files
   - If a PR number: fetch and review the PR
3. Perform the review using the appropriate checklist:
   - Code: correctness, style, security, tests, complexity
   - Content: accuracy, clarity, structure, voice, completeness
4. If the project has a security component, also invoke the **Security Agent** perspective
5. Output the review in the standard Review Output Format (see `agents/reviewer.md`)
6. Provide actionable feedback with specific suggestions
7. Offer to implement any fixes for critical issues found
