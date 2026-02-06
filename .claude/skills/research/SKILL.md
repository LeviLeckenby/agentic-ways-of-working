---
name: research
description: "Conduct deep research on a topic using parallel investigation"
user-invocable: true
context: fork
---

# Research

Conduct deep research on a topic using the Researcher agent.

## Arguments
$ARGUMENTS - The research question or topic

## Instructions

1. Invoke the **Researcher Agent** (see `agents/researcher.md`) mindset
2. Parse the research question from: $ARGUMENTS
3. Determine research scope:
   - **Technical**: Technology evaluation, library comparison, best practices
   - **Domain**: Business domain, industry knowledge, competitive landscape
   - **Feasibility**: Can this be done? What are the constraints?
4. Execute the research methodology:
   - Define the question precisely
   - Search multiple sources (web, documentation, code)
   - Gather supporting and opposing viewpoints
   - Analyze findings for patterns and trade-offs
   - Synthesize into actionable recommendations
5. Use parallel subagents for independent research threads when appropriate
6. Output findings in the standard Research Output Format
7. Include confidence levels and knowledge gaps
8. Ask if the user wants to dive deeper into any finding
