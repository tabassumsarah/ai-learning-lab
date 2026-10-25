# First implementation milestone

## M1: One article, one complete learning journey

After architecture approval, build one local vertical slice covering ingestion, exploration, five-question assessment, evaluation, and a persisted results dashboard. Use a fake provider for deterministic development and one configured live provider for a bounded manual smoke test. UI polish, agents, and additional source types are outside this milestone.

Implementation sequence:

1. Scaffold Svelte 5/SvelteKit, TypeScript, Tailwind, and Vitest; pin compatible Node/package versions. Add server-only configuration, SQLite migrations, and a fake AI adapter.
2. Implement safe article fetching/extraction, snapshot review, passages, and persistence.
3. Add the AI gateway with strict schemas, reservations, usage display, and concept/tutor services.
4. Add frozen questions, draft answers, explicit submission, evaluation, and dashboard derivation.
5. Run fixture/security/quality gates; document local setup, credentials, provider data disclosure, and limits.

## Acceptance criteria

- A fresh checkout can run locally using documented setup; schema initialization is repeatable. Missing credentials show a useful state without revealing secrets.
- A supported article URL produces a reviewable snapshot with stable passages. Unsupported HTML, private destinations, redirects to private networks, oversized pages, and timeouts fail safely.
- The learner confirms extraction before a paid analysis. The app shows 3–8 grounded concepts and can answer a follow-up with valid passage links or an insufficient-evidence response.
- Starting assessment produces exactly five frozen questions in the specified categories, two rubric criteria per question, and at least three reasoning prompts. No private rubric or expected answer appears in pre-submission browser payloads.
- Five draft answers survive reload. Submission is explicit and freezes answers; duplicate submissions do not trigger another grading call. Assisted practice is labelled.
- Evaluation returns feedback for all five answers, deterministic scores, demonstrated/missed/unassessed concepts, and concrete revisit links. Ambiguous results are labelled and not given a definitive aggregate score.
- Reload restores the dashboard. Provider timeout, malformed output, interrupted process, and explicit retry preserve prior work and produce visible usage states.
- Every paid attempt is recorded. A configured cap blocks calls before dispatch, including concurrent calls/reservations, and unknown billing remains visible.
- Credentials are absent from browser bundles, HTML, action responses, and logs. External HTML/scripts and prompt-injection fixtures cannot gain executable or tool capabilities.
- Vitest deterministic gates and the human-reviewed AI quality gates in [the evaluation strategy](./testing-and-evaluation.md) pass. Record live model/version, latency, token usage, estimated cost, and observed failures.

Milestone evidence: a reproducible test report, a recorded manual walkthrough or screenshots of the full journey, and the live evaluation report. These are future implementation deliverables, not part of this design-only change.
