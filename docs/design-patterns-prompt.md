# Plugin Prompt: Design Patterns & Engineering Standards

You are adding a Design Patterns & Engineering Standards section to an existing V1 capability design document for an enterprise procurement portal. The document is located at `docs/contract-clause-analysis-capability-design.md` — this is the ONLY file that should be updated.

IMPORTANT: We are NOT building this system. This is a design/architecture exercise. All additions should describe the patterns, standards, and conventions — no code implementations. No code blocks except short illustrative pseudocode where it genuinely clarifies a pattern.

IMPORTANT: A scratchpad exists at `docs/scratchpad.md`. You MUST update the scratchpad as you work and after every turn. Log what you reviewed, what changes you made, and any open questions. This is non-negotiable.

## Placement

Insert the new section as Section 10 — immediately before the current Section 10 (Implementation Plan). Renumber all subsequent sections (current 10→11, 11→12, 12→13, 13→14, 14→15, 15→16). Fix ALL internal cross-references throughout the document — search for every occurrence of "Section X" and update accordingly. The Summary section currently references "Section 12" for V1 simplifications — this will need updating.

## Current Tech Stack (for context)

- Frontend: Next.js + React (TypeScript)
- Backend: Node.js + Fastify (TypeScript)
- Document Parsing: Docling (Python/FastAPI microservice)
- Database: PostgreSQL (AWS RDS)
- File Storage: AWS S3 + KMS
- Job Queue: AWS SQS
- Auth: AWS Cognito
- Infrastructure: AWS ECS Fargate or EKS, AWS CDK (TypeScript)
- External APIs: Contract Analysis API, Anthropic Claude API
- Virus Scanning: ClamAV (containerised)
- CI/CD: GitHub Actions, Amazon ECR
- Testing: Jest, pytest, Playwright

## What to add

The section should cover three areas: architecture patterns, code conventions, and engineering standards.

### Architecture Patterns
Make explicit the patterns already implied by the document:
- **Adapter pattern** — wrapping the external Contract Analysis API and Anthropic Claude API behind typed interfaces, enabling swap-out without touching business logic (referenced in Section 14, vendor lock-in risk)
- **Repository pattern** — data access abstraction over PostgreSQL for capability runs, findings, audit logs
- **State machine** — the capability run lifecycle (created → processing → completed/failed), referenced in the implementation plan
- **Validation pipeline** — the three-layer pattern (schema → confidence → LLM cross-check) as a composable chain
- **Circuit breaker** — already described in Section 8, but formalise as a named pattern with the library/approach
- **Event-driven audit logging** — all audit writes go through an event bus/queue rather than inline DB calls

### Code Conventions
- **Project structure** — describe the folder layout for the monorepo or multi-repo approach (backend, frontend, Docling service, infrastructure)
- **Naming conventions** — file naming, database table/column naming (snake_case), API endpoint naming, TypeScript interface naming
- **Error handling standard** — how errors are structured, propagated, and logged consistently across services. Typed error classes with error codes.
- **Logging format** — JSON structured logs with mandatory fields (correlation_id, service, action, timestamp). Reference the observability section (currently Section 9).
- **API response envelope** — standard response shape for all portal API endpoints (success and error cases)

### Engineering Standards
- **API versioning** — how the portal's own API endpoints are versioned (URL path vs. header), and how external API versions are pinned
- **Code review expectations** — what a PR must include (description, test coverage, migration notes if applicable)
- **Dependency management** — how dependencies are pinned, audited, and updated (Dependabot/Renovate, lockfiles, security scanning)
- **Documentation standards** — what must be documented (API contracts via OpenAPI, data model changes, architectural decisions via lightweight ADRs)
- **Feature flags** — V1 approach to toggling capabilities and features without redeployment (ties into the capability registration model described in Section 13)

Keep it concise and practical — match the tone of the rest of the document. Use British English throughout. Avoid over-engineering the standards themselves — these should be "just enough" for a small team shipping V1, not an enterprise governance framework.
