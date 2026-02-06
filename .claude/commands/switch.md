# Switch Project

Switch the active project context to a different repository.

## Instructions

1. List all available projects in `repos/` with their descriptions
2. Let the user select which project to switch to
3. Load the selected project's context:
   - Read `repos/{project}/CLAUDE.md`
   - Check git status for current state
   - Look for in-progress work (branches, uncommitted changes)
   - Check TODO.md or task tracking
4. Summarize the project's current state
5. Ask what the user wants to work on in this project
