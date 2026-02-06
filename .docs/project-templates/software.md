# CLAUDE.md Template: Software Project

```markdown
# {Project Name}

> {One-line description}

## Project Type
software

## Tech Stack
- **Language**: {e.g., TypeScript, Python, Rust}
- **Framework**: {e.g., Next.js, FastAPI, Actix}
- **Database**: {e.g., PostgreSQL, MongoDB, SQLite}
- **Testing**: {e.g., Jest, pytest, cargo test}
- **Deployment**: {e.g., Vercel, Docker, AWS}

## Directory Structure
```
src/           # Source code
tests/         # Test files
docs/          # Documentation
scripts/       # Build and utility scripts
```

## Coding Conventions
- {Naming convention: camelCase, snake_case, etc.}
- {Formatting: prettier, black, rustfmt, etc.}
- {Import ordering convention}
- {Error handling pattern}
- {Logging convention}

## Development Workflow
1. Branch from main: `git checkout -b {type}/{description}`
2. Implement with tests
3. Run `{test command}` to verify
4. Run `{lint command}` to check style
5. Commit with conventional commit message
6. Push and create PR

## Architecture
{Brief description of the system architecture, key components, and their relationships}

## Key Decisions
- {ADR-001: Decision about X because Y}
- {ADR-002: Decision about X because Y}

## Current Goals
- [ ] {Goal 1}
- [ ] {Goal 2}
- [ ] {Goal 3}

## Agent Notes
- Primary agents: Architect, Developer, Tester, Reviewer
- Run tests after every significant change
- Follow existing patterns - don't introduce new patterns without Architect approval
```
