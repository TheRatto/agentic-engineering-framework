# Workflow for Cursor 2.4

This document describes how to use the framework with Cursor 2.4's subagents and skills.

## Overview

Cursor 2.4 introduces **Skills** (discoverable agent capabilities) and **Subagents** (parallel execution). This framework adapts to leverage these features while maintaining strict role boundaries and artefact-driven state management.

## Feature Execution Modes

### Mode 1: Sequential (Recommended for Quality Gates)

Use skills sequentially to maintain strict role boundaries and quality gates.

**Example:**
```
1. /planner define features for user authentication
2. /coder feature F-010
3. /reviewer feature F-010
4. /tester feature F-010
5. /docs update docs for feature F-010
```

**When to use:**
- First-time feature implementation
- Features with dependencies
- When strict role boundaries are critical
- Quality gates (review, test) - always sequential

### Mode 2: Parallel Subagents (For Independent Tasks)

Use subagents when tasks can run in parallel without conflicts.

**Example: Feature with multiple independent components**
```
Main Agent: "Implement feature F-010 using subagents"
  ├─> Subagent 1: /coder (API endpoint)
  ├─> Subagent 2: /coder (UI component)
  └─> Subagent 3: /docs (Documentation)

Then sequential:
  → /reviewer (integration review)
  → /tester (end-to-end validation)
```

**When to use:**
- Multiple independent components can be built in parallel
- Tasks don't share mutable state
- Speed is more important than strict isolation
- Documentation can be updated alongside implementation

### Mode 3: Hybrid (Recommended for Complex Features)

Use subagents for parallel work, then sequential skills for quality gates.

**Example:**
```
1. Main agent spawns subagents for parallel implementation
   ├─> Subagent 1: /coder (Component A)
   └─> Subagent 2: /coder (Component B)

2. After implementation, use sequential /reviewer skill
   → /reviewer feature F-010

3. After review, use sequential /tester skill
   → /tester feature F-010

4. Conditional /docs skill
   → /docs update docs for feature F-010
```

**When to use:**
- Complex features with independent components
- When you want speed for implementation but control for quality gates
- Large features that benefit from parallelization

### Mode 4: Orchestrated (Recommended for Standard Workflow)

Use the orchestrator skill to handle the entire feature lifecycle automatically.

**Example:**
```
/orchestrate feature F-010
```

Or with parallelization:
```
/orchestrate feature F-010 --parallel
```

**When to use:**
- Standard feature execution
- When you want minimal manual intervention
- For consistent workflow execution

## When to Use Subagents vs Skills

### Use Subagents When:
- ✅ Multiple independent components can be built in parallel
- ✅ Tasks don't share mutable state
- ✅ Speed is more important than strict isolation
- ✅ Documentation can be updated alongside implementation
- ✅ You want to maximize parallelization

### Use Skills (Sequential) When:
- ✅ Quality gates (review, test) - **always sequential**
- ✅ Features with dependencies
- ✅ When strict role boundaries are critical
- ✅ First-time feature implementation
- ✅ When you need manual control over each step

## Workflow State Management

**Critical:** Subagents do NOT replace artefact-driven state management.

### State Rules:
1. **Feature status** still lives in `FEATURES.md`
2. **Reports** still go to `/reports/`
3. **State transitions** still follow `WORKFLOW.md` rules
4. **Subagents must update artefacts**, not just chat context
5. **All agents** (including subagents) must read framework documents

### Artefact Updates:
- Each subagent must file its own implementation report
- Main agent coordinates but doesn't replace individual reports
- Feature status updates follow WORKFLOW.md state machine
- All state is persisted in files, not chat history

## Quality Gate Rules

### Review Phase (Always Sequential)
- Review must happen after all implementation is complete
- Single reviewer validates integration of parallel work
- Review cannot be parallelized
- Review must wait for all implementation reports

### Test Phase (Always Sequential)
- Testing must happen after review approval
- Single tester validates end-to-end functionality
- Testing cannot be parallelized
- Test must wait for review approval

## Example Workflows

### Simple Feature (Sequential)
```
Feature: F-010 - Add user login form

1. /planner define feature F-010
2. /coder feature F-010
3. /reviewer feature F-010
4. /tester feature F-010
5. /docs update docs for feature F-010
```

### Complex Feature (Hybrid)
```
Feature: F-011 - User authentication system

Implementation (Parallel):
  ├─> Subagent 1: /coder (API endpoints)
  ├─> Subagent 2: /coder (UI forms)
  └─> Subagent 3: /docs (API documentation)

Quality Gates (Sequential):
  → /reviewer feature F-011 (integration review)
  → /tester feature F-011 (end-to-end validation)
```

### Orchestrated Feature
```
Feature: F-012 - Payment processing

/orchestrate feature F-012 --parallel

Orchestrator automatically:
1. Analyzes feature complexity
2. Spawns subagents for parallel implementation
3. Coordinates sequential review
4. Coordinates sequential testing
5. Updates documentation if needed
```

## Integration with Framework Rules

### WORKFLOW.md Still Applies
- Feature lifecycle states (todo, doing, review, test, done, blocked)
- State transition rules
- Definition of Done
- Mandatory workflow steps

### Role Definitions Still Apply
- Each skill references `framework/agents/{ROLE}.md`
- Role constraints are enforced
- Non-responsibilities are maintained
- Output formats follow TEMPLATES.md

### Artefact Requirements Still Apply
- Implementation reports in `/reports/implementation/`
- Review reports in `/reports/reviews/`
- Test reports in `/reports/tests/`
- Feature status in `FEATURES.md`

## Best Practices

1. **Start Sequential**: Use sequential skills for your first few features to understand the workflow
2. **Parallelize Implementation**: Use subagents for implementation when components are independent
3. **Keep Quality Gates Sequential**: Always use sequential skills for review and test
4. **Use Orchestrator**: For standard workflows, use `/orchestrate` to reduce manual overhead
5. **Maintain Artefacts**: Ensure all subagents file reports and update state
6. **Read Framework Docs**: All agents (including subagents) must read framework documents

## Troubleshooting

### Subagent Not Updating State
- Ensure subagent reads framework documents
- Verify subagent files reports in `/reports/`
- Check that subagent updates `FEATURES.md` status

### Parallel Work Conflicts
- Only parallelize truly independent components
- Use sequential mode if components share state
- Coordinate through artefacts, not chat

### Quality Gate Issues
- Always use sequential skills for review/test
- Wait for all implementation reports before review
- Ensure review approval before testing

## Migration from Manual Workflow

If you're currently using manual startup prompts:

1. **Try Skills First**: Replace startup prompts with skill invocations
   - `/coder feature F-010` instead of copying startup prompt
   
2. **Use Orchestrator**: For complete automation
   - `/orchestrate feature F-010` handles entire workflow

3. **Keep Manual Control**: Startup prompts still work if you need fine-grained control

See `MIGRATION_CURSOR_2.4.md` for detailed migration steps.
