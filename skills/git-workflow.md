# Skill: Git Workflow

Standard git operations and branching strategy for all projects.

---

## Branching Strategy

### Branch Naming
```
{type}/{short-description}
```

Types:
- `feat/` - New feature
- `fix/` - Bug fix
- `refactor/` - Code refactoring
- `docs/` - Documentation
- `test/` - Adding or updating tests
- `chore/` - Maintenance, dependencies, config
- `spike/` - Exploratory/research work (may be discarded)

Examples: `feat/add-auth`, `fix/login-redirect`, `docs/api-reference`

### Branch Rules
- Never commit directly to `main` or `master`
- Always branch from the latest main
- Keep branches short-lived (merge within 1-3 sessions)
- Delete branches after merging

## Commit Convention

```
{type}({scope}): {description}

{optional body: what and why, not how}

Co-Authored-By: {agent} <noreply@ai-agent.dev>
```

### Types
- `feat` - New feature
- `fix` - Bug fix
- `refactor` - Code restructuring without behavior change
- `docs` - Documentation only
- `test` - Adding or fixing tests
- `chore` - Build, deps, tooling
- `style` - Formatting, whitespace
- `perf` - Performance improvement
- `ci` - CI/CD changes

### Rules
- Subject line: imperative mood, no period, under 72 chars
- Body: explain what and why, wrap at 72 chars
- One logical change per commit
- Never include secrets or large binaries

## Common Operations

### Starting Work
```bash
git checkout main
git pull origin main
git checkout -b {type}/{description}
```

### Saving Progress
```bash
git add {specific-files}
git commit -m "{type}({scope}): {description}"
```

### Creating a PR
```bash
git push -u origin {branch}
gh pr create --title "{title}" --body "{description}"
```

### Handling Conflicts
1. Fetch latest main: `git fetch origin main`
2. Rebase or merge: `git rebase origin/main` (prefer rebase for clean history)
3. Resolve conflicts in each file
4. Continue: `git rebase --continue`
5. Force push to branch only (never to main): `git push --force-with-lease`

## Git Worktrees for Parallel Agent Work

When multiple agents need to work on different features simultaneously, use git worktrees to provide isolated workspaces:

```bash
# Create a worktree for each parallel agent
git worktree add ../project-feat-auth feat/add-auth
git worktree add ../project-feat-search feat/add-search

# Each agent works in its own worktree directory
# with its own branch, files, and terminal

# When done, remove the worktree
git worktree remove ../project-feat-auth
```

**Benefits**: Each agent gets an isolated workspace with its own branch, avoids merge conflicts during parallel development, and keeps the main working tree clean.

**Best for**: Agent Teams where each teammate owns a separate feature or module.

## Safety Rules
- NEVER force push to main/master
- NEVER use `--no-verify` to skip hooks
- NEVER use `git reset --hard` without user confirmation
- ALWAYS use `--force-with-lease` instead of `--force`
- ALWAYS verify branch before pushing
