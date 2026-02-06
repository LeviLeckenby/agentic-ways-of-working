---
name: spec
description: "Create a Given/When/Then specification for a feature before implementation"
user-invocable: true
argument-hint: "[feature description]"
---

# Specification

Create a formal specification for a feature using Given/When/Then scenarios before implementation begins. This prevents spec drift — the gap between what was asked and what was built.

## Arguments
$ARGUMENTS - Description of the feature to specify

## When to Use
- Before implementing any non-trivial feature
- When requirements are ambiguous or complex
- When multiple agents will work on different parts of a feature
- Skip for: trivial changes, bug fixes with clear reproduction steps, config changes

## Instructions

1. **Understand the feature** described in: $ARGUMENTS
2. If the description is vague, ask clarifying questions before proceeding

3. **Define the core behavior** using Given/When/Then scenarios:
   ```
   ### Scenario: {descriptive name}
   Given: {precondition / initial state}
   When: {action / trigger}
   Then: {expected outcome / postcondition}
   ```

4. **Cover these dimensions**:
   - **Happy path**: The primary success scenario (at least 1)
   - **Edge cases**: Boundary conditions, empty inputs, max values (at least 2)
   - **Error cases**: Invalid inputs, unauthorized access, network failures (at least 2)
   - **Integration points**: How this feature interacts with existing systems

5. **Document constraints**:
   - Performance requirements (response time, throughput)
   - Compatibility requirements (browsers, APIs, versions)
   - Security requirements (auth, input validation, data protection)

6. **Define acceptance criteria**:
   - Measurable conditions that prove the feature works
   - Map each criterion to one or more Given/When/Then scenarios

7. **Output the specification** in a structured format:
   ```
   # Specification: {Feature Name}

   ## Overview
   {1-2 sentence summary}

   ## Scenarios
   {Given/When/Then scenarios}

   ## Constraints
   {Performance, compatibility, security requirements}

   ## Acceptance Criteria
   {Measurable conditions mapped to scenarios}

   ## Out of Scope
   {Explicitly excluded items}
   ```

8. **Save the spec** to the project's working directory (e.g., `specs/{feature-name}.md` or alongside the relevant code)

9. **Present to the user** for approval before implementation begins

10. **After approval**, the spec becomes the source of truth:
    - Developers implement against the scenarios
    - Reviewers validate against the acceptance criteria
    - Testers derive test cases from the Given/When/Then scenarios
