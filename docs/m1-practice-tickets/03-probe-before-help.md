# 03: Probe uncertain reasoning before revealing corrective help

**Tracking:** [GitHub #3](https://github.com/tabassumsarah/ai-learning-lab/issues/3). Published planning snapshot; GitHub is authoritative for current status. Implementation and paid calls are not authorized by publication.

## What to build

When an explanation exposes a misconception, the learner receives one targeted question before corrective help, or can request the explanation immediately. When meaning is unclear, the learner can clarify without the app turning uncertainty into a confident weakness. The original response remains intact and revealed help is recorded.

## Acceptance criteria

- [ ] Add a tutor task with instructions separate from the evaluator. Given a misconception, generate and validate one focused source-supported probe without embedding the correction or model answer in the prompt.
- [ ] Freeze the probe task/criteria and save its answer as a linked attempt, reusing draft/submit/evaluate behavior. Preserve the original submitted response and evaluation.
- [ ] After the probe response, or an explicit direct-explanation request, show source-backed corrective help and a specific revisit action. A failing probe-generation operation leaves prior work intact and still allows explicit direct help.
- [ ] Sound baseline responses bypass remediation without manufacturing a misconception. An ambiguous response receives a clarification prompt; if clarification is insufficient, the judgment remains uncertain. New reasoning in clarification is not retroactively credited to the original response.
- [ ] Persist revealed hints, corrections, and prior-answer exposure as assistance events affecting subsequent evidence. Showing a probe/help response twice does not create duplicate attempts or assistance events.
- [ ] Withheld correction/private criteria are absent from pre-reveal browser payloads. Article/answer injection text cannot override the task or gain tools. The runtime has no model browsing or code-execution capability.
- [ ] Reload/restart at the probe, clarification, and help stages restores the correct state without revealing help early or losing draft responses. Generation/evaluation failures have explicit retry and redacted errors.
- [ ] Primary-boundary tests cover misconception → probe → help, direct-help bypass, sound bypass, ambiguity/clarification, hidden correction, assistance, and resume behavior using deterministic fake responses.

## Blocked by

- Ticket 02: Receive validated feedback on a submitted explanation.

## Demo

Show a misconception receiving one probe, then help. Repeat using the direct-help action. Show an ambiguous answer asking for clarification and retaining uncertainty if it remains unclear.
