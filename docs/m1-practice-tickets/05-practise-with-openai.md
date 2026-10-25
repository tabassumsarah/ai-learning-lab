# 05: Complete the practice loop with OpenAI under visible spending limits

**Tracking:** [GitHub #5](https://github.com/tabassumsarah/ai-learning-lab/issues/5). Published planning snapshot; GitHub is authoritative for current status. Implementation and paid calls are not authorized by publication.

## What to build

The learner can switch from explicitly labelled demo practice to a real OpenAI-led practice loop, understand what content will be transmitted, approve a bounded operation, and see usage and failures without losing progress. Verify that the selected model provides acceptable feedback for this concept before calling the slice complete.

## Acceptance criteria

- [ ] Configure one selected OpenAI model through the small existing provider boundary, using separate tutor/evaluator instructions and the same validated task/result contracts. Keep fake mode available without credentials; live results and simulated results cannot be confused.
- [ ] Before first live transmission, disclose the external destination and content being sent and obtain explicit confirmation. Explain estimated operation cost before dispatch. Missing credentials or dated pricing disables live calls while drafts and history remain accessible; credentials are never requested in chat or exposed in browser payloads/logs.
- [ ] Enforce configured token ceilings, integer cost accounting, session/day spending limits, and conservative pre-call reservations including active reservations. Display reported versus estimated/unknown usage and failed attempts. Do not interpret missing usage as zero or silently repair/retry with another paid call.
- [ ] Keep one active paid operation per session with stable idempotency and accepted-result protection. A timeout or interruption is recorded as unknown billing and offers an explicit, newly reserved retry; never claim exactly-once provider billing.
- [ ] UI-to-server-to-database fault tests using the fake provider cover budget rejection, concurrent requests, malformed output, unsupported citations, timeout/restart, missing configuration, explicit retry, and result restoration. Live calls are not part of default tests.
- [ ] Run a separately approved bounded live quality set for the one sample concept: sound, partial, fluent-but-wrong, alternative-valid, ambiguous, and recall-without-transfer responses, with paired equivalent-reasoning answers of different English fluency. Repeat enough to expose variability within the approved budget; define case count/repetitions before spending.
- [ ] Reject the candidate configuration if it fabricates material source claims, accepts a clearly wrong mechanism as sound, penalises English fluency in reasoning judgments, or leaks private answers. Verify all accepted citations resolve and inspect their actual support. Unresolved failures block completion rather than being averaged away.
- [ ] Inspect that probes address the specific reasoning gap and changed examples require application beyond repetition. Record model/prompt/schema versions, case outcomes, latency, usage, cost, and limitations in a reproducible report. Developer review calibrates the app; no human practice buddy is required at runtime.
- [ ] Perform and record a bounded live browser journey through baseline, probe/help as appropriate, changed-example practice, and restored history. Record safe failures and explicit retry. Do not claim this one-concept check replaces full M1 gates or proves durable learning.

## Blocked by

- Ticket 04: Apply the concept to a changed example and revisit attempt history.

Additional live-work gates: choose the exact OpenAI model; approve dated price assumptions, task limits, session/day caps, evaluation budget, and fixed evaluation case count/repetitions; configure API access securely. Provider choice alone does not satisfy these gates. The adapter and deterministic budget/failure tests may be developed without issuing paid calls after implementation is authorized.

## Demo

Complete the same practice loop with real OpenAI responses, inspect source-backed reasoning and separate clarity feedback, view actual usage, and demonstrate that a rejected/failed operation preserves work and requires explicit retry.
