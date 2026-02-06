---
description: "Code quality standards for source code files"
paths: ["*.ts", "*.tsx", "*.js", "*.jsx", "*.py", "*.rs", "*.go", "*.java", "*.rb", "*.php", "*.cs", "*.cpp", "*.c", "*.swift", "*.kt"]
---

# Code Quality Standards

- Read and understand existing code before modifying it
- Follow the project's existing conventions and patterns
- Write the simplest code that solves the problem - no over-engineering
- Handle errors appropriately at system boundaries, not everywhere
- Add tests for new behavior alongside implementation
- No dead code, unused imports, or leftover debug statements
- Functions should have single, clear responsibility
- Naming should be clear, consistent, and descriptive
- No features not explicitly requested
- Trust internal code; validate at system boundaries only
