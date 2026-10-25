# First implementation milestone

Status: revised proposal. Implementation begins after architecture approval and resolution of the provider, schedule, and cost settings below.

## M1: One concept, AI-led practice, and a later review

Build one local vertical slice: article ingestion and source review → concept choice → prior-knowledge probe → spoken or typed explanation → AI feedback → changed-example retry → saved review date and email → later unaided practice. The learner needs no human buddy. Use fake learning, transcription, and email adapters for deterministic development, then bounded live checks. Aim for a 10–15 minute initial loop with pause/resume.

Implementation sequence:

1. Scaffold Svelte 5/SvelteKit, TypeScript, Tailwind, and Vitest; pin compatible versions. Add server-only settings, SQLite migrations, and fake adapters.
2. Implement safe article extraction, immutable snapshots, source confirmation, passages, and concept selection.
3. Add AI contracts, budgets/usage, provisional prior-knowledge diagnosis, audience choice, and clearly labelled prerequisite support.
4. Add typed drafts and bounded speech transcription with correction/confirmation and temporary-audio cleanup. Freeze individual prompts and responses; persist assistance, evaluations, and feedback challenges.
5. Add fresh-example retries and optional short writing practice; derive dated evidence without aggregate scores. Persist concept review plans, due/overdue views, and external scheduled-email reconciliation.
6. Run deterministic/security/quality gates and a bounded live journey including actual email receipt and later review. Document setup, external disclosures, retention, pricing, and limits.

## Acceptance criteria

- Fresh checkout runs locally with repeatable schema setup and helpful missing-credential states. Secrets remain server-side.
- Supported public HTML produces a confirmable snapshot with stable passages. Private destinations, unsafe redirects, oversized/unsupported content, and timeouts fail safely.
- The learner chooses one concept and an audience (default: technically curious software colleague unfamiliar with the topic). The AI uses a brief prior explanation/follow-up to adapt support; the learner can correct its inference.
- Article-supported claims have valid evidence. Supplementary prerequisite explanations are visibly unverified and do not silently become assessment criteria. Insufficient evidence yields a narrower question or uncertainty.
- Typed and spoken responses share reasoning criteria. Transcripts can be corrected before submission, drafts survive reload, and temporary audio is discarded on success/failure/cancellation/restart. Recording failure leaves a text fallback.
- Practice is turn-based. The AI waits for the explanation, probes reasoning, offers one targeted prompt before correction unless direct help is requested, and records assistance. No human practice assessor is required.
- Each prompt and its expected reasoning/criteria freeze before display. Submission explicitly freezes one response. Duplicate submissions do not deliberately create another paid call or evaluation.
- Feedback separates reasoning from explanation structure; grammar, accent, pauses, and vocabulary sophistication do not lower reasoning judgments. Unclear meaning prompts clarification. The learner can challenge feedback and inspect original/revised judgments; unresolved ambiguity stays uncertain.
- A changed-example retry tests reasoning beyond recall. Evidence distinguishes assistance, unaided reasoning, later review, and unassessed dimensions; there is no permanent mastery label. Optional short writing asks for the learner's draft/revision before a sample rewrite.
- A visible, overrideable next review date and one email reminder are saved. Early review/date change cancels or replaces the reminder; failed/unknown operations remain visible and retryable. Email contains no answer, score, or correction. There are no repeated overdue emails.
- Reminder delivery works with the local app closed after successful external scheduling. Email tells the learner to open the laptop app; it does not promise remote access. Due/overdue concepts remain visible. A later review asks before revealing previous feedback and records any assistance.
- Reload, timeout, malformed output, interrupted processes, and explicit retries preserve drafts, submitted responses, evidence, and due dates. Deletion reconciles external reminders without retaining learning content in cancellation records.
- Learning, transcription, and email costs have explicit supported accounting and limits. Every external attempt is recorded; unknown usage is never treated as free. No silent paid retries.
- Injection fixtures cannot gain executable/tool capabilities or leak hidden expected answers. Keyboard-only input, citation navigation, labelled controls, and clear errors work.
- The deterministic and developer-reviewed quality gates in [testing and evaluation](./testing-and-evaluation.md) pass. Human calibration tests the app, not each learner practice session.

## Resolve before implementation

OpenAI is selected for learning AI. Select the exact learning model and transcription/email providers using bounded quality and capability checks. Confirm audio formats/limits and retention, email sender setup and cancellation/idempotency behavior, price accounting and caps, review intervals, uncertainty behavior, recipient/time zone/delivery-time preferences, and the bounded evaluation budget. These remain proposed choices, not final ADRs.

Mandatory five-question assessments, aggregate score dashboards, comprehensive coverage, live voice, English coaching, audio playback, full blog drafting, SMS, repeated overdue reminders, agents, and additional source types are outside M1.

Milestone evidence: reproducible deterministic report, manual journey screenshots or recording, bounded live quality/cost report, and a pilot across three personally relevant concepts including fresh-example and later unaided evidence. Report missed reviews and remaining gaps without assuming success. These are future implementation deliverables, not completed work.
