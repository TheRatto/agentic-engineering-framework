# Coder Skill

## When to use
Use this skill when implementing a feature from FEATURES.md. The Coder implements exactly one feature according to its defined scope and acceptance criteria.

## How to invoke
- Slash command: `/coder` or `/code`
- Example: `/coder feature F-010`
- Or mention: "implement feature F-010"

## Context required
- Feature ID from FEATURES.md
- Feature must be in `todo` or `doing` status
- Architecture decisions (ADRs) must be available if needed
- PROJECT_BRIEF.md and PRD.md for project context

## What this skill does
1. Reads `framework/agents/CODER.md` for full role definition and constraints
2. Reads framework documents (FRAMEWORK_OVERVIEW.md, WORKFLOW.md, ARTEFACTS.md, STYLE_GUIDE.md, TEMPLATES.md)
3. Reads FEATURES.md to locate the assigned feature
4. Confirms feature scope, acceptance criteria, and test requirements
5. Implements the feature according to scope
6. Produces implementation report in `reports/implementation/`
7. Generates next-agent prompt for REVIEWER

## Constraints
- Implements exactly one feature
- Does not expand scope
- Does not refactor unrelated code
- Follows existing architecture and patterns
- Updates feature status from `todo` to `doing` when implementation begins
- Does not mark feature as `done` (Tester owns done status)

## Outputs
- Working code and tests
- Implementation report: `F-XXX-IMPLEMENTATION-REPORT.md` in `reports/implementation/`
- Next-agent prompt for REVIEWER (ready to paste)

## Test execution rules
- Default test mode is one-shot: `vitest run` (not watch)
- Watch mode only when explicitly requested
- Must stop all test watchers before completion
- Completion message must include: `Tests: <PASS/FAIL> (<command>) — Watchers: <none/left running intentionally>`

## Related skills
- `/reviewer` - Next step after implementation
- `/planner` - If feature needs re-scoping
- `/architect` - If architectural decisions are needed
- `/orchestrate` - To run complete feature workflow

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Confirms repository root and current branch
2. Reads framework documents
3. Reads role definition: `framework/agents/CODER.md`
4. Reads project state: FEATURES.md, STATUS.md
5. Locates feature and confirms scope, acceptance criteria, tests required
6. Stops and asks if anything is missing, ambiguous, or conflicts with role constraints

## Definition of Done (Coder Perspective)
The Coder's work is complete when:
- The feature behaves as specified
- Code builds/runs locally
- Required tests are present
- Implementation report is written and filed
- Next-agent prompt is generated

Final approval is **not** the Coder's responsibility.
