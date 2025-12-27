# Agentic Engineering Framework

A structured, auditable framework for building software with AI coding agents.

This repository provides a disciplined approach to agent-assisted software development, focusing on **context control**, **decision traceability**, and **role separation** to avoid the common pitfalls of “vibe coding”.

---

## Why this exists

AI coding agents are powerful, but without structure they tend to:
- lose context
- introduce scope creep
- mix responsibilities
- make undocumented decisions
- silently change project state

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

## What’s in this repository

- `/framework/`  
  The framework itself: workflows, artefact definitions, schemas, tooling rules, and Git discipline.

- `/framework/agents/`  
  Agent role definitions and startup prompts.

- `/0. Project Template/`  
  A ready-to-copy project template for real-world use.

This repo is **tool-agnostic** — it works with Cursor, ChatGPT, Claude, or any LLM that supports multi-agent workflows.

---

## Who this is for

- Developers using AI coding agents who want reliability
- Teams experimenting with agentic workflows
- Consultants and technical leaders evaluating AI-assisted development
- Anyone frustrated with “it worked yesterday, now it doesn’t” AI coding sessions

---

## How to use it

1. Clone this repository
2. Copy `0. Project Template/` for a new project
3. Follow the framework workflow
4. Use agents deliberately, one role at a time

The framework is designed to be **adapted**, not blindly followed.

---

## Status

This framework is actively evolving.
Expect refinement, not churn.

---

## License

See LICENSE for details.
