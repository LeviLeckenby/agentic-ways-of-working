---
description: "Testing standards for test files"
paths: ["*test*", "*spec*", "tests/**", "**/__tests__/**"]
---

# Testing Standards

- Arrange-Act-Assert (AAA) structure
- One behavior per test (guideline, not strict rule)
- Descriptive test names: test_{what}_{scenario}_{expected}
- Tests should cover: happy path, critical failure modes, boundary conditions
- Tests should be fast: milliseconds for unit, seconds for integration
- Never delete a test just because it fails - determine if the test or code is wrong
- Tests must be meaningful - not just asserting trivially true conditions
- Use realistic but not real data
- Test public APIs and interfaces, not private implementation details
