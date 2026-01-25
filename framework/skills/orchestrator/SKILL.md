# Feature Orchestrator Skill

## When to use
Use this skill to execute a complete feature through the workflow, automatically coordinating agents and subagents. The Orchestrator reduces manual overhead by managing the entire feature lifecycle.

## How to invoke
- Slash command: `/orchestrate` or `/run-feature` or `/orchestrate-feature`
- Example: `/orchestrate feature F-010`
- Example with parallel: `/orchestrate feature F-010 --parallel`
- Or mention: "run feature F-010" or "orchestrate feature F-010"

## Context required
- Feature ID from FEATURES.md
- Feature must be defined with clear scope and acceptance criteria
- Architecture decisions (ADRs) must be available if needed

## What this skill does

### 1. Analysis Phase (main agent)
- Reads FEATURES.md to locate the feature
- Determines feature complexity
- Identifies parallelization opportunities
- Creates execution plan
- Determines if feature has independent components

### 2. Implementation Phase
**Simple Feature (Sequential):**
- Invokes `/coder` skill
- Waits for implementation completion

**Complex Feature (Parallel Subagents):**
- Spawns subagents for independent components
- Each subagent uses `/coder` skill
- Coordinates implementation completion
- Ensures all implementation reports are filed

### 3. Review Phase (always sequential)
- Invokes `/reviewer` skill
- Waits for approval before proceeding
- If changes required, returns to implementation phase

### 4. Test Phase (always sequential)
- Invokes `/tester` skill
- Validates feature completion
- If tests fail, returns to implementation phase

### 5. Documentation Phase (conditional)
- If documentation needed, spawns `/docs` subagent
- Can run in parallel with next feature if appropriate
- Otherwise runs sequentially after testing

## Execution modes

### Mode 1: Sequential (default)
```
Main Agent → /coder → /reviewer → /tester → /docs (if needed)
```

### Mode 2: Parallel (with --parallel flag)
For features with independent components:
```
Main Agent
  ├─> Subagent 1: /coder (Component A)
  ├─> Subagent 2: /coder (Component B)
  └─> Subagent 3: /docs (Documentation)
  
Then sequential:
  → /reviewer (integration review)
  → /tester (end-to-end validation)
```

## State management
- All state updates go to FEATURES.md
- All reports go to `/reports/`
- Orchestrator tracks progress but doesn't modify feature status directly
- Each agent skill updates status according to WORKFLOW.md
- Artefact-driven state is maintained throughout

## Constraints
- Never skip quality gates (review/test)
- Always maintain artefact-driven state
- Subagents must produce reports, not just code
- Quality gates (review/test) are always sequential
- Implementation can be parallelized if components are independent

## Outputs
- Complete feature execution through workflow
- All required reports filed in `/reports/`
- Feature status updated in FEATURES.md
- Execution summary with outcomes

## Related skills
- Individual agent skills can be used for manual control
- `/planner` - If feature needs definition first
- `/architect` - If architectural decisions are needed

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Reads FEATURES.md to locate feature
2. Reads WORKFLOW.md to understand workflow rules
3. Analyzes feature complexity
4. Creates execution plan
5. Begins execution

## Definition of Done (Orchestrator Perspective)
Orchestration is complete when:
- Feature status is `done` in FEATURES.md
- All required reports are filed
- All quality gates have passed
- Documentation is updated if needed

## Error handling
- If any phase fails, orchestrator reports the issue
- Returns control to user with clear next steps
- Maintains state in FEATURES.md
- Does not attempt to fix issues automatically
