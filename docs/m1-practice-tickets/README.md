# M1 first practice slice — published ticket breakdown

Status: all five tickets are published on GitHub with enhancement and needs-info labels and native blocking relationships. None is marked ready-for-agent. GitHub is authoritative for execution status; these local files retain the planning snapshot. Publication does not authorize implementation or paid calls.

Source: [saved slice spec](../m1-first-practice-slice.md). The spec's agreed scope and action/loader testing boundary are preserved. Local planning IDs 01–05 map to GitHub issues #1–#5 below.

| Planning snapshot / GitHub issue | Blocked by | Demoable behavior |
| --- | --- | --- |
| [01: Save a first explanation](./01-save-first-explanation.md) · [#1](https://github.com/tabassumsarah/ai-learning-lab/issues/1) | No other ticket; architecture/sample approval gate | Review source → confirm → draft → submit → reload/restart |
| [02: Receive demo feedback](./02-receive-demo-feedback.md) · [#2](https://github.com/tabassumsarah/ai-learning-lab/issues/2) | 01 | Submitted response → validated, visibly simulated feedback → source links |
| [03: Probe before help](./03-probe-before-help.md) · [#3](https://github.com/tabassumsarah/ai-learning-lab/issues/3) | 02 | Misconception → targeted probe or direct help; ambiguity → clarification |
| [04: Try a changed example](./04-try-changed-example.md) · [#4](https://github.com/tabassumsarah/ai-learning-lab/issues/4) | 03 | Fresh scenario → response → feedback → dated history with assistance |
| [05: Practise with OpenAI](./05-practise-with-openai.md) · [#5](https://github.com/tabassumsarah/ai-learning-lab/issues/5) | 04; live model/cost/access gates | Real AI-led loop with visible spending controls and bounded quality evidence |

The published native dependency chain is #1 → #2 → #3 → #4 → #5 (each issue blocks the next). Each edge names the immediate prerequisite; earlier prerequisites are inherited. This intentionally favors a small sequential learning project over parallel implementation. Each implementation ticket includes its UI, server behavior, persistence, appropriate tests, and error states; there are no standalone scaffold/database/provider-only tickets. The repository currently has no application code to prefactor.

## Common constraints

- Develop and test through public server actions/loaders with real temporary SQLite and fake provider responses. Check outcomes after reopening the database rather than internal helper details. Include manual keyboard/browser checks where relevant.
- Keep private criteria, expected answers, credentials, and raw provider errors server-side. Render untrusted text safely and preserve request-origin checks from the first ticket onward.
- Preserve frozen tasks/responses, explicit submission/retry, dated evidence, and assistance. No aggregate score or permanent mastery label. English fluency does not lower reasoning judgments.
- Deterministic demo behavior is not evidence of AI assessment quality. A bounded, developer-reviewed live check belongs to ticket 05; normal practice requires no human buddy.
- No speech, URL ingestion, formal feedback disputes, scheduled review, or email delivery is added by this breakdown. Those remain later work required by full M1, not removed requirements.

## Approval and sequencing gates

The saved spec currently lists exact model selection and cost limits as prerequisites before implementation generally. This breakdown proposes refining that gate: allow tickets 01–04 to be implemented with no paid network access once their applicable architecture and sample-source choices are approved; require model/pricing/spend approval before the live portions of ticket 05. This is a proposal for review, not an automatic change to the approved spec or milestone.

Before ticket 01, confirm the applicable stack and bundled-source provenance representation and select original/permitted sample content and concept. The first ticket can author an original short sample as part of implementation if that approach is approved. No full speech/email architecture decision is needed to draft or build the isolated typed demo, subject to explicit scope/gate approval.

Before any live calls, separately approve the exact model, price snapshot, task ceilings, session/day limits, live evaluation budget, and fixed case count/repetitions. OpenAI is the selected learning provider; none of those numeric/configuration choices is silently inferred.

## Remaining planning questions

1. Is five tickets the right size, or should any be merged/split?
2. Are the immediate blocking edges justified, especially keeping the OpenAI integration after the complete demo loop?
3. Is the proposed fake-first gate refinement acceptable while model and spending details remain unresolved?

The learner explicitly approved publication of these five tickets. Bodies, labels, open states, and all four native blocking relationships were verified after creation. Keep execution status and acceptance checkboxes on GitHub rather than maintaining a competing local tracker. Resolve the remaining architecture/sample and live-model/budget gates before marking relevant work ready; no code implementation, paid calls, commit, or push was authorized by publication.
