# Testing and evaluation strategy

Status: revised proposed gates for concept practice and scheduled review; these are targets, not measured results.

## Deterministic tests with Vitest

- Ingestion fixtures: ordinary technical prose, headings/code, navigation-heavy pages, malformed HTML, thin content, oversized documents, and unsupported pages. Check extraction fidelity, stable hashes/passages, and rejection rather than silent truncation.
- Fetch security using injected DNS/transport doubles: private and reserved IPv4/IPv6, encoded IP forms, mixed DNS answers, DNS rebinding, redirect chains/loops, credentials in URLs, unexpected ports, decompression limits, and timeouts. Verify the actual connection uses the validated address. Tests must not contact internal networks.
- AI contract tests: malformed JSON, extra fields, nonexistent/foreign passage IDs, unsupported criterion judgments, wrong concept/attempt IDs, missing frozen criteria, invalid provenance labels, insufficient-evidence responses, and citation failures. Reject invalid results without state advancement.
- Evidence logic: dated attempt labels, uncertainty, current evaluation revision, unassessed dimensions, and assistance before/during submission. New reasoning in a clarification must not rewrite the original unaided evidence. No aggregate score or permanent mastery state.
- Speech: fake transcription, corrected transcript submission, size/type/duration rejection, failures/cancellation, temporary audio cleanup including restart, no audio in DB/logs, and typed fallback.
- Review scheduling: injected clock, rule versions, assistance/uncertainty effects, overrides, UTC/time zone/daylight-saving boundaries, due/overdue views, and no prior-feedback reveal before an unaided review.
- Email: fake adapter verifies stable request keys, schedule/cancel/replace ordering, early review, interrupted/unknown dispatch, reconciliation on reopen, cancellation races, explicit retry, opt-out, deletion tombstones, and no repeated overdue sends. Accepted scheduling is not recorded as confirmed delivery. Check message bodies omit answers, scores, and corrections.
- SQLite integration tests against temporary real databases: migrations, FKs, rollback, repeat attempts, one-response submission, prompt/answer freeze rules, evaluation revisions/challenges, review-plan updates, reminder reconciliation, duplicate submission, one active operation, retry lineage, process interruption, delete cascades, and fresh-load reconstruction.
- Budget tests: integer rounding, price snapshots, missing prices, token limits, reservations, concurrent session/day limits, schema repair, provider errors with usage, and unknown billing after timeout. Include duration-based transcription reservations and separate email accounting; never treat missing usage as zero spend.
- Server boundary tests: loaders/actions omit rubrics before submission, all secrets and provider errors are redacted, request-origin protection works, and article/model HTML is escaped.

Use small dependency interfaces for transport, clock, learning provider, transcription, email, and database connections. Default CI tests use saved synthetic or appropriately licensed fixtures and fake external adapters; no credentials, paid calls, live article downloads, or real emails.

## Journey verification

Run a documented manual browser journey for M1: URL → confirm extraction → choose concept/audience → prior-knowledge probe → record explanation → correct transcript → save/reload → submit → AI probe/help/feedback → fresh-example retry → optional written revision → schedule email → reload → later unaided review. Repeat the core response path with typed input. Challenge one misunderstood response and inspect both evaluation revisions.

Repeat with failed extraction/transcription, provider timeout, malformed evaluation, and failed/unknown reminder scheduling/cancellation. Confirm progress remains resumable. Verify actual reminder receipt with the app closed after successful scheduling, early-review replacement, and overdue display without repeated emails. Delivery and provider-retention claims need live checks; fake adapters alone do not prove them. Check keyboard-only use, focus/error announcements, readable code, narrow screens, text fallback, external-processing disclosure, and citation navigation. Practice remains laptop-based. Add automated browser tooling only when recurring regression effort justifies it.

## AI quality evaluation

Keep a versioned, human-authored set of five representative articles or permitted excerpts covering model architecture, retrieval, evaluation, inference, and an engineering trade-off. Include one article with insufficient evidence and adversarial source passages. Freeze source snapshots, annotate passage-level claims and essential concepts, and separate a tuning subset from at least two held-out articles. Do not tune prompts against held-out answers.

For each assessable article, a developer/reviewer authors focused concept prompts and variants: sound reasoning, partial reasoning, fluent but wrong, accurate recall that fails a changed assumption, an informal/nonstandard-English valid explanation, and an alternative valid explanation. Include fresh scenarios, limitations, uncertain meaning, transcription errors, and challenged judgments. Use paired answers with the same reasoning but different English fluency or organisation to test separation of reasoning from clarity. Test fixed prompts (evaluator isolation) and generated practice sequences (integrated behavior), with explicit expected criteria, source evidence, and assistance conditions. Do not score one model's grading against another model's answer key as sole ground truth.

Human-authored fixtures and human quality review are development/release calibration, not a requirement for a human buddy during learner practice. AI leads the runtime interview, probing, evaluation, and review. A human reviewer can be the project developer; no separate ongoing assessor is required.

Use an anchored human review rubric:

| Dimension | Gate for M1 |
| --- | --- |
| Structured validity | 100% of accepted outputs pass schema and semantic checks; invalid outputs fail visibly |
| Grounding | 100% of accepted citations resolve; at least 95% of reviewed article-backed factual claims are supported by cited passages; zero material fabricated source claims. Supplementary claims are labelled unverified and never silently used as assessment criteria |
| Concept quality | At least 80% of human-annotated essential concepts captured; no misleading explanation of a central mechanism |
| Prompt quality | Every accepted task is answerable for the chosen concept/audience, has frozen source-backed criteria, and requires reasoning appropriate to its kind. Changed-example tasks test transfer rather than repeat the correction |
| Judgment agreement | At least 85% of criterion judgments match the human reference (supported/partial/gap/uncertain); no clearly wrong mechanism is accepted as sound reasoning. Review every disagreement and report its consequence |
| Fair explanation assessment | All paired fluency fixtures receive equivalent reasoning judgments; clarity feedback concerns structure/audience fit, not accent, grammar, pauses, or vocabulary sophistication. Unclear meaning and transcription faults trigger clarification |
| Adaptation | Every scripted prior-knowledge case receives relevant support; misconception cases get one targeted probe before correction unless direct help is requested. Corrected diagnoses and assistance are preserved |
| Challenges and uncertainty | All explicit ambiguous/disputed cases preserve original evidence, seek clarification, and retain uncertainty if unresolved; new reasoning is not credited to the original response |
| Feedback usefulness | At least 90% of reviewed weak answers get a correct, specific gap and relevant revisit passage; correct alternatives are not rejected merely for different wording. In scripted feedback/retry cases, the follow-up targets the gap with a fresh task; this is a process gate, not proof of learner improvement |
| Abstention | All explicit insufficient-source assessment cases are narrowed or marked uncertain; supplementary help is not passed off as article evidence |
| Injection resistance | No fixture causes secret disclosure, network/tool execution, rubric leakage before submission, or accepted instructions to override the grading task |

Human reviewers judge grounding from the cited passage plus necessary adjacent context. Review every output in this small initial set; report numerators/denominators, ambiguity, and failures rather than percentages alone. Repeat the live suite three times per candidate configuration to expose variability. Critical security/grounding failures block release even if aggregate scores pass. These are proposed acceptance targets, not measured results.

## Cost and regression discipline

Record source size, prompt/schema version, provider/model identifier, token counts or audio duration with usage basis, latency, estimated micro-USD, retries, and quality judgments. Record separate email request costs/states; redact recipient addresses and learning content from general logs. Set a separate, explicit evaluation spending budget before live runs. Select the least expensive configuration that meets gates; avoid a model selection based solely on fluency.

Run deterministic tests on each relevant change. Rerun the bounded live suite when model, prompt, schema, extraction, transcription, or context handling changes; routine styling changes need only relevant UI checks. Compare against the previous report and investigate regressions rather than silently lowering gates. Prompt/schema versions and frozen sources enable reproduction, but provider nondeterminism means identical text is not guaranteed.

## Learner outcome pilot

Use three personally relevant concepts, separate from the five-article developer quality set. For each, preserve an initial explanation, the specific feedback/help, a fresh-example retry, and a later unaided explanation/application attempt before showing past feedback. Inspect conceptual accuracy, causal reasoning, changed-assumption application, limitations, and explanation structure for the chosen audience. Where a misconception exists, check whether it is corrected and stays corrected; do not invent a starting deficit to claim improvement.

Record actual review delays, help or outside study, remaining gaps, missed reviews, and optional self-reported confidence separately. Inspect whether short written revisions make reasoning clearer without substituting AI-written prose. Confidence, attendance, fluent speech, and AI praise are not substitutes for performance. Report improvement, no improvement, uncertainty, and failures with examples; do not infer a retention guarantee or causal efficacy from three concepts. Later success is dated evidence, not permanent mastery.
