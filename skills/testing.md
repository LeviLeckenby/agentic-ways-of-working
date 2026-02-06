# Skill: Testing

Testing strategies, patterns, and standards.

---

## Testing Philosophy

- Tests exist to catch regressions and document behavior
- A failing test should immediately tell you what broke
- Fast tests get run; slow tests get skipped. Keep them fast.
- Test behavior, not implementation details

## Test Levels

### Unit Tests
- Test a single function or method in isolation
- Mock external dependencies
- Should run in milliseconds
- Cover: core logic, calculations, transformations, edge cases

### Integration Tests
- Test how components work together
- Use real dependencies where practical (databases, file systems)
- Should run in seconds
- Cover: API endpoints, database queries, service interactions

### End-to-End Tests
- Test complete user flows
- Use the system as a user would
- Can run in minutes
- Cover: critical user journeys, authentication flows, payment paths

## Test Writing Standards

### Structure: Arrange-Act-Assert
```
// Arrange - Set up test data and conditions
// Act - Execute the behavior being tested
// Assert - Verify the result
```

### Naming Convention
```
test_{what_is_being_tested}_{scenario}_{expected_result}
```
Or the project's existing convention.

### One Assertion Per Test (Guideline)
- Each test should verify one behavior
- Multiple related assertions on the same result are fine
- Multiple assertions testing different behaviors should be separate tests

## What to Test

| Priority | What | Why |
|----------|------|-----|
| High | Public API / interfaces | These are contracts with consumers |
| High | Business logic | This is where bugs matter most |
| High | Error handling at boundaries | Failure modes affect users |
| Medium | State transitions | Complex state often has bugs |
| Medium | Edge cases (null, empty, boundary) | Common source of production issues |
| Low | Simple transformations | Low risk of bugs |
| Skip | Framework internals | Not your responsibility |
| Skip | Trivial code (getters, pass-through) | No logic to test |

## Test Data

- Use realistic but not real data
- Create factory functions or builders for complex test objects
- Never use production data in tests
- Keep test data close to the test that uses it

## When Tests Fail

1. Read the failure message carefully
2. Determine if the test or the code is wrong
3. If the code changed intentionally, update the test
4. If the code changed unintentionally, fix the regression
5. Never delete a test just because it fails
