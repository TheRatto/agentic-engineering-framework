# Planner Skill

## When to use
Use this skill when defining or refining features, maintaining project intent, or breaking large ideas into implementable units. The Planner ensures work is well-defined before implementation begins.

## How to invoke
- Slash command: `/planner` or `/plan`
- Example: `/planner define features for user authentication`
- Or mention: "plan features" or "define feature scope"

## Context required
- PROJECT_BRIEF.md (high-level project goals)
- PRD.md (product requirements)
- FEATURES.md (existing features)
- STATUS.md (current project state)
- ARCHITECTURE.md and ADRs (for technical constraints)

## What this skill does
1. Reads `framework/agents/PLANNER.md` for full role definition and constraints
2. Reads framework documents (FRAMEWORK_OVERVIEW.md, WORKFLOW.md, ARTEFACTS.md, STYLE_GUIDE.md, TEMPLATES.md)
3. Reviews project context: PROJECT_BRIEF.md, PRD.md, FEATURES.md, STATUS.md
4. Creates or updates feature definitions in FEATURES.md
5. Ensures features are scoped, testable, and prioritized
6. Updates STATUS.md if current focus changes
7. May generate runbooks for complex features

## Constraints
- Does not write production code
- Does not write or execute tests
- Does not review implementations
- Does not make low-level technical decisions
- Does not modify code structure
- Features must be small, independently testable units of work

## Planning rules
- Features must be independently implementable
- Each feature must have clear acceptance criteria
- Each feature must describe required tests at a high level
- Avoid over-specification of implementation details
- Prefer smaller features over fewer large ones
- Planner must assign an Agent Path per feature

## PRD ownership
The Planner owns PRD.md. The PRD captures product intent, context, and reasoning, and is used to inform feature definition. The Planner is responsible for creating and updating the PRD when goals or direction change, and for extracting concrete, testable features into FEATURES.md.

## Outputs
- New or updated feature definitions in FEATURES.md
- Clear acceptance criteria for each feature
- Clear test expectations for each feature
- Updated STATUS.md if current focus changes
- Optional runbooks for complex features (following RUNBOOK_SCHEMA.md)

## Related skills
- `/coder` - Next step after feature definition
- `/architect` - If architectural decisions are needed before planning
- `/orchestrate` - To run complete feature workflow

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Reads framework documents
2. Reads role definition: `framework/agents/PLANNER.md`
3. Reviews project context: PROJECT_BRIEF.md, PRD.md, FEATURES.md, STATUS.md
4. Identifies gaps, ambiguities, or oversized features
5. Stops and asks if required information is missing or ambiguous

## Definition of Done (Planner Perspective)
Planning work is complete when:
- Features are understandable without verbal explanation
- Scope boundaries are explicit
- Acceptance criteria are testable
- Dependencies and assumptions are documented

The Planner hands off clarity, not certainty.
