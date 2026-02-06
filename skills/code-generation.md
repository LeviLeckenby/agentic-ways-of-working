# Skill: Code Generation

Patterns and standards for generating high-quality code.

---

## Principles

1. **Read before write** - Always understand existing code before adding to it
2. **Match the style** - Follow the project's existing conventions
3. **Minimal changes** - Make the smallest change that solves the problem
4. **Test alongside** - Write tests with the implementation, not after
5. **No gold-plating** - Only build what was requested

## Pre-Generation Checklist

Before writing any code:
- [ ] Read the relevant existing files
- [ ] Identify the coding style (naming, formatting, patterns)
- [ ] Understand the testing approach
- [ ] Know the project's error handling conventions
- [ ] Check for existing utilities that might be reused

## Code Quality Standards

### Naming
- Variables/functions: descriptive, following project convention (camelCase, snake_case, etc.)
- Files: match project's file naming convention
- Constants: UPPER_CASE or project convention
- Types/Classes: PascalCase or project convention

### Structure
- Functions do one thing
- Files have a single responsibility
- Imports are organized (stdlib, external, internal)
- No circular dependencies

### Error Handling
- Validate at system boundaries (user input, API responses)
- Trust internal code - don't validate between internal functions
- Use the project's error handling pattern (exceptions, Result types, etc.)
- Provide meaningful error messages at user-facing boundaries

### Documentation
- Don't add documentation to code you didn't change
- Code should be self-documenting where possible
- Add comments only where the "why" isn't obvious from the code
- Update existing documentation when you change documented behavior

## Anti-Patterns to Avoid

- Creating abstractions for single-use code
- Adding feature flags for new features (just build the feature)
- Writing defensive code for impossible states
- Adding backward-compatibility shims in new code
- Over-parameterizing functions "for flexibility"
- Creating utility files for one helper function
