# Tester Skill

## When to use
Use this skill when validating that an implemented feature behaves correctly and meets acceptance criteria. The Tester decides pass or fail.

## How to invoke
- Slash command: `/tester` or `/test`
- Example: `/tester feature F-010`
- Or mention: "test feature F-010"

## Context required
- Feature ID from FEATURES.md
- Feature must be in `test` status (after review approval)
- Implementation report from `reports/implementation/`
- Review report from `reports/reviews/` (if available)

## What this skill does
1. Reads `framework/agents/TESTER.md` for full role definition and constraints
2. Reads framework documents (FRAMEWORK_OVERVIEW.md, WORKFLOW.md, ARTEFACTS.md, STYLE_GUIDE.md, TEMPLATES.md)
3. Reads testing context: FEATURES.md, STATUS.md, implementation report
4. Validates feature behaviour against acceptance criteria
5. Executes required tests (manual or automated)
6. Identifies regressions or edge cases
7. Produces test report in `reports/tests/`
8. Updates feature status to `done` (if pass) or `doing` (if fail)

## Constraints
- Does not modify code
- Does not change feature scope
- Does not redesign tests
- Does not update documentation
- Does not approve architectural changes
- All issues are reported, not fixed

## Testing process
For each feature:
1. Review acceptance criteria
2. Run required tests
3. Perform basic exploratory validation
4. Check for obvious regressions

Testing depth should match the feature's importance and risk.

## Test execution rules
- Default test mode is one-shot: `vitest run` (not watch)
- Watch mode only when explicitly requested
- Must stop all test watchers before completion
- Completion message must include: `Tests: <PASS/FAIL> (<command>) — Watchers: <none/left running intentionally>`

## Test outcomes
### ✅ Pass
- Feature meets acceptance criteria
- No blocking issues found
- Feature status updated to `done` in FEATURES.md

### ❌ Fail
- Issues documented clearly
- Reproduction steps provided
- Expected vs actual behaviour described
- Feature status returned to `doing` in FEATURES.md

Failures must be concrete and actionable.

## Outputs
- Test report: `F-XXX-TEST-REPORT.md` in `reports/tests/`
- Explicit Pass or Fail outcome
- Feature status update in FEATURES.md

## Related skills
- `/reviewer` - Previous step (review)
- `/docs` - Next step (if documentation needed)
- `/orchestrate` - To run complete feature workflow

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Confirms repository root and current branch
2. Reads framework documents
3. Reads role definition: `framework/agents/TESTER.md`
4. Reads testing context: FEATURES.md, STATUS.md, implementation report
5. Stops and asks if acceptance criteria or test expectations are unclear

## Definition of Done (Tester Perspective)
Testing is complete when:
- Outcome is explicit (Pass or Fail)
- Results are clearly documented
- Issues (if any) are reproducible
- Feature state is updated correctly in FEATURES.md
