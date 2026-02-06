# Gemini Instructions

> **This file exists for compatibility with Gemini-based tools and workflows.**
> The source of truth is **CLAUDE.md** in this same directory.

---

## Required: Read CLAUDE.md

**Before doing anything else, you MUST read `CLAUDE.md` in this directory.** It contains the complete instructions for operating in this workspace, including:

- Session initialization protocol (ask the user which project to work on)
- Full methodology reference (`.docs/ways-of-working.md`)
- Agent persona catalog (`.docs/agent-catalog.md`)
- Workspace structure and conventions
- Safety rules and quality standards
- Available commands and workflows

## Quick Start

1. Read `CLAUDE.md` in this directory
2. Read `.docs/ways-of-working.md` for the full methodology
3. Follow the "On Session Start" protocol from CLAUDE.md
4. Ask the user which project to work on
5. Load project context and begin work

## Key Principle

This workspace uses an **agentic ways of working** methodology with specialized agent personas for different task types. The methodology is model-agnostic - it works with any AI model. See `agents/` for all persona definitions and `.docs/agent-catalog.md` for the complete catalog.

All instructions, conventions, and protocols are defined in `CLAUDE.md` and the documents it references. **CLAUDE.md is the single source of truth.**

## Gemini-Specific Notes

- When using Gemini models, apply the same agent persona system described in the methodology
- Model tier mapping: Gemini Ultra/Pro → Tier 1-2 tasks, Gemini Flash → Tier 3 tasks
- All workspace conventions, safety rules, and protocols apply regardless of model
