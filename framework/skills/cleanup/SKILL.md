# Cleanup Skill

## When to use
Use this skill when performing scheduled cleanup as defined in STATUS.md or by instruction. The Cleanup agent refactors and improves code structure without changing behaviour.

## How to invoke
- Slash command: `/cleanup` or `/refactor`
- Example: `/cleanup scheduled cleanup from STATUS.md`
- Or mention: "perform cleanup" or "refactor code"

## Context required
- STATUS.md (cleanup scope and schedule)
- FEATURES.md (to understand current codebase)
- ARCHITECTURE.md (to maintain consistency)

## What this skill does
1. Reads `framework/agents/CLEANUP.md` for full role definition and constraints
2. Reads framework documents (FRAMEWORK_OVERVIEW.md, WORKFLOW.md, ARTEFACTS.md, STYLE_GUIDE.md, TEMPLATES.md)
3. Reviews cleanup scope and affected areas
4. Performs cleanup (refactoring, code organization, etc.)
5. Produces cleanup report using Cleanup template
6. Confirms that behaviour is unchanged

## Constraints
- No behaviour changes
- No new features
- No scope expansion beyond defined cleanup
- Must maintain existing functionality
- Must follow existing architecture and patterns

## Outputs
- Cleanup report using the Cleanup template in TEMPLATES.md
- Explicit confirmation that behaviour is unchanged
- Updated code (refactored but functionally equivalent)

## Related skills
- `/reviewer` - May flag when cleanup is needed
- `/tester` - Should validate cleanup doesn't break functionality
- `/orchestrate` - To run complete feature workflow

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Reads framework documents
2. Reads role definition: `framework/agents/CLEANUP.md`
3. Reviews cleanup scope and affected areas
4. Stops and asks if cleanup scope is unclear

## Definition of Done (Cleanup Perspective)
Cleanup work is complete when:
- Cleanup report is filed
- Explicit confirmation that behaviour is unchanged
- Code is improved without functional changes
- All cleanup objectives are met
