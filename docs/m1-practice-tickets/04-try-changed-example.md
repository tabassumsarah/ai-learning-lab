# 04: Apply the concept to a changed example and revisit attempt history

**Tracking:** [GitHub #4](https://github.com/tabassumsarah/ai-learning-lab/issues/4). Published planning snapshot; GitHub is authoritative for current status. Implementation and paid calls are not authorized by publication.

## What to build

After baseline practice and any needed help, the learner attempts a new scenario or changed assumption, receives feedback, and can revisit both dated explanations and the assistance between them. This completes the first practice loop in demo mode without claiming independent mastery or long-term retention.

## Acceptance criteria

- [ ] Generate one source-supported changed-example task with explicit assumptions, a link to the prior attempt, and frozen private criteria before display. For a sound initial response, offer transfer practice without requiring corrective help.
- [ ] Validated tasks address the same concept while changing the scenario/assumption. Semantic quality fixtures/review distinguish genuine transfer from a paraphrase of the correction; JSON validation alone is not presented as proving this.
- [ ] Unsupported or malformed tasks fail visibly and leave previous responses/feedback intact. Explicit retry cannot duplicate an accepted next attempt or deliberately dispatch concurrent duplicate calls.
- [ ] The learner saves, reloads, submits, and receives feedback on the new response using the existing action/loader journey. Evaluation does not use tutor persuasion as a grading input.
- [ ] Show baseline, probe where applicable, changed-example responses, dates, current feedback, source links, and assistance. Preserve all original responses and distinguish helped practice from an attempt completed without additional help. Prior corrections remain visible as context, not erased to imply independence.
- [ ] Immediate improvement does not produce a permanent understood/mastered label, aggregate score, or retention claim. Uncertain judgments and unassessed reasoning dimensions remain visible.
- [ ] A restart during generation, drafting, or evaluation preserves the loop. Pending operations become interrupted with clear explicit recovery; no accepted results are silently regenerated.
- [ ] Action/loader integration tests exercise the complete baseline → probe/help or sound bypass → changed example → history journey against reopened SQLite. A keyboard-only browser walkthrough verifies navigation, citation links, state messages, and resume behavior.

## Blocked by

- Ticket 03: Probe uncertain reasoning before revealing corrective help.

## Demo

Complete the demo practice loop, restart the app, and inspect both explanations, their feedback, and exactly what help was shown between attempts.
