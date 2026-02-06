# Skill: Documentation

Standards for creating and maintaining documentation.

---

## Documentation Types

### README.md
Every project should have a README with:
- Project name and one-line description
- How to install/setup
- How to run (dev, test, build)
- Key architecture decisions or pointers
- How to contribute

### API Documentation
- Document every public endpoint/interface
- Include request/response examples
- Note authentication requirements
- List error codes and their meanings

### Architecture Documentation
- High-level system overview
- Component boundaries and responsibilities
- Data flow diagrams (described textually)
- Key decisions and their rationale (ADRs)

### Inline Documentation
- Only where the "why" isn't obvious
- Never restate what the code already says
- Keep comments up-to-date with the code
- Use TODO with issue links for known improvements

## Writing Standards

- **Audience-appropriate** - Technical docs for developers, guides for users
- **Scannable** - Use headings, bullet points, code blocks
- **Current** - Outdated docs are worse than no docs
- **Minimal** - Don't document what's obvious or standard
- **Tested** - Code examples should actually work

## When to Update Documentation

- When public API changes
- When setup/installation process changes
- When new architectural decisions are made
- When documentation is discovered to be wrong
- Do NOT update docs for internal implementation changes
