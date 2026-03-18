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
