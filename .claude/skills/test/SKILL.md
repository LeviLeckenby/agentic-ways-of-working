---
name: test
description: "Run project tests, analyze results, identify failures, and suggest fixes"
user-invocable: true
---

# Test

Run the project's test suite, analyze results, identify failures, and optionally write new tests to improve coverage.

## Arguments
$ARGUMENTS - Optional: specific test file/directory, or "write"/"cover" to generate new tests

## Instructions

### 1. Detect Test Framework

Determine how this project runs tests by checking (in order):

1. **Read the project's CLAUDE.md** (`repos/{project}/CLAUDE.md`) for explicit test instructions -- this takes precedence over auto-detection
2. **Check package.json** for `scripts.test`, `scripts.test:unit`, `scripts.test:e2e` (JavaScript/TypeScript projects: jest, vitest, mocha, playwright)
3. **Check for pytest** (`pytest.ini`, `pyproject.toml [tool.pytest]`, `setup.cfg`, or `conftest.py`)
4. **Check for Cargo.toml** (Rust: `cargo test`)
5. **Check for go.mod** (Go: `go test ./...`)
6. **Check for build.gradle or pom.xml** (Java/Kotlin: gradle test, mvn test)
7. **Check for mix.exs** (Elixir: `mix test`)
8. **Check for Makefile** with a `test` target

If no test framework is detected, report this to the user and suggest an appropriate framework based on the project's language and structure.

### 2. Run Tests

Run the test suite based on $ARGUMENTS:

- **No arguments**: Run the full test suite
- **Specific file/directory**: Run only those tests
- **"write" or "cover"**: Skip to Phase 4 (Write New Tests) after running existing tests first

Capture the full output including:
- Total tests run
- Tests passed
- Tests failed
- Tests skipped
- Coverage report (if the test runner produces one)
- Execution time

### 3. Analyze Results

#### If ALL tests pass:

Report the summary:
```
## Test Results: ALL PASSING

- Total: {count}
- Passed: {count}
- Skipped: {count} {list skipped test names if any}
- Coverage: {percentage if available}
- Duration: {time}
```

If coverage data is available and below 80%, note which areas lack coverage.

#### If tests FAIL:

For EACH failing test:

1. **Read the failing test file** to understand what it expects
2. **Read the code under test** to understand the actual behavior
3. **Determine the cause**: Is the test wrong, or is the code wrong?
   - **Test is wrong**: The code behavior is correct but the test has an outdated expectation, wrong assertion, or flawed setup
   - **Code is wrong**: The test expectation is correct but the code has a bug
   - **Both need updating**: An intentional behavior change was made but the test was not updated
   - **Environment issue**: Test depends on external state, timing, or configuration
4. **Suggest a specific fix** with the exact code change needed

Report each failure:
```
## Test Results: {count} FAILING

### Failure 1: {test name}
- **File**: {test file path}:{line}
- **Error**: {error message}
- **Diagnosis**: {test wrong | code wrong | both | environment}
- **Root cause**: {explanation}
- **Suggested fix**: {specific code change}
```

Ask the user if they want the fixes applied automatically.

### 4. Write New Tests (when $ARGUMENTS contains "write" or "cover")

Generate new tests to improve coverage.

#### 4a. Analyze Coverage Gaps

1. If a coverage report is available, identify files and functions with low or no coverage
2. If no coverage report, use heuristic analysis:
   - Find all source files using Glob
   - Find all test files using Glob
   - Identify source files that have no corresponding test file
   - Within tested files, identify exported functions/methods that have no test

#### 4b. Write Tests

For each coverage gap, write tests following these principles:

- **Match the project's existing test patterns**: naming conventions, file organization, import style, assertion library
- **Use AAA structure** (Arrange-Act-Assert) for each test
- **Cover three categories** in priority order:
  1. **Happy path**: Normal expected inputs produce correct outputs
  2. **Critical failure modes**: Invalid inputs, null/undefined, empty collections, network failures, permission errors
  3. **Boundary conditions**: Zero, one, max values, empty strings, large inputs, Unicode, concurrent access
- **Test names should describe the scenario**, not the implementation (e.g., `should return empty array when no items match filter` not `test_filter_function`)
- **Each test should be independent** -- no shared mutable state between tests
- **Avoid testing implementation details** -- test behavior and outcomes, not internal method calls

#### 4c. Verify New Tests

1. Run the new tests to confirm they pass
2. Run the full test suite to confirm nothing was broken
3. Report what was added:

```
## New Tests Written

### {test file}
- {test name}: {what it covers}
- {test name}: {what it covers}

### Coverage Impact
- Before: {percentage or "unknown"}
- After: {percentage or "unknown"}
- New tests: {count}
```
