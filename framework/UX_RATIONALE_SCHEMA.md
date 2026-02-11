# UX_RATIONALE_SCHEMA.md

## Purpose

This document defines the structure for `UX_RATIONALE.md`.

`UX_RATIONALE.md` records why design decisions were made, what alternatives were
considered, and which evidence or references informed decisions.

---

## Entry Format

Each entry should correspond to one feature or one major design decision.

### Entry Header

- Feature ID or decision ID
- Date
- Author (Designer)

---

### Problem Context

- What user or business problem this design addresses
- Relevant constraints (platform, accessibility, technical)

---

### Design Directions Considered

List 2-3 directions and include:

- Short description
- Main strengths
- Main risks

---

### Selected Direction

- Which option was selected
- Why it was selected
- Why alternatives were rejected

---

### Usability and Accessibility Notes

- Expected usability outcomes
- Accessibility considerations and expected compliance
- Edge cases and failure states considered

---

### Contemporary References

When research is used, include:

- Source link
- Short note on relevance
- What was adapted (not copied)

---

### Validation Plan

- What should be tested (qualitative or quantitative)
- Acceptance signals
- Risks to monitor post-implementation

---

## Maintenance Rules

- Add a new entry when design direction materially changes
- Keep rationale consistent with `UI_SPEC.md` and `DESIGN_GUIDE.md`
- Do not include implementation code details
