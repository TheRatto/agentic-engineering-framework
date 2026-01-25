# Migration Guide: Framework to Cursor 2.4

This guide helps you migrate from the manual startup prompt workflow to Cursor 2.4's skills and subagents.

## Overview

Cursor 2.4 introduces:
- **Skills**: Discoverable agent capabilities (invoke with `/skill-name`)
- **Subagents**: Parallel execution of independent tasks

The framework adapts to leverage these features while maintaining:
- Artefact-driven state management
- Strict role boundaries
- Quality gates (review/test remain sequential)

## Migration Steps

### Step 1: Verify Cursor Version

Ensure you're running Cursor 2.4 or later:
- Check Cursor version in About menu
- Skills and subagents require Cursor 2.4+

### Step 2: Skills Are Already Created

The framework now includes skills in `framework/skills/`:
- `coder/SKILL.md`
- `reviewer/SKILL.md`
- `tester/SKILL.md`
- `planner/SKILL.md`
- `architect/SKILL.md`
- `docs/SKILL.md`
- `security-reviewer/SKILL.md`
- `cleanup/SKILL.md`
- `orchestrator/SKILL.md`

These skills are automatically discoverable by Cursor.

### Step 3: Test Skills

Start with a simple feature to test skills:

**Before (Manual):**
```
1. Open framework/agents/AGENT_STARTUP_PROMPTS.md
2. Copy CODER startup prompt
3. Replace <FEATURE_ID> with F-010
4. Paste into Cursor chat
5. Wait for completion
6. Copy REVIEWER startup prompt
7. ... repeat
```

**After (Skills):**
```
1. /coder feature F-010
2. /reviewer feature F-010
3. /tester feature F-010
```

Or use orchestrator:
```
/orchestrate feature F-010
```

### Step 4: Understand Execution Modes

Read `WORKFLOW_CURSOR_2.4.md` to understand:
- When to use sequential skills
- When to use parallel subagents
- When to use orchestrator

### Step 5: Gradual Adoption

You don't need to migrate everything at once:

**Option A: Hybrid Approach**
- Use skills for new features
- Keep using startup prompts for complex manual control
- Gradually adopt orchestrator

**Option B: Full Migration**
- Use orchestrator for all features
- Fall back to individual skills if needed
- Use startup prompts only for edge cases

**Option C: Skills Only**
- Replace all startup prompts with skills
- Don't use subagents initially
- Add parallelization later

### Step 6: Update Team Documentation

If working in a team:
1. Share `WORKFLOW_CURSOR_2.4.md` with team
2. Update project-specific workflow docs
3. Document which mode your team prefers

## Migration Checklist

- [ ] Verify Cursor 2.4+ is installed
- [ ] Test `/coder` skill with a simple feature
- [ ] Test `/reviewer` skill
- [ ] Test `/tester` skill
- [ ] Read `WORKFLOW_CURSOR_2.4.md`
- [ ] Try `/orchestrate` for a complete feature
- [ ] Verify artefacts are still generated correctly
- [ ] Verify state updates in FEATURES.md
- [ ] Update team documentation (if applicable)

## Common Migration Patterns

### Pattern 1: Simple Feature (Sequential)

**Old:**
```
Copy CODER prompt → Paste → Wait
Copy REVIEWER prompt → Paste → Wait
Copy TESTER prompt → Paste → Wait
```

**New:**
```
/coder feature F-010
/reviewer feature F-010
/tester feature F-010
```

### Pattern 2: Complex Feature (Orchestrated)

**Old:**
```
Manually coordinate multiple agents
Track state in chat
Copy/paste prompts repeatedly
```

**New:**
```
/orchestrate feature F-010 --parallel
```

### Pattern 3: Parallel Implementation

**Old:**
```
Not possible - had to be sequential
```

**New:**
```
Main agent spawns subagents:
  ├─> Subagent 1: /coder (Component A)
  └─> Subagent 2: /coder (Component B)
Then: /reviewer feature F-010
```

## What Stays the Same

### Framework Structure
- Role definitions in `framework/agents/` still apply
- Skills reference these role definitions
- All constraints and rules remain

### Artefact-Driven State
- Feature status in `FEATURES.md`
- Reports in `/reports/`
- State transitions follow `WORKFLOW.md`
- No reliance on chat history

### Quality Gates
- Review and test remain sequential
- Definition of Done unchanged
- Quality standards maintained

### Role Boundaries
- Each agent has explicit responsibilities
- Non-responsibilities are enforced
- Role purity is maintained

## What Changes

### Invocation Method
- **Before**: Copy/paste startup prompts
- **After**: Invoke skills with `/skill-name` or use orchestrator

### Parallelization
- **Before**: Always sequential
- **After**: Can parallelize implementation (quality gates stay sequential)

### Automation
- **Before**: Manual coordination
- **After**: Orchestrator can handle complete workflow

### Discovery
- **Before**: Need to know exact prompt format
- **After**: Skills are discoverable via slash commands

## Troubleshooting Migration

### Skills Not Found
- Ensure Cursor 2.4+ is installed
- Check that `framework/skills/` directory exists
- Verify `SKILL.md` files are present
- Restart Cursor if needed

### State Not Updating
- Skills still update `FEATURES.md` and `/reports/`
- Verify artefact updates are happening
- Check that skills read framework documents

### Subagents Not Working
- Subagents require Cursor 2.4+
- Use orchestrator or manually spawn subagents
- Ensure subagents file reports

### Want Manual Control
- Startup prompts still work
- Use individual skills instead of orchestrator
- Mix and match as needed

## Rollback Plan

If you need to rollback:
1. Skills are additive - they don't break existing prompts
2. Startup prompts in `AGENT_STARTUP_PROMPTS.md` still work
3. You can use both approaches simultaneously
4. No changes to core framework structure

## Next Steps

1. **Read**: `WORKFLOW_CURSOR_2.4.md` for detailed workflow patterns
2. **Test**: Try skills with a simple feature
3. **Experiment**: Try orchestrator for automation
4. **Adopt**: Choose your preferred execution mode
5. **Share**: Update team documentation with your approach

## Support

- Framework docs: `framework/FRAMEWORK_OVERVIEW.md`
- Workflow: `framework/WORKFLOW.md` and `framework/WORKFLOW_CURSOR_2.4.md`
- Role definitions: `framework/agents/*.md`
- Skills: `framework/skills/*/SKILL.md`
