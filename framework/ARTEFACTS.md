# Artefact Definitions

This document defines the **types of artefacts used by the framework**.
It specifies structure and ownership, not content.

---

## Core Artefacts (Always Present)

### PROJECT_BRIEF.md

**Purpose:** Single-page project orientation  
**Owner:** Planner  

**Required Sections:**
- Project goal
- Target users
- Non-goals
- Definition of success

---

### FEATURES.md

**Purpose:** Source of truth for all work  
**Owner:** Planner / Release Manager  

Each feature must include:
- Feature ID
- Title
- Status
- Scope (bullet points)
- Acceptance criteria
- Tests required
- Notes / links to related artefacts

---

### STATUS.md

**Purpose:** Shared situational awareness  
**Owner:** Release Manager / Reviewer  

Contains:
- Current focus
- Recently completed features
- Known risks and technical debt
- Upcoming decisions or milestones

---

## Planning & Design Artefacts

### PRD.md

**Purpose:** Problem framing and intent  
**Owner:** Planner  

Notes:
- Describes *what* and *why*
- Does not prescribe implementation details

---

### UI_SPEC.md

**Purpose:** UI behaviour and states  
**Owner:** Designer  

Includes:
- Screens or components
- States and transitions
- User-facing copy (if relevant)

Conforms to UI_SPEC_SCHEMA.md

---

### DESIGN_GUIDE.md

**Purpose:** Visual language and interaction style direction  
**Owner:** Designer

Includes:

- Visual positioning and design intent
- Color, typography, and spacing systems
- Differentiation rules and anti-generic constraints
- Platform-level design considerations

Conforms to DESIGN_GUIDE_SCHEMA.md

---

### UX_RATIONALE.md

**Purpose:** Decision traceability for UX/UI choices  
**Owner:** Designer

Includes:

- Design options considered
- Selected direction and trade-offs
- Research references and adaptation notes
- Validation and risk notes

Conforms to UX_RATIONALE_SCHEMA.md

---

### ARCHITECTURE.md

**Purpose:** High-level system structure  
**Owner:** Architect / Reviewer  

Includes:
- Major components
- Data flow
- Key constraints

Conforms to ARCHITECTURE_SCHEMA.md

---

## Decision Tracking

### ADRs (`/ADR/`)

**Purpose:** Record architectural decisions  
**Owner:** Architect / Reviewer  

Each ADR must include:
- Context
- Decision
- Consequences

---

## Documentation Artefacts

### CHANGELOG.md

**Purpose:** Track externally relevant changes  
**Owner:** Documentation Agent  

Includes:
- User-visible behaviour changes
- Configuration changes
- Breaking changes

---

## Execution Reports (`/reports/`)

All execution reports must be filed in the `/reports/` directory.

### Implementation Reports (`/reports/implementation/`)

**Purpose:** Document implementation details for a feature  
**Owner:** Coder  

Each implementation report must include:
- What was implemented
- Files changed
- Tests added or updated
- Notes for reviewer

Filename convention: `F-XXX-IMPLEMENTATION-REPORT.md`

### Review Reports (`/reports/reviews/`)

**Purpose:** Document review outcomes and feedback  
**Owner:** Reviewer  

Each review report must include:
- Decision (Approved or Changes required)
- Blocking issues (if any)
- Non-blocking notes
- DoD check results

Filename convention: `F-XXX-REVIEW-REPORT.md`

### Test Reports (`/reports/tests/`)

**Purpose:** Document test execution results  
**Owner:** Tester  

Each test report must include:
- Test scope
- Results (Pass / Fail)
- Issues found (if any)
- Notes

Filename convention: `F-XXX-TEST-REPORT.md`

---

## Usage Rule

Artefacts coordinate work.  
Chat history does not.

If information is important, it belongs in an artefact.
