# Workflow Rules

This document defines the **mandatory, project-agnostic workflow**
for all agent-driven development using this framework.

---

## Feature Lifecycle States

Each feature must exist in exactly one of the following states:

1. `todo` – Defined but not started
2. `doing` – Being implemented by a Coder
3. `review` – Awaiting Reviewer feedback
4. `test` – Under validation by Tester
5. `done` – Meets Definition of Done
6. `blocked` – Cannot progress (reason documented)

State transitions must be explicitly updated in `FEATURES.md`.

---

## Feature Status Transitions

The following rules govern feature state changes. Each transition has a single owner.

| State    | Set by    | When |
|----------|-----------|------|
| `todo`   | Planner   | When creating or (re)opening a feature |
| `doing`  | Coder     | When implementation starts |
| `review` | Coder     | When implementation is complete and implementation report is filed |
| `test`   | Reviewer  | When review is Approved (handoff to Tester) |
| `done`   | Tester    | When validation Pass |
| `doing`  | Tester    | When validation Fail (with documented issues) |
| `blocked`| Any       | When the feature cannot progress (reason documented) |

- Planner creates features in `todo` only.
- Coder moves `todo` → `doing` at start; `doing` → `review` when implementation is complete (report filed).
- Reviewer moves `review` → `test` when Approved; does not change status when Changes required.
- Tester moves `test` → `done` on Pass; `test` → `doing` on Fail.

This ensures clear ownership of progress and prevents premature completion.

---

## Mandatory Feature Flow (Full Path)

For every feature with **Path: full** (the default):

1. Planner defines or updates the feature (if required), and sets Path (and optionally Batch)
2. Designer defines UX/UI direction for UI-impacting features (required unless explicitly waived)
3. Coder implements **one feature only** (or a Batch when set) and files implementation report(s) in `reports/implementation/`
4. Coder moves feature status to `review` when implementation is complete
5. Reviewer approves or rejects the implementation and files review report in `reports/reviews/`; on Approved, moves status to `test`
6. Tester validates behaviour and files test report in `reports/tests/`; on Pass, moves status to `done`
7. Documentation is updated **if required**

Skipping steps is not permitted for full-path features.

---

## Lightweight Path (Exception)

When Planner sets **Path: lightweight** for a feature:

- The feature is small, low-risk, and well-scoped (e.g. config change, single function, copy change; no new dependencies, UI, auth, or security impact).
- Coder may move the feature from `doing` to `done` when **lightweight DoD** is met: acceptance criteria met, required tests run and passing, no new TODOs, no architecture change.
- No separate Reviewer or Tester sessions. Reviewer and Tester are not invoked for that feature.
- Coder still produces an implementation report and follows all other Coder constraints.
- Only Planner may set Path: lightweight; Coder must not self-assign lightweight.

---

## Batching

When Planner sets **Batch** on a feature (optional list of feature IDs, e.g. F-011, F-012):

- Coder may implement all features in the batch in one session, in the order given.
- Each feature in the batch must have its own implementation report (or one report with a clear section per feature).
- Status transitions apply per feature: Coder moves each to `review` when that feature is complete (full path), or to `done` when lightweight DoD is met (lightweight path).
- Batch is only for features that are all `todo` and suitable to implement together (e.g. all lightweight, or one logical unit). Quality gates (Reviewer, Tester) remain per feature for full-path batched features.

---

## UI Design Gate (Required Unless Waived)

For UI-impacting features, the Designer step is mandatory unless explicitly waived.

UI-impacting features include:

- new screens, dialogs, or major layout changes
- non-trivial interaction flows
- significant visual style direction changes
- new interaction states, validation, or accessibility constraints

Required Designer outputs:

- `UI_SPEC.md` updates
- `DESIGN_GUIDE.md` updates (or confirmation of no change)
- `UX_RATIONALE.md` entry

Waiver rules:

- Waiver must be explicitly documented in `FEATURES.md` notes
- Waiver reason must be project-valid (e.g., backend-only feature, no UI effect)
- Reviewer must verify waiver legitimacy during review

---

---

## Security & Threat Review Gate (Conditional)

A Security Review is required **only** when a feature or architectural change
crosses a defined risk boundary.

### Security Review Triggers

Invoke the Security Reviewer when one or more of the following occur:

- Introduction of external input (CLI args, files, user input)
- Introduction of persistence (filesystem, database)
- Introduction of network access
- Introduction of authentication or authorisation
- Handling of secrets, credentials, or tokens
- Addition of third-party dependencies
- Significant architectural refactor
- Change from internal to external distribution
- Entry into a regulated or safety-critical domain

### Workflow Integration

- The Reviewer must flag when a Security Review is required
- The Security Reviewer performs threat and vulnerability assessment
- Security Review outputs are documented (e.g. SECURITY_REVIEW.md)
- The Security Reviewer does **not** approve or reject features
- Identified mitigations may result in new follow-up features

Security Review is a **gate**, not a feature lifecycle step.

---

## Project-Level Coordination

- STATUS.md is updated by the role that introduces or resolves a **project-level** change in focus, risk, or readiness
- Feature-level progress belongs exclusively in FEATURES.md
- Tool usage must follow MCP_TOOLING_GUIDE.md.

---

## Definition of Done (DoD)

A feature may only be marked `done` if **all** of the following are true:

- Acceptance criteria are met
- Required tests pass (or an explicit waiver is documented)
- No unexplained TODOs are introduced
- Architecture remains consistent with existing patterns
- Documentation is updated if behaviour or configuration changed
- Feature state is correctly updated in `FEATURES.md`

The **Reviewer** is accountable for enforcing the DoD.

---

## Cleanup & Refactoring

- Cleanup is **scheduled**, not opportunistic
- Cleanup agents run:
  - On cadence (e.g. every N features), or
  - When the Reviewer flags structural debt
- Cleanup must not introduce new features or scope changes

---

## Release Discipline

- Only `done` features may be released
- Release state must be explicit
- Experimental or partial features must be clearly flagged

---

## Execution Aids

Runbooks and helper files may be used to reduce execution friction.

- **FEATURE_RUNNER.md** may be used as a convenience checklist for stepping through a feature.
- These aids do not replace the mandatory workflow defined in this document.
- Authority and state transitions remain governed by role definitions and artefacts.

---

## Cursor 2.4 Subagent Integration

### Subagent Rules

1. **Quality Gates Remain Sequential**
   - Review and Test phases MUST be sequential
   - No parallel review or testing of the same feature
   - Single reviewer validates integration of parallel work
   - Single tester validates end-to-end functionality

2. **Implementation Can Be Parallel**
   - Multiple independent components can be implemented via subagents
   - Each subagent must produce its own implementation report
   - Main agent coordinates integration
   - Subagents must not share mutable state

3. **State Updates**
   - Subagents update FEATURES.md status according to workflow rules
   - Each subagent files reports in `/reports/`
   - Main agent ensures consistency
   - All state is artefact-driven, not chat-based

4. **Artefact Requirements**
   - Subagents must read framework documents
   - Subagents must follow role definitions in `framework/agents/`
   - Subagents must produce required outputs per TEMPLATES.md
   - Subagents must update FEATURES.md status correctly

### Example: Parallel Implementation

**Feature F-010: User Authentication**
- Component A: API endpoints (subagent 1)
- Component B: UI forms (subagent 2)
- Component C: Documentation (subagent 3)

**Execution:**
1. Main agent spawns 3 subagents with `/coder` skill
2. Each subagent implements its component
3. Each subagent files implementation report in `/reports/implementation/`
4. Main agent coordinates integration
5. Sequential `/reviewer` skill reviews integration
6. Sequential `/tester` skill validates end-to-end

**State Management:**
- Feature status updated in FEATURES.md by each subagent
- All reports filed in `/reports/`
- Review and test phases update status sequentially
- Final status is `done` only after all phases complete

### When to Use Subagents

**Use Subagents When:**
- Feature has multiple independent components
- Components don't share mutable state
- Speed is more important than strict isolation
- Documentation can be updated alongside implementation

**Use Sequential Skills When:**
- Quality gates (review, test) - always sequential
- Features with dependencies between components
- First implementation of a feature type
- When strict role boundaries are critical

### Skills vs Manual Prompts

The framework supports both:
- **Skills**: Invoke with `/coder feature F-010` (Cursor 2.4+)
- **Manual Prompts**: Copy/paste from AGENT_STARTUP_PROMPTS.md

Both approaches follow the same workflow rules and produce the same artefacts.

See `WORKFLOW_CURSOR_2.4.md` for detailed workflow patterns with skills and subagents.