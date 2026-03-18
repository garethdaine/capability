# Brainstorming Session: contract-clause-design-review

**Started:** 2026-03-18
**Time budget:** 10 minutes
**Task:** Review V1 capability design document for gaps, inconsistencies, and areas to strengthen. Output is improvements to the design doc only — no code.

---

## Session Log

### Phase 0 — Setup
- Git: enabled (existing repo)
- Session directory created
- Read design doc (523 lines, 13 sections) and scratchpad

### Phase 1 — Discovery (compressed)
Context scan complete. Key findings from initial read:

**Critical inconsistencies found:**
1. Workflow diagram (Section 3) and sequence diagram (Section 7) don't show Docling parsing step — contradicts Section 2.3
2. Three-layer validation (Section 2.4) not reflected in workflow/sequence diagrams
3. FINDING table missing `confidence_score` and `verification_status` fields — but Section 2.4 describes these features with UI badges
4. API request payload (Section 5.1) shows raw file being sent, but Section 2.3 says parsed content goes to the API — ambiguous

**Missing concerns an interviewer would probe:**
5. No observability/monitoring section (logging, metrics, alerting)
6. No data retention policy specifics
7. No testing strategy description
8. No multi-tenancy consideration in data model
9. Summary doesn't explicitly tie back to the four assignment criteria

## Approaches
- **Selected**: Both — rapid pass (fix inconsistencies + add missing sections)

## Execution Log

### Inconsistency Fixes Applied
1. **Section 3 workflow diagram** — Added Docling parsing step and validation steps between upload and API call
2. **Section 7 sequence diagram** — Added Docling service and Claude API participants; added parsing call, three-layer validation steps, and async LLM cross-check flow
3. **Section 6 data model** — Added `confidence_score` (decimal) and `verification_status` (string) to FINDING table, with design decision rationale
4. **Section 5.1 API request** — Changed `file` to `parsed_content` to reflect that Docling-processed text is sent, not raw file
5. **Section 10 implementation plan** — Added LLM cross-check service to Phase 2, observability setup to Phase 4, updated data model task description

### New Content Added
6. **Section 9 (new) — Observability & Monitoring** — Structured logging, key metrics table (6 metrics with alert thresholds), health checks, data retention policy
7. **Section 14 Summary (rewritten)** — Explicitly maps to the four assignment criteria: practical, reliable, extensible, simple

### Housekeeping
8. Renumbered sections 10-13 → 11-14 to accommodate new Section 9
