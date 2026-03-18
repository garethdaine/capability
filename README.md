# Contract Clause Analysis — Capability Design (V1)

**Author**: Gareth Daine
**Date**: 18 March 2026
**Context**: No Code Sage — 4th Stage Interview (90-minute practical exercise)

---

## Overview

This repository contains the V1 capability design for a **Contract Clause Analysis** feature within an enterprise procurement client portal. The portal allows procurement teams to run guided workflows (capabilities) that produce structured, auditable results.

The design document covers the full system architecture — from user-facing workflow through to deployment strategy — for a capability where a user uploads a supplier contract, the system parses and analyses it via an external API, validates the results through a three-layer accuracy pipeline, and presents structured findings (missing clauses, unusual clauses, clauses requiring negotiation) that can be linked to procurement initiatives.

This is a **design and architecture exercise** — no implementation code. The document demonstrates how the system would be built to be practical, reliable for enterprise use, extensible for future capabilities, and appropriately scoped for V1.

---

## Deliverable

**[`docs/contract-clause-analysis-capability-design.md`](docs/contract-clause-analysis-capability-design.md)** — The primary design document (765 lines, 16 sections + appendix).

### Document Structure

| Section | Title | Description |
|---------|-------|-------------|
| 1 | Approach | Design philosophy and framing |
| 2 | V1 Tech Stack | Full stack overview, architecture diagram, Docling microservice, three-layer validation |
| 3 | Overall Workflow | Mermaid flowchart — happy path and all failure branches |
| 4 | User Experience Flow | Four-screen user journey |
| 5 | API Integration Design | Request/response payloads, validation rules |
| 6 | Data Model | Mermaid ERD (9 tables), design decision rationale |
| 7 | Processing Sequence | Mermaid sequence diagram — async flow with retries and LLM cross-check |
| 8 | Guardrails & Error Handling | File security, API resilience, result integrity, audit trail |
| 9 | Observability & Monitoring | Structured logging, key metrics, health checks, data retention, GDPR |
| 10 | Design Patterns & Engineering Standards | Architecture patterns, code conventions, engineering standards |
| 11 | Implementation Plan | Four-phase delivery (Foundation → Integration → Frontend → Hardening) |
| 12 | Testing, CI/CD & Deployment | Testing strategy, GitHub Actions pipeline, ECS deployment, rollback |
| 13 | V1 Simplifications | Eight deliberate scope cuts with future upgrade paths |
| 14 | Extensibility | Framework vs. capability-specific separation, capability registration |
| 15 | Key Technical Risks | Risk register with impact, likelihood, and mitigations |
| 16 | Summary | Explicit mapping to the four assignment criteria |
| Appendix A | Tools & Approach | Tooling and methodology used to produce this document |

### Tech Stack Summary

Next.js + React (TypeScript) frontend, Node.js + Fastify (TypeScript) backend, Docling (Python/FastAPI) for document parsing, PostgreSQL (AWS RDS), AWS-native infrastructure (Cognito, S3+KMS, SQS, ECS Fargate, Secrets Manager), ClamAV for virus scanning, Anthropic Claude API for LLM cross-checking. AWS CDK for infrastructure-as-code, GitHub Actions for CI/CD.

---

## Repository Contents

```
capability/
├── README.md                                          ← This file
└── docs/
    ├── contract-clause-analysis-capability-design.md   ← Primary deliverable
    ├── scratchpad.md                                   ← Session log — every decision and change tracked
    ├── brainstorm-prompt.md                            ← Prompt used for AgentOps review pass
    └── design-patterns-prompt.md                       ← Prompt used for design patterns section
```

---

## Design Process

The document was built iteratively within the 90-minute timebox using AI-assisted tooling (see Appendix A in the design document for full details):

1. **Scaffold** — Requirements clarification, STAR framing, initial 12-section draft
2. **Deepen** — Tech stack decisions, Docling and three-layer validation design, architecture diagram
3. **Review & Harden** — Independent brainstorm review (Claude CLI / AgentOps), fix inconsistencies, add Observability and GDPR sections
4. **Extend & Polish** — Testing/CI/CD, Design Patterns, Engineering Standards via targeted prompts, multiple verification passes

Every conversation turn is logged in [`docs/scratchpad.md`](docs/scratchpad.md), and every major change is captured in the git history.

---

## Git History

The commit log shows how the document evolved from initial draft to final version:

```
6294456 docs: add design patterns section prompt
9b7ef64 docs: add design patterns and engineering standards (Section 10)
d2b08ba docs: drop Vercel mention, keep frontend deployment AWS-native (S3 + CloudFront)
1936586 docs: add testing, CI/CD, and deployment strategy (Section 11)
cddf635 docs: refine sequence ordering, extensibility, GDPR, and UX badges
bd70580 fix: revert to British English throughout (organisational, analyse)
ec6470a fix: address review feedback — 2 critical, 2 moderate, 1 minor
39bc662 docs: fix inconsistencies and add observability section to capability design
cd2e9ee Add brainstorm prompt and update scratchpad
a6cc355 Add V1 tech stack section and remove time estimates
ce3aaba Add initial Contract Clause Analysis capability design
```

Run `git log --oneline` for the latest, or `git log` for full commit details with timestamps.
