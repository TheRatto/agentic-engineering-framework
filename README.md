# Agentic Engineering Framework

A structured, auditable framework for building software with AI coding agents.

This framework provides a disciplined approach to agent-assisted software development, focusing on **context control**, **decision traceability**, and **role separation** to avoid the common pitfalls of unstructured AI-assisted coding.

---

## Why this exists

AI coding agents are powerful, but without structure they tend to:

- Lose context between sessions
- Introduce scope creep
- Mix responsibilities (planning while coding, coding while reviewing)
- Make undocumented decisions
- Silently change project state

This framework applies proven software engineering practices — roles, artefacts, workflows, and decision records — to agentic development, making AI-assisted coding **predictable, reviewable, and scalable**.

---

## Core Principles

- **Explicit roles**  
  Planner, Architect, Coder, Reviewer, Tester, Docs, Security Reviewer — each with clear authority and constraints.

- **Artefact-driven workflow**  
  PRDs, FEATURES, ADRs, Architecture summaries, UI specs, changelogs — no hidden state.

- **Decision traceability**  
  Architectural decisions are captured once and never re-litigated.

- **Context containment**  
  Agents operate in narrow scopes to prevent drift and unintended changes.

- **Human-in-the-loop authority**  
  The framework supports AI acceleration without surrendering control.

---

## What's in this repository

- **`/framework/`**  
  The framework itself: workflows, artefact definitions, schemas, tooling rules, and Git discipline.

- **`/framework/agents/`**  
  Agent role definitions and startup prompts.

- **`/reports/`**  
  Execution reports (implementation, review, test) filed by agents.

- **Project files**  
  Template project files (FEATURES.md, STATUS.md, PROJECT_BRIEF.md, PRD.md, etc.) for projects using the framework.

This framework is **tool-agnostic** — it works with Cursor, ChatGPT, Claude, or any LLM that supports multi-agent workflows.

---

## Who this is for

- Developers using AI coding agents who want reliability
- Teams experimenting with agentic workflows
- Consultants and technical leaders evaluating AI-assisted development
- Anyone frustrated with "it worked yesterday, now it doesn't" AI coding sessions

---

## How to use it

1. Copy this template for a new project
2. Define your project: Create `PROJECT_BRIEF.md` and `PRD.md`
3. Use agent startup prompts from `framework/agents/AGENT_STARTUP_PROMPTS.md`
4. Follow the workflow: PLANNER → CODER → REVIEWER → TESTER
5. File reports in `/reports/` as work progresses

The framework is designed to be **adapted**, not blindly followed.

For detailed framework documentation, see:
- **`framework/FRAMEWORK_OVERVIEW.md`** — Core principles and philosophy
- **`framework/WORKFLOW.md`** — Mandatory workflow rules
- **`framework/ARTEFACTS.md`** — Artefact definitions
- **`framework/agents/AGENT_STARTUP_PROMPTS.md`** — Copy/paste prompts for each role

---

## Quick Start

### Prerequisites

Before using this framework, you must have:

- **PROJECT_BRIEF.md** — High-level project goals, target users, constraints, and definition of success
- **PRD.md** — Product requirements document describing what needs to be built and why

These documents are required because:
- The **PLANNER** agent uses them to define features with proper scope and acceptance criteria
- The framework assumes project intent is already established before feature development begins
- Agents reference these documents to ensure features align with project goals

### Starting a Feature

1. Open `framework/agents/AGENT_STARTUP_PROMPTS.md`
2. Copy the **CODER** startup prompt (if feature is defined) or **PLANNER** prompt (if feature needs definition)
3. Replace `<FEATURE_ID>` with your feature ID (e.g., `F-010`)
4. Paste into a new Cursor chat
5. The agent will output the next-agent prompt for you to copy/paste

See **`framework/WORKFLOW.md`** for the complete workflow.

---

## Status

This framework is actively evolving. Expect refinement, not churn.

---

## License

MIT
