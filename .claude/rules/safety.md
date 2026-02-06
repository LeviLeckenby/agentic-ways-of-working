---
description: "Core safety rules that apply to all files in the workspace"
---

# Safety Rules

- Never commit secrets, API keys, tokens, passwords, or certificates
- Never force-push to main/master branches
- Never delete files, branches, or data without explicit user confirmation
- Never bypass safety checks (--no-verify, skipping tests, disabling hooks)
- Never run destructive commands (rm -rf, DROP TABLE) without user approval
- Never expose internal system paths in outputs
- Always use --force-with-lease instead of --force when force-pushing to branches
- Treat all .env files as sensitive - never log or display their contents
