# HireMind AI MVP

A local-first AI-assisted resume screening prototype with a React UI, Express API, SQLite persistence, and Gemini resume assessment.

## Start

1. Install Node.js 20+.
2. Run `npm install`.
3. Copy `.env.example` to `.env` and set `GEMINI_API_KEY` (backend only). You can change `GEMINI_MODEL` to a model available to your account.
4. In one terminal run `npm run server`.
5. In another terminal run `npm run dev`.
6. Open the local URL printed by Vite.

## Workflow

Create a job in Jobs, specifying criteria weights totaling 100. Open the job, upload selectable-text PDF resumes, and run screening. Candidate records and PDFs are stored locally; Gemini evaluates each PDF and returns evidence and 0–100 criterion scores. The server calculates weighted scores and the verdict using job threshold: Pass ≥ threshold, Review ≥ threshold minus 15, otherwise Fail. HR can independently approve or reject with a mandatory recorded reason. Reports use stored candidate data.

## Scope and limitations

- Screening runs sequentially to reduce Gemini free-tier rate-limit pressure. Rate-limit failures are displayed per candidate; use retry after the quota resets.
- PDFs must contain extractable text. Scanned PDFs need OCR, not included here.
- Duplicate PDFs are detected per job by SHA-256 hash.
- No real authentication, multi-user access, email sending, OCR, encryption at rest, or production deployment hardening.
- Blind review hides names in the UI, but does not redact PDF content. It is not an anonymity guarantee.
- AI scoring is an advisory heuristic and can be inconsistent. Resume quotes and scores should be independently verified. Never use automated scores as the sole basis for employment decisions.
- Keep `.env`, `hiremind.db`, and `uploads/` private. Do not upload real personal data without consent and appropriate security safeguards.
