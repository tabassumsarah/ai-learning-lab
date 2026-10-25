# 01: Review one concept and save a first explanation

**Tracking:** [GitHub #1](https://github.com/tabassumsarah/ai-learning-lab/issues/1). Published planning snapshot; GitHub is authoritative for current status. Implementation and paid calls are not authorized by publication.

## What to build

A learner can start the local application, review a bundled sample article with numbered passages, confirm it, and write, save, and explicitly submit one explanation for a technically curious software colleague. Returning after reload or process restart restores the same attempt. This is a working UI-to-server-to-SQLite journey, not a scaffolding-only ticket.

## Acceptance criteria

- [ ] A fresh checkout has documented local setup, compatible pinned dependencies, repeatable database initialization, and one runnable practice page. Include the proposed application foundation as part of this behavior rather than a separate infrastructure ticket.
- [ ] Bundle one original or permitted article, stable passages, one concept, and one baseline mechanism/reasoning prompt. Record honest bundled-source provenance and demonstrate that reinitialization/reload does not duplicate the learning session.
- [ ] Show the sample-material label, concept, default audience, and readable numbered source passages. Confirmation unlocks practice and is persisted.
- [ ] Freeze the prompt, expected reasoning, private criteria, and passage references before display. Public responses omit expected answers/private criteria; direct mutation attempts cannot replace the frozen task.
- [ ] A learner can save an editable typed draft and recover it after reload/reopening SQLite. Show clear save failures without claiming unsaved work is persisted.
- [ ] Explicit nonblank submission freezes the response; later edits are rejected. Repeat submission returns the same submitted attempt rather than creating another attempt. The UI honestly shows submitted/awaiting feedback until evaluation is added.
- [ ] Bind locally, retain request-origin protection, safely render source/learner text, and provide labelled keyboard-accessible controls and loading/error states. There are no paid calls or required API credentials.
- [ ] Server-action/loader tests against temporary real SQLite verify source confirmation, draft restoration, immutable submission, duplicate prevention, and hidden-answer exclusion. A manual browser walkthrough verifies the actual form and passage navigation.

## Blocked by

None of the other tickets. Before implementation, confirm the proposed SvelteKit/TypeScript/SQLite/Zod/Vitest stack, bundled-source representation, and selected sample article/concept. Those decisions are not settled by drafting this ticket.

## Demo

Open the sample, confirm it, save an explanation, restart the app, submit, and show that the submitted response cannot be edited or duplicated.
