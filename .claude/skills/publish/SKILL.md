---
name: publish
description: "Prepare validated content for publishing - the content equivalent of /ship"
user-invocable: true
argument-hint: "[content description or scope]"
---

# Publish

Prepare validated content for publishing. This is the content project equivalent of `/ship` — it enforces quality gates before content is considered ready for publication.

## Arguments
$ARGUMENTS - Optional: specific content scope or publishing details

## Instructions

### 0. Content Validation Pipeline Check (BLOCKING)
Before ANYTHING else, verify the Content Validation Pipeline has been completed:
- Has the content been self-reviewed by the Writer? (structure, flow, style guide)
- Has a Reviewer (as Editor) approved the content? If not, invoke one now.
- Has a Researcher fact-checked the content? (for non-fiction/informational content) If not, invoke one now.
- Were conditional validators run as needed?
  - Marketing content → Brand voice review
  - Technical content → Technical accuracy review
  - SEO-relevant → SEO optimization check

**If validation has NOT been completed, RUN IT NOW before proceeding.**

### 1. Pre-publish checklist
- Review all content to be published
- Verify consistency across sections/chapters/episodes
- Check for any placeholder text, TODO markers, or incomplete sections
- Verify all references, links, and citations are valid
- Confirm style guide compliance throughout

### 2. Quality gates (run in parallel where possible)
- **Consistency check**: Voice, tone, terminology consistent throughout
- **Completeness check**: No gaps, all sections present, all promised content delivered
- **Accuracy check**: Facts verified, claims supported, references valid
- **Format check**: Proper formatting, no rendering issues, metadata complete
- **Accessibility check** (if applicable): Alt text, readability level, inclusive language

### 3. If ANY gate fails
- Report what failed and why
- Offer to fix issues
- Re-run failed checks after fixes
- Do NOT proceed until all gates pass

### 4. Prepare for publication
- Assemble final content in publication-ready format
- Generate any required metadata (descriptions, tags, categories)
- Create publication checklist specific to the platform/medium:
  - **Book**: Final manuscript, table of contents, front/back matter
  - **Video**: Final script, show notes, thumbnail copy, description, tags
  - **Audio**: Final script, show notes, transcript, distribution metadata
  - **Marketing**: Final copy, creative assets list, publication schedule
- Ask the user what to do next:
  a. Mark as ready for publication (update project tracking)
  b. Commit content to repository
  c. Export/package for external platform

### 5. Post-publish
- Update project progress tracking
- Note any follow-up items (promotion, analytics setup, etc.)
- Summarize what was published with validation status
