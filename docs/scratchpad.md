# Capability Assignment - Scratchpad

## Session Context
- **Date**: 2026-03-18
- **Assignment**: No Code Sage 4th stage interview - practical test
- **Timebox**: 90 minutes (due 5:30pm)
- **Deliverable**: Shareable markdown document

## Task Summary
Design the first working version of a "Contract Clause Analysis" capability for an enterprise procurement client portal. The portal runs guided workflows (capabilities) that help procurement teams complete tasks and produce structured results.

## Decisions Made
- **Format**: Markdown (.md)
- **Tone**: Balanced hybrid — product thinking backed by technical depth
- **Diagrams**: Mermaid (workflow, data model, sequence)
- **Frontend**: Next.js + React (TypeScript)
- **Backend**: Node.js + Fastify (TypeScript)
- **Parsing**: Docling (Python/FastAPI microservice)
- **Security/Infra**: AWS-native (Cognito, S3+KMS, Secrets Manager)
- **Analysis Accuracy**: Schema validation + confidence scoring + LLM cross-check (Anthropic Claude API)
- **Database**: PostgreSQL (AWS RDS)

## Key Requirements from Brief
1. Practical to deliver
2. Reliable enough for enterprise use
3. Extensible enough for future capabilities
4. Simple enough — don't over-engineer V1

## Guardrails (from brief)
- API responses must be validated before being shown to users
- Capability results must be traceable and auditable
- System must handle failed or slow API responses safely
- User uploads must be processed securely

## Approach — STAR
- **SITUATION**: Enterprise procurement portal needs its first capability. Contract Clause Analysis uses an external API. Must be production-quality but V1-scoped.
- **TASK**: Design the end-to-end workflow, data model, API integration, error handling, and implementation plan. Show it's extensible without over-engineering.
- **ACTION**: Produce a structured design doc with workflow diagrams, data model, API contract, guardrails, implementation phases, and deliberate V1 simplifications.
- **RESULT**: A polished markdown doc Gareth can share as his interview submission.

## Conversation Log

### Turn 1
- Gareth provided the assignment brief
- Clarifying questions asked: format (markdown), tone (balanced hybrid), diagrams (yes, Mermaid)
- Built full deliverable: `contract-clause-analysis-capability-design.md`
- Sections: Approach, Workflow (Mermaid flowchart), UX Flow (4 screens), API Integration (request/response/validation), Data Model (Mermaid ERD with 9 tables), Sequence Diagram, Guardrails, Implementation Plan (4 phases/4 weeks), V1 Simplifications table, Extensibility, Risks & Mitigations, Summary
- Status: Draft complete, ready for Gareth's review

### Turn 2
- Gareth asked to commit initial pass (no push)
- Attempted to init git in wrong folder (`/mnt/nocodesage/`) — Gareth already had a repo in `./capability`
- Removed errant `.git` folder from working directory
- Hit SSH auth issues, lock file issues — resolved

### Turn 3
- Committed initial draft as `ce3aaba` on `main` in `./capability`
- Git config: name "Gareth Daine", email `1745959+garethdaine@users.noreply.github.com`
- Gareth pushed from local terminal

### Turn 4
- Removed week/time estimates from implementation plan (Phase 1-4 headings) and summary
- Kept phased structure intact, just stripped timeframes
- Lesson: Gareth flagged we weren't updating scratchpad each turn — now caught up

### Turn 5
- Added V1 Tech Stack section (new Section 2) to design doc
- Decisions made via AskUserQuestion:
  - **Frontend**: Next.js + React (TypeScript)
  - **Backend**: Node.js + Fastify (TypeScript)
  - **Parsing**: Docling (Python/FastAPI microservice) — IBM open-source, strong layout/table extraction
  - **Security**: AWS-native (Cognito, S3+KMS, Secrets Manager, WAF)
  - **Accuracy**: Three-layer validation — schema check → confidence scoring → Anthropic Claude API cross-check on low-confidence findings
  - **Docling integration**: Standalone Python microservice called via HTTP from the Node.js backend
- Added architecture diagram (Mermaid flowchart) showing all services and connections
- Renumbered all sections (2→3 through 12→13) and fixed internal cross-references
- Document now has 13 sections

### Turn 6
- Committed tech stack changes as `a6cc355` — push failed (SSH), Gareth pushed locally

### Turn 7
- Created `docs/brainstorm-prompt.md` for AgentOps brainstorming command
- Prompt covers: what's been done, task context, tech stack, all 13 sections
- Includes IMPORTANT notes: only update the design doc, this is architecture not implementation, must update scratchpad every turn

### Turn 8 — Brainstorming Review Session (10-min rapid pass)
- Ran design doc review via `/agentops:enterprise:brainstorm`
- **4 inconsistency fixes**: Workflow diagram now shows Docling step, sequence diagram includes Docling + Claude + three-layer validation, FINDING table has confidence_score + verification_status, API request payload clarified as parsed content
- **New Section 9**: Observability & Monitoring — structured logging, 6 key metrics with alert thresholds, health checks, data retention policy
- **Summary rewritten** (Section 14): Now explicitly maps to the 4 assignment criteria (practical, reliable, extensible, simple)
- **Implementation plan updated**: Added LLM cross-check service (Phase 2), observability setup (Phase 4), updated data model task
- Sections renumbered 10-13 → 11-14
- Document now has 14 sections

### Turn 9 — Review feedback fixes (5 issues)
- **CRITICAL fix 1**: Reordered Section 3 workflow diagram — validation/scoring now happens after API response, not before. Added ClamAV scan step with infected-file branch to error state.
- **CRITICAL fix 2**: Added ClamAV virus scan step to Section 7 sequence diagram after file upload, with audit log entry and 422 rejection on detection.
- **MODERATE fix 1**: Committed to AWS SQS (removed "or BullMQ (Redis)" ambiguity) in Section 2.1 tech stack table.
- **MODERATE fix 2**: Aligned endpoint spelling — `POST /analyse` → `POST /analyze` (American English, matching capability name).
- **MINOR fix**: `organisational` → `organizational` in API response example (line 205).

### Turn 10 — British English correction
- Reverted American English changes from Turn 9: `organizational` → `organisational`, `/analyze` → `/analyse`
- Document convention: British English throughout

### Turn 12 — Four targeted refinements
1. **Sequence diagram ordering** (Section 7): Swapped lines — API_REQUEST now created before the external API call, ensuring trace exists even if the call crashes
2. **Capability registration** (Section 12): Added paragraph explaining database-seeded registration with slug-based routing
3. **GDPR/data residency** (Section 9): Added subsection on single-region deployment, data residency, and GDPR right-to-deletion with audit log redaction approach
4. **Verification badges in UX** (Section 4, Screen 4): Added "Verified"/"Under Review" badge description with cross-reference to Section 2.4

### Turn 18 — Design Patterns & Engineering Standards prompt
- Gareth requested new section covering design patterns and engineering standards
- Decisions: full engineering standards scope (architecture patterns + code conventions + standards), placed before Implementation Plan (Section 10)
- Created copyable plugin prompt covering: adapter/repository/state machine/validation pipeline/circuit breaker/event-driven audit patterns, code conventions (project structure, naming, error handling, logging, API envelope), engineering standards (API versioning, code review, dependency management, documentation, feature flags)
- Saved to `docs/design-patterns-prompt.md`
- Plugin will insert as Section 10, renumber 10→11 through 15→16, fix all cross-references

### Turn 17 — Final re-review after Gareth's 4 amendments
- Confirmed all 4 fixes applied correctly:
  1. Sequence diagram: API_REQUEST now created before external API call (line 388-389)
  2. Capability registration: database-seeded with slug routing added to Section 13 (line 621)
  3. GDPR/data residency: subsection added to Section 9 (lines 469-470)
  4. Verification badges: Screen 4 description updated with cross-ref to Section 2.4 (line 152)
- Section numbering 1-15: correct
- All cross-references verified: Section 2.4, 4, 6, 10, 12 — all correct
- Summary (Section 15) references Section 12: correct
- British English: consistent throughout
- Vercel mention: removed (S3 + CloudFront only, line 564)
- **Status: Document complete. No issues. Ready to submit.**

### Turn 15 — Re-review after Testing/CI/CD/Deployment added
- Full re-read of document (653 lines, 15 sections)
- New Section 11 verified: testing strategy, CI/CD pipeline, deployment, V1 simplifications — all consistent with tech stack
- Section numbering 1-15: correct
- Summary cross-reference to "Section 12": correct
- British English: maintained
- Tech choices aligned: Jest/pytest/Playwright/GitHub Actions/ECR/ECS/CDK all match Section 2
- Three-layer validation testing maps correctly to Section 2.4
- ~~One minor observation: Vercel mentioned alongside AWS-native stack (line 564)~~ — resolved Turn 16
- Status: Document complete. No issues remaining.

### Turn 16 — Drop Vercel mention
- Replaced "deploys to Vercel (or as a static export to S3 + CloudFront)" with "deploys as a static export to S3 + CloudFront" to keep the stack consistently AWS-native

### Turn 18 — Design Patterns & Engineering Standards section added
- Added new Section 10 with three subsections:
  - **10.1 Architecture Patterns**: Adapter (API wrappers), Repository (data access), State machine (run lifecycle), Validation pipeline (composable three-layer chain), Circuit breaker (opossum), Event-driven audit logging (queue-based)
  - **10.2 Code Conventions**: Monorepo structure (3 packages + infra), naming conventions (kebab-case files, snake_case DB, PascalCase types), typed error classes with error codes, JSON structured logging format (5 mandatory fields), API response envelope (success/error shapes)
  - **10.3 Engineering Standards**: URL path API versioning, PR/code review expectations, dependency management (Renovate, lockfiles, audit in CI), documentation standards (OpenAPI, migration comments, lightweight ADRs), database-driven feature flags tied to capability registration
- Renumbered sections 10-15 → 11-16, subsections 11.x → 12.x
- Fixed cross-references: "Section 10, Phase 4" → "Section 11, Phase 4", "Section 12" → "Section 13" in Summary, "Section 13" → "Section 14" for extensibility, "Section 14" → "Section 15" for risks
- Document now has 16 sections

### Turn 13 — Testing/CI/CD/Deployment prompt
- Created copyable prompt for Claude plugin to add testing, CI/CD, and deployment strategy section
- Covers: unit/integration/e2e testing, CI/CD pipeline, deployment strategy, V1 simplifications
- Instructs plugin to insert after Section 10, renumber subsequent sections, fix cross-references
- British English, match existing doc tone

### Turn 14 — Testing, CI/CD & Deployment section added
- Added new Section 11 with four subsections:
  - **11.1 Testing Strategy**: Unit (Jest/pytest), integration (real Postgres, mocked HTTP APIs, Docling contract tests), E2E (Playwright, 5 key flows), three-layer validation testing approach, V1 test scope cuts
  - **11.2 CI/CD Pipeline**: GitHub Actions, 5 stages (lint→test→integration→build→deploy), trunk-based branching, migration handling, ECR container registry
  - **11.3 Deployment Strategy**: AWS CDK (TypeScript), independent ECS service deployment, rolling updates for zero-downtime, Secrets Manager injection, rollback via ECS task definition revert
  - **11.4 V1 Simplifications**: 6-row table of deferred testing/deployment enhancements
- Renumbered sections 11-14 → 12-15
- Fixed Summary cross-reference: "Section 11" → "Section 12"
- Document now has 15 sections

### Turn 11 — Final review before manual review
- Re-read full document (578 lines, 14 sections)
- **All 5 previous issues confirmed resolved**: workflow logic, ClamAV in sequence, SQS commitment, British English consistent
- **AgentOps additions verified**: Section 9 (Observability), rewritten Summary (Section 14), updated sequence diagram with Docling + Claude participants, implementation plan updated
- **Structural integrity**: 14 sections sequential, all cross-references correct, 3 Mermaid diagrams internally consistent, data model aligned with accuracy layer
- **4 minor observations flagged for Gareth's manual review** (non-blocking):
  1. Sequence diagram: API_REQUEST created after sending to API (should arguably be before)
  2. Section 12 (Extensibility): no mention of how new capabilities get registered
  3. No GDPR/data residency mention despite handling supplier contracts
  4. "Verified"/"Under Review" badges described in Section 2.4 but not in Screen 4 UX description
- Status: Document is interview-ready. Gareth doing manual review.
