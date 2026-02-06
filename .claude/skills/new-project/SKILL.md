---
name: new-project
description: "Create a new project in the workspace with proper structure and CLAUDE.md"
user-invocable: true
---

# New Project

Create a new project in the workspace.

## Instructions

1. Ask the user for:
   - **Project name** (will be used as the directory name in `repos/`)
   - **Project type**: software | book | video | audio | marketing | general
   - **Brief description**: One-liner about the project
   - **Tech stack** (if software): Languages, frameworks, key dependencies
   - **Repository URL** (optional): If cloning an existing repo

2. If cloning an existing repo:
   ```
   cd repos && git clone {url} {project-name}
   ```

3. If creating from scratch:
   ```
   mkdir -p repos/{project-name}
   cd repos/{project-name} && git init
   ```

4. Create a `CLAUDE.md` in the new project based on the project type template from `.docs/project-templates/`

5. Include in the project's CLAUDE.md:
   - Project name and description
   - Project type
   - Tech stack (if applicable)
   - Coding/style conventions (if applicable)
   - Directory structure expectations
   - Key goals / roadmap items

6. Create initial project structure based on type:
   - **Software**: src/, tests/, docs/, README.md, .gitignore
   - **Book**: chapters/, notes/, outline.md, style-guide.md
   - **Video**: scripts/, assets/, storyboards/, production-notes.md
   - **Audio**: scripts/, episodes/, show-notes/, planning.md
   - **Marketing**: campaigns/, content/, analytics/, strategy.md
   - **General**: docs/, notes/, README.md

7. Confirm creation to the user and ask what they want to work on first
