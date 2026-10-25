# M1 slice: Explain one concept, receive AI feedback, and try a changed example

Status: slice scope and server-action/loader testing boundary confirmed by the learner. This is the first increment within M1, not the completed MVP. OpenAI is selected as the learning AI provider. Architecture choices, the exact model, cost limits, and live evaluation budget remain unresolved; implementation and paid calls are not authorized. The learner approved publication of the five implementation tickets; see the [published ticket breakdown](./m1-practice-tickets/README.md).

## Problem Statement

The learner wants to improve reasoning and their ability to explain AI ideas to a technically curious colleague. Reading and repeating an article can feel like understanding without demonstrating it. They need an AI-led opportunity to explain a mechanism, receive specific source-backed feedback, and test their reasoning when an assumption changes. No human practice buddy should be required, and English fluency must not affect the reasoning judgment.

The repository currently contains design proposals but no application code or existing test infrastructure. The first increment should exercise learning behavior across UI, server, persistence, and an AI boundary rather than deliver only scaffolding or a disconnected provider wrapper.

## Solution

Provide a local practice page for one bundled, licensed or original article snapshot and one preselected concept. The learner reviews the numbered passages, confirms the source, and answers a focused prompt in writing for the default audience: a technically curious software colleague unfamiliar with the topic.

The AI evaluator returns reasoning judgments and separate explanation-structure feedback. A sound or ambiguous response receives suitable feedback; a misconception first receives one targeted probe, unless the learner requests a direct explanation. After source-backed help, a new task changes an assumption or application scenario. Both responses and their feedback remain available after reload and process restart, with assistance visible and uncertainty preserved.

Use typed input to isolate the reasoning-feedback loop in this first increment. Spoken practice and scheduled reinforcement remain requirements of the full M1; this slice does not substitute for them or claim to validate durable learning.

## User Stories

1. As a learner, I want to open one local practice page, so that I can try the learning loop without account setup.
2. As a learner, I want to review the bundled article and numbered passages, so that I know what the practice is grounded in.
3. As a learner, I want to confirm the source before it is sent to an AI provider, so that I control external processing.
4. As a learner, I want a single concept and a clear intended audience, so that my explanation has a focused purpose.
5. As a learner, I want a question that asks how or why a mechanism works, so that I practise reasoning rather than terminology recall.
6. As a learner, I want to save and resume my draft, so that a reload does not erase my work.
7. As a learner, I want to submit deliberately, so that the AI evaluates the explanation I intended to give.
8. As a learner, I want reasoning feedback supported by article passages, so that I can inspect its basis.
9. As a learner, I want explanation-structure feedback kept separate from reasoning, so that English fluency is not mistaken for understanding.
10. As a learner, I want a targeted question before a misconception is explained, so that I can try to repair my reasoning myself.
11. As a learner, I want to request the direct explanation instead, so that I can get unstuck.
12. As a learner, I want unclear meaning to be marked uncertain and clarified, so that ambiguity is not automatically counted as a misconception.
13. As a learner, I want a changed-example task after help, so that I can test application instead of repeating a correction.
14. As a learner, I want assistance and attempt relationships shown, so that immediate improvement is not presented as independent mastery.
15. As a learner, I want dated responses and feedback restored after restart, so that I can revisit the evidence.
16. As a learner, I want failed evaluation to preserve my submitted response, so that I can explicitly retry without rewriting it.
17. As a learner, I want disclosure, estimated costs, caps, and unknown usage shown, so that I control paid requests.
18. As a learner, I want clear keyboard-accessible loading and error states, so that I can complete the loop reliably.

## Implementation Decisions

All architectural choices here remain proposed and reuse the existing design direction.

- Use one local SvelteKit application with Svelte, TypeScript, SQLite, Zod contracts, and Vitest. Bind to loopback; keep provider credentials, expected answers, private criteria, and raw provider errors server-side. Include repeatable schema setup and local run instructions.
- Bundle one original or permitted article snapshot, stable passages, one concept, and one baseline prompt with frozen source-backed criteria. Clearly identify it as bundled sample material. Do not accept arbitrary URLs in this slice or fabricate fetch provenance: record a real original URL where applicable, otherwise a fixture identifier with an explicit bundled origin. Reuse these records across reloads without creating duplicate sessions. This origin distinction is a proposed refinement to the URL-oriented source schema, not a final ADR.
- The baseline explanation supplies initial evidence of knowledge. A separate learner-profile diagnostic, concept discovery, and audience selection are deferred; use the agreed default audience. Do not infer a permanent learner level.
- Build through server actions and public loaders. The application coordinates attempts, tutor probes/help, evaluator requests, and public feedback views. Tutor and evaluator use separate instructions; the evaluator receives the source, frozen task, and submitted answer without persuasive tutor commentary. Assistance is recorded independently.
- A draft is editable and persistable. Explicit nonblank submission freezes the response; tasks and private criteria freeze before display. Initial evaluation is immutable. A clarification creates a linked probe attempt rather than overwriting submitted text; unresolved meaning remains uncertain. Formal feedback disputes and revised evaluation histories are deferred.
- For a misconception, persist the evaluation but withhold its corrective explanation while offering one targeted probe. After that response, or an explicit direct-help request, reveal source-backed feedback. Sound responses may proceed to the changed example; do not manufacture a gap. Ambiguous responses receive a clarification prompt without a confident judgment. Record every revealed hint, correction, or prior answer that affects the next attempt.
- Generate one changed-example prompt with explicit assumptions and source-backed criteria, validate it, then freeze it before display. Reject paraphrases of the correction or tasks requiring unsupported external facts during quality review. If a valid task cannot be generated, fail visibly without discarding previous work; let the learner retry explicitly.
- Evaluate task-relevant conceptual accuracy, causal reasoning, application, and limitations using supported/partial/gap/uncertain judgments. Return separate clarity observations about logical order, explicit connections, and audience fit. Equivalent reasoning is valid. Grammar and vocabulary sophistication do not lower reasoning judgments. Feedback includes response-specific evidence, source references, and a next action; valid citation IDs alone do not prove factual correctness.
- Persist only the source, passages, session, concept, attempts, assistance, accepted evaluations, and AI-operation/call records needed for this loop. Preserve baseline, probe, and changed-example relationships and timestamps. Use transactions for state transitions, no network calls inside them, and no aggregate score or permanent mastery field.
- The AI gateway validates schemas, source membership, and cross-field constraints. Invalid output cannot advance accepted learning state. Use idempotency, one active paid operation per session, and explicit retry. On restart, interrupted calls become visible with unknown usage; never promise exactly-once provider billing.
- Develop with a deterministic fake provider and an explicit demo indicator; fabricated responses are never represented as real AI assessment. Completion also requires an OpenAI adapter with an evaluated model and a bounded live walkthrough. Before live calls, disclose content transmission and require configured dated pricing, token ceilings, session/day caps, and an explicit evaluation budget. Missing credentials or prices disables live calls without losing work.
- Render article/model text safely and retain origin protections. Neither the model nor sample content gains browsing, filesystem, code-execution, or tool capability. Do not log responses or credentials.

## Testing Decisions

Proposed primary boundary: invoke the same server actions and loaders used by the UI, with a temporary real SQLite database and a fake AI provider. Assert public behavior and persisted results after reloading/reopening the database, rather than internal call order or helper names. The learner confirmed this boundary during spec review. No existing automated tests provide code-level prior art; follow the existing testing-and-evaluation design.

Acceptance scenarios:

1. Source review and confirmation lead to one focused task; expected answers and private criteria are absent from pre-submission browser payloads.
2. A saved draft survives reload; nonblank explicit submission freezes it. Double submission does not create duplicate accepted results or deliberate provider requests.
3. A sound response gets supported reasoning feedback without an invented weakness. Paired equivalent answers with different English fluency receive equivalent reasoning judgments.
4. A misconception produces one probe before corrective help unless direct help is requested. Ambiguity creates clarification and stays uncertain when unresolved.
5. Changed-example practice stores a new frozen task and response, retains the original, and records assistance without claiming independent mastery.
6. Foreign citations, malformed output, provider failure, timeout, budget rejection, and restart preserve prior work and expose accurate retry/usage states.
7. Loading the same session after reopening SQLite reconstructs responses, feedback, assistance, and attempt relationships.

Add focused deterministic contract, budget, and transaction tests where the primary boundary cannot isolate a material failure clearly. Perform a manual keyboard-only browser walkthrough for forms, citations, reload/resume, loading, and errors.

A fake provider proves orchestration, not AI quality. Before calling the slice complete, review a bounded live set for the selected concept: sound, partial, plausible-but-wrong, alternative-valid, ambiguous, and recall-without-transfer answers, including paired fluency variants. Every accepted citation must resolve; no material source fabrication, fluent-but-wrong full acceptance, private-answer leakage, or English-fluency reasoning penalty is acceptable. Inspect whether probes and changed examples target reasoning rather than merely change wording. Record model/prompt versions, costs, failures, and limitations. This small check does not replace the full M1 evaluation suite or demonstrate long-term learning.

## Out of Scope

URL fetching/extraction, multiple articles or concept discovery, speech/transcription, supplementary prerequisite teaching beyond the bundled source, configurable audiences, full prior-knowledge profiling, formal feedback challenges/revisions, separate blog-writing exercises, scheduled reviews, email/SMS, long-term retention claims, full M1 release/pilot gates, aggregate scores, agents, code execution, remote hosting, and user accounts.

These are slice exclusions, not removal of agreed M1 requirements. In particular, spoken practice, feedback challenges, and scheduled email reinforcement still belong to M1.

## Further Notes

This spec is grounded in the existing product requirements, architecture, logical schema, M1 plan, and evaluation strategy; it does not replace them. The bundled-source origin refinement and deferral of feedback-to-review-plan atomic updates apply only to this increment and need explicit scope approval. Later scheduling work must restore the full feedback/review-plan transition requirements.

Before implementation: approve the applicable architecture and bundled-source representation; select the exact OpenAI model; confirm task limits, cost caps, and live evaluation budget. Full M1 still requires decisions about transcription, scheduling, and email. Do not label the issue ready-for-agent while these slice prerequisites remain unresolved. Once approved and resolved, the normal to-spec publication target is the project tracker with ready-for-agent; the learner has explicitly approved publication of the five linked tickets, which remain gated and are not ready-for-agent.
