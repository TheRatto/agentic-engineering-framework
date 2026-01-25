# Documentation Skill

## When to use
Use this skill when updating documentation related to a feature or recent changes. The Documentation agent keeps project documentation current and accurate.

## How to invoke
- Slash command: `/docs` or `/documentation`
- Example: `/docs update docs for feature F-010`
- Or mention: "update documentation" or "document feature F-010"

## Context required
- Feature ID (if feature-specific)
- Implementation summaries from `reports/implementation/`
- STATUS.md (current project state)
- Relevant artefacts (ARCHITECTURE.md, UI_SPEC.md, ADRs)

## What this skill does
1. Reads `framework/agents/DOCS.md` for full role definition and constraints
2. Reads framework documents (FRAMEWORK_OVERVIEW.md, WORKFLOW.md, ARTEFACTS.md, STYLE_GUIDE.md, TEMPLATES.md)
3. Reviews documentation context: implementation summaries, STATUS.md, relevant artefacts
4. Identifies documentation that no longer reflects reality
5. Updates existing documents (preferred over creating new ones)
6. Produces documentation update summary
7. Updates CHANGELOG.md if required

## Constraints
- Does not invent behaviour
- Does not modify code
- Prefers updating existing documents over creating new ones
- Only documents what actually exists
- Follows CHANGELOG_SCHEMA.md for changelog entries

## Outputs
- Documentation updates (ARCHITECTURE.md, README.md, API docs, etc.)
- Documentation Update Summary (per TEMPLATES.md)
- Changelog entry if required (following CHANGELOG_SCHEMA.md)

## Related skills
- `/tester` - Previous step (after feature validation)
- `/coder` - If documentation is needed during implementation
- `/orchestrate` - To run complete feature workflow

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Reads framework documents
2. Reads role definition: `framework/agents/DOCS.md`
3. Reviews documentation context: implementation summaries, STATUS.md, relevant artefacts
4. Identifies documentation that no longer reflects reality
5. Stops and asks if scope is unclear

## Definition of Done (Documentation Perspective)
Documentation work is complete when:
- All relevant documentation reflects current reality
- Updates are clear and accurate
- Changelog is updated if user-visible changes occurred
- Documentation Update Summary is filed
