---
name: start
description: "Initialize a new working session - lists projects, loads context, establishes goals"
user-invocable: true
argument-hint: "[project-name]"
---

# Session Start

Initialize a new working session in the agentic-wow workspace.

## Instructions

1. Read the workspace CLAUDE.md for current configuration
2. List available projects by scanning the `repos/` directory
3. Present the user with:
   - List of existing projects (with brief description from each project's CLAUDE.md if available)
   - Option to create a new project
   - Option to work on workspace-level tasks (methodology, agents, skills)
4. Once the user selects a project:
   - Read `repos/{project}/CLAUDE.md` if it exists
   - Check `git status` in the project directory
   - Look for TODO.md, CHANGELOG.md, or open issues
   - Summarize the current state of the project
5. Ask the user what they want to accomplish this session
6. Create a task list based on their goals
7. Begin execution using the appropriate agent personas

## Context
- Workspace root: Current working directory
- Projects live in: `repos/`
- Agent definitions: `agents/`
- Methodology: `.docs/ways-of-working.md`
