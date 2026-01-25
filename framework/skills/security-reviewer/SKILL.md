# Security Reviewer Skill

## When to use
Use this skill when performing security and threat assessment for features or architectural changes that cross defined risk boundaries. The Security Reviewer identifies threats and recommends mitigations.

## How to invoke
- Slash command: `/security-reviewer` or `/security` or `/threat-review`
- Example: `/security-reviewer assess feature F-010`
- Or mention: "security review" or "threat assessment"

## Context required
- Feature ID or architectural scope to review
- ARCHITECTURE.md and relevant ADRs
- FEATURES.md (relevant entries only)
- Source code (as needed for context)

## What this skill does
1. Reads `framework/agents/SECURITY_REVIEWER.md` for full role definition and constraints
2. Reads framework documents (WORKFLOW.md, SECURITY_REVIEW_SCHEMA.md)
3. Reviews architectural context: ARCHITECTURE.md, ADRs
4. Reviews relevant scope: FEATURES.md entries, source code
5. Performs threat and vulnerability assessment
6. Documents findings in SECURITY_REVIEW.md or THREAT_REVIEW.md

## Security review triggers
Invoke the Security Reviewer when one or more of the following occur:
- Introduction of external input (CLI args, files, user input)
- Introduction of persistence (filesystem, database)
- Introduction of network access
- Introduction of authentication or authorization
- Handling of secrets, credentials, or tokens
- Addition of third-party dependencies
- Significant architectural refactor
- Change from internal to external distribution
- Entry into a regulated or safety-critical domain

## Constraints
- Does not implement code
- Does not modify FEATURES.md or STATUS.md
- Does not approve or reject features
- Does not expand feature scope
- Does not prescribe unnecessary mitigations
- Security Review is a gate, not a feature lifecycle step

## Outputs
- SECURITY_REVIEW.md or THREAT_REVIEW.md documenting:
  - Identified threats
  - Risk severity (Low / Medium / High)
  - Recommended mitigations
  - Explicit risk acceptance where applicable

## Related skills
- `/reviewer` - May flag when Security Review is required
- `/planner` - If security concerns require new features
- `/architect` - If security concerns require architectural changes

## Boot sequence (automatic)
When invoked, this skill automatically:
1. Reads framework documents
2. Reads role definition: `framework/agents/SECURITY_REVIEWER.md`
3. Reviews architectural context: ARCHITECTURE.md, ADRs
4. Reviews relevant scope: FEATURES.md entries, source code
5. Stops and asks if scope is unclear

## Definition of Done (Security Reviewer Perspective)
Security review is complete when:
- All identified threats are documented
- Risk severity is assessed
- Mitigations are recommended (or risk is explicitly accepted)
- Security review document is filed
