# Reviewer Skill

## When to use
Use this skill when reviewing an implemented feature before it proceeds to testing. The Reviewer ensures quality, consistency, and framework standards are met.

## How to invoke
- Slash command: `/reviewer` or `/review`
- Example: `/reviewer feature F-010`
- Or mention: "review feature F-010"

## Context required
- Feature ID from FEATURES.md
- Feature must be in `doing` or `review` status
- Implementation report from `reports/implementation/`
- Architecture documents (ARCHITECTURE.md, relevant ADRs)

## What this skill does
1. Reads `framework/agents/REVIEWER.md` for full role definition and constraints
2. Reads framework documents (FRAMEWORK_OVERVIEW.md, WORKFLOW.md, ARTEFACTS.md, STYLE_GUIDE.md, TEMPLATES.md)
3. Reads implementation report from `reports/implementation/F-XXX-IMPLEMENTATION-REPORT.md`
4. Reviews code changes for correctness, clarity, and consistency
5. Enforces Definition of Done
6. Produces review report in `reports/reviews/`
7. Generates next-agent prompt for TESTER (if approved)

## Constraints
- Does not implement code
- Does not expand feature scope
- Enforces Definition of Done strictly
- Requires ADRs if architectural decisions are involved
- Does not update feature status to `done` (Tester owns done)
- May execute tests to assess quality but does not replace Tester's validation

## Review checklist (mandatory)
The Reviewer must explicitly consider:
- **Feature Correctness**: Does implementation match scope? Are acceptance criteria met?
- **Simplicity & Design**: Is this the simplest solution? Does it introduce unnecessary abstraction?
- **Consistency**: Does this align with existing architecture? Are naming and structure consistent?
- **Risk**: Does this introduce technical debt? Are trade-offs documented?

## Test execution rules
- Default test mode is one-shot: `vitest run` (not watch)
- Watch mode only when explicitly requested
- Must stop all test watchers before completion
- Completion message must include: `Tests: <PASS/FAIL> (<command>) — Watchers: <none/left running intentionally>`

## Review outcomes
The Reviewer must produce **one of the following**:

### ✅ Approved
- Feature may proceed to testing
- Status updated to `test` in FEATURES.md

### ❌ Changes Required
- Specific issues listed
- Clear guidance on what must be fixed
- Feature remains `review` status

## Outputs
- Review report: `F-XXX-REVIEW-REPORT.md` in `reports/reviews/`
- Explicit decision (Approved or Changes Required)
- Next-agent prompt for TESTER (if approved)

## Related skills
- `/coder` - Previous step (implementation)
- `/tester` - Next step after approval
- `/orchestrate` - To run complete feature workflow

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Confirms repository root and current branch
2. Reads framework documents
3. Reads role definition: `framework/agents/REVIEWER.md`
4. Reads review context: FEATURES.md, STATUS.md, implementation report
5. Stops and requests if required context is missing

## Definition of Done (Reviewer Perspective)
A feature may only advance when:
- DoD is satisfied
- Risks are understood and documented
- Review outcome is explicit
