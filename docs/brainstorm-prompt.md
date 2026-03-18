# Brainstorm Prompt: Contract Clause Analysis — Capability Design Review

You are reviewing a V1 capability design document for an enterprise procurement portal. The document is located at `docs/contract-clause-analysis-capability-design.md` — this is the ONLY file that should be updated as a result of this review.

IMPORTANT: We are NOT building this system. This is a design/architecture exercise for a time-boxed 90-minute interview assignment. The output is the design document itself — no code, no implementation. All suggestions should result in improvements to the document's clarity, completeness, and persuasiveness as a technical design artefact.

IMPORTANT: A scratchpad exists at `docs/scratchpad.md`. You MUST update the scratchpad as you work and after every turn. Log what you reviewed, what changes you made or recommended, and any open questions. This is non-negotiable.

## Task Context

The assignment asks: "Explain how you would build the first working version of a Contract Clause Analysis capability for an enterprise procurement client portal." The response must demonstrate it is practical to deliver, reliable for enterprise use, extensible for future capabilities, and simple enough not to over-engineer V1.

The capability workflow: a user uploads a supplier contract → the system parses it (Docling) → sends it to an external Contract Analysis API → validates and scores the response → displays findings (missing clauses, unusual clauses, clauses needing negotiation) → the user can link results to a procurement initiative.

Guardrails from the brief: API responses must be validated before display, results must be traceable and auditable, the system must handle failed/slow API responses safely, and uploads must be processed securely.

## What the document currently covers (13 sections)

1. Approach — framing and design philosophy
2. V1 Tech Stack — full stack overview with architecture diagram (Mermaid), Docling microservice detail, three-layer analysis accuracy (schema validation → confidence scoring → Anthropic Claude API cross-check)
3. Overall Workflow — Mermaid flowchart with happy path and failure branches
4. User Experience Flow — 4-screen journey (landing, upload, processing, results)
5. API Integration Design — request/response payloads, validation rules table
6. Data Model — Mermaid ERD with 9 tables (Capability, CapabilityRun, DocumentUpload, ApiRequest, CapabilityResult, Finding, Initiative, InitiativeResultLink, AuditLog) plus design decision rationale
7. Processing Sequence — Mermaid sequence diagram showing async flow with retries
8. Guardrails & Error Handling — file security, API resilience, result integrity, audit trail
9. Implementation Plan — 4 phases (Foundation, Integration, Frontend, Hardening)
10. V1 Simplifications — table of 8 deliberate scope cuts with future upgrade paths
11. Extensibility — framework vs. capability-specific separation, reuse story
12. Technical Risks — risk register with impact, likelihood, and mitigations
13. Summary

## Tech stack decisions

Next.js + React (TS) frontend, Node.js + Fastify (TS) backend, Docling (Python/FastAPI) for document parsing, AWS-native infrastructure (Cognito, S3+KMS, Secrets Manager, RDS PostgreSQL, SQS, ECS/EKS), ClamAV for virus scanning, Anthropic Claude API for LLM cross-checking.

## Your task

Review the document for gaps, weaknesses, or areas that could be strengthened. Consider whether the design convincingly addresses the assignment criteria. Look for missing concerns, unclear trade-offs, sections that could be tighter or more specific, and anything an experienced interviewer would probe on. Suggest concrete improvements — additions, restructuring, or rewrites — that should be applied to `docs/contract-clause-analysis-capability-design.md`.
