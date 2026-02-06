# Skill: Refactoring

Patterns and practices for safely restructuring code.

---

## Refactoring Principles

1. **Never refactor and change behavior at the same time** - One or the other per commit
2. **Tests first** - Ensure tests cover the current behavior before changing structure
3. **Small steps** - Each refactoring step should be individually verifiable
4. **Keep it green** - Tests should pass after every step

## Common Refactoring Patterns

### Extract Function
When a block of code does a distinct thing, extract it into a named function.
- Trigger: Code block with a comment explaining what it does
- Trigger: Same code pattern in multiple places

### Inline Function
When a function's body is as clear as its name.
- Trigger: Single-use function that adds indirection without clarity

### Rename
When a name doesn't clearly communicate purpose.
- Trigger: You have to read the implementation to understand what it does

### Move
When code is in the wrong module/file/class.
- Trigger: Function uses more from another module than its own

### Simplify Conditional
When conditionals are nested or complex.
- Trigger: More than 2 levels of nesting, or conditions that are hard to read

### Replace Primitive with Type
When a primitive (string, number) represents a domain concept.
- Trigger: Validation logic scattered across multiple locations

## Safety Checklist

Before refactoring:
- [ ] Tests exist and pass for the code being changed
- [ ] I understand what the code does
- [ ] I have a clear goal for the refactoring
- [ ] The scope is manageable (not refactoring the world)

During refactoring:
- [ ] Each step is small and verifiable
- [ ] Tests pass after each step
- [ ] No behavior changes mixed in

After refactoring:
- [ ] All tests still pass
- [ ] Code is measurably better (clearer, simpler, less duplicated)
- [ ] No dead code left behind
