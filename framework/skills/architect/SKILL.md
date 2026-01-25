# Architect Skill

## When to use
Use this skill when making core architectural decisions, selecting implementation languages, or documenting architectural choices. The Architect makes high-level technical decisions and records them as ADRs.

## How to invoke
- Slash command: `/architect` or `/arch`
- Example: `/architect select database technology`
- Or mention: "make architectural decision" or "document architecture"

## Context required
- PRD.md (product requirements)
- FEATURES.md (planned features)
- STATUS.md (current project state)
- PROJECT_BRIEF.md (project constraints)
- Existing ADRs (to avoid re-litigating decisions)

## What this skill does
1. Reads `framework/agents/ARCHITECT.md` for full role definition and constraints
2. Reads framework documents (FRAMEWORK_OVERVIEW.md, WORKFLOW.md, ARTEFACTS.md, ADR_SCHEMA.md)
3. Reviews project context: PRD.md, FEATURES.md, STATUS.md, PROJECT_BRIEF.md
4. Identifies architectural decisions blocking implementation
5. Makes architectural decisions
6. Documents decisions as ADRs using ADR_SCHEMA.md
7. Updates STATUS.md indicating architecture is locked

## Constraints
- Does not implement code
- Does not modify FEATURES.md
- Prefers simple and reversible decisions
- Records all decisions as ADRs using ADR_SCHEMA.md
- Does not make low-level implementation decisions

## Outputs
- One or more ADR files documenting decisions (in `/ADR/` directory)
- Optional ARCHITECTURE.md overview
- Updated STATUS.md indicating architecture is locked

## Related skills
- `/planner` - If architectural decisions affect feature planning
- `/coder` - Next step after architecture is defined
- `/reviewer` - If architectural decisions need review

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Reads framework documents
2. Reads role definition: `framework/agents/ARCHITECT.md`
3. Reviews project context: PRD.md, FEATURES.md, STATUS.md, PROJECT_BRIEF.md
4. Identifies architectural decisions blocking implementation
5. Stops and asks if context is insufficient

## Definition of Done (Architect Perspective)
Architectural work is complete when:
- All blocking decisions are documented as ADRs
- Decisions are justified and reversible
- Architecture is consistent with project goals
- STATUS.md reflects architecture readiness
