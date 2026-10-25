# 02: Receive validated feedback on a submitted explanation

**Tracking:** [GitHub #2](https://github.com/tabassumsarah/ai-learning-lab/issues/2). Published planning snapshot; GitHub is authoritative for current status. Implementation and paid calls are not authorized by publication.

## What to build

The learner requests feedback on their submitted explanation and sees source-backed reasoning judgments separately from explanation-structure observations. A deterministic fake provider makes the journey testable without credentials or paid calls. Demo output is explicitly labelled simulated; it is not represented as real AI assessment.

## Acceptance criteria

- [ ] Add a small provider contract used by the evaluator, with task/prompt/schema versions and validated structured results. Record operation/call state and accepted evaluations without coupling application behavior to one vendor.
- [ ] Evaluate the frozen source, prompt, criteria, and submitted response without persuasive tutor commentary. Use supported/partial/gap/uncertain judgments with response evidence, source references, and next actions; omit aggregate scores and permanent mastery claims.
- [ ] In a sound demo case, show positive reasoning evidence without inventing a gap. Keep feedback on logical order, explicit connections, and audience fit separate from reasoning. Grammar or vocabulary sophistication is not a reasoning criterion.
- [ ] Persist valid misconception judgments but show only that a follow-up is needed until the probe/help flow is available. Do not leak the corrective explanation through loaders or action responses. Ambiguous cases visibly remain uncertain rather than receiving a confident verdict.
- [ ] A new fake evaluation succeeds only after schema, source-membership, and cross-field checks. Malformed output or foreign passage IDs fail visibly without accepting partial feedback or changing the submitted text.
- [ ] Double requests do not create duplicate accepted evaluations or deliberate provider calls. Provider failures preserve the submitted response, show a useful redacted error, and offer explicit retry. Fake calls are identified as simulated with zero paid spend, not as reported live usage.
- [ ] Loading the same session after restart restores the submitted answer, evaluation state, and any feedback already allowed to be shown. Credentials, private criteria, and raw provider errors stay server-side.
- [ ] Action/loader tests use real SQLite and scripted provider fixtures for sound, misconception, ambiguous, malformed, and failing outcomes. They verify public behavior and result persistence; scripted fixtures do not count as proof of grading quality.

## Blocked by

- Ticket 01: Review one concept and save a first explanation.

## Demo

Submit an explanation, request clearly labelled demo feedback, follow a source citation, reload, and recover the same feedback. Demonstrate an invalid provider result and explicit retry without losing the response.
