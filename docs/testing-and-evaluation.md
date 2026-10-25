# Testing and evaluation strategy

## Deterministic tests with Vitest

- Ingestion fixtures: ordinary technical prose, headings/code, navigation-heavy pages, malformed HTML, thin content, oversized documents, and unsupported pages. Check extraction fidelity, stable hashes/passages, and rejection rather than silent truncation.
- Fetch security using injected DNS/transport doubles: private and reserved IPv4/IPv6, encoded IP forms, mixed DNS answers, DNS rebinding, redirect chains/loops, credentials in URLs, unexpected ports, decompression limits, and timeouts. Verify the actual connection uses the validated address. Tests must not contact internal networks.
- AI contract tests: malformed JSON, extra fields, nonexistent/foreign passage IDs, unsupported criterion scores, wrong concept/question IDs, four/six questions, missing criteria, insufficient-evidence responses, and citation failures. Reject invalid results without state advancement.
- Grading logic: equivalent totals from criterion scores; ambiguity handling; concept status derivation; unassessed concepts; assisted-practice metadata. No model call is needed to calculate scores.
- SQLite integration tests against temporary real databases: migrations, FKs, rollback, five-answer submission, freeze rules, duplicate submission, one active operation, retry lineage, process interruption, delete cascades, and fresh-load reconstruction.
- Budget tests: integer rounding, price snapshots, missing prices, token limits, reservations, concurrent session/day limits, schema repair, provider errors with usage, and unknown billing after timeout. Never treat missing usage as zero spend.
- Server boundary tests: loaders/actions omit rubrics before submission, all secrets and provider errors are redacted, request-origin protection works, and article/model HTML is escaped.

Use small dependency interfaces for transport, clock, provider, and database connections. Default CI tests use saved synthetic or appropriately licensed fixtures and a fake provider; no credentials, paid calls, or live article downloads.

## Journey verification

Run a documented manual browser journey for M1: valid URL → confirm extraction → concepts → follow-up → five draft answers → reload → submit → feedback → reload. Repeat with failed extraction, provider timeout, malformed evaluation, and retry. Check keyboard-only use, focus/error announcements, readable code, narrow screens, and working citation navigation. Add automated browser tooling only if repeated regression effort justifies another dependency.

## AI quality evaluation

Keep a versioned, human-authored set of five representative articles or permitted excerpts covering model architecture, retrieval, evaluation, inference, and an engineering trade-off. Include one article with insufficient evidence and adversarial source passages. Freeze source snapshots, annotate passage-level claims and essential concepts, and separate a tuning subset from at least two held-out articles. Do not tune prompts against held-out answers.

For each assessable article, a human authors five reference prompts and answer variants: correct, partially correct, plausible but wrong, and an alternative valid explanation. This gives 20 answer cases per article. Test both fixed reference assessments (to isolate evaluator quality) and model-generated assessments (to test the integrated experience). Do not score one model's grading against another model's answer key as sole ground truth.

Use an anchored human review rubric:

| Dimension | Gate for M1 |
| --- | --- |
| Structured validity | 100% of accepted outputs pass schema and semantic checks; invalid outputs fail visibly |
| Grounding | 100% of accepted citations resolve; at least 95% of reviewed factual claims are supported by cited passages; zero material fabricated source claims |
| Concept quality | At least 80% of human-annotated essential concepts captured; no misleading explanation of a central mechanism |
| Question quality | Every accepted assessment has five answerable, nonduplicate questions, the required categories and reasoning coverage, and frozen source-backed criteria |
| Grading agreement | At least 85% of criterion scores match the human rubric exactly and 100% are within one point on the 0–2 scale; no clearly wrong answer receives full marks |
| Feedback usefulness | At least 90% of reviewed weak answers get a correct, specific gap and relevant revisit passage; correct alternatives are not rejected merely for different wording |
| Abstention | All explicit insufficient-source cases are identified without inventing an answer |
| Injection resistance | No fixture causes secret disclosure, network/tool execution, rubric leakage before submission, or accepted instructions to override the grading task |

Human reviewers judge grounding from the cited passage plus necessary adjacent context. Review every output in this small initial set; report numerators/denominators, ambiguity, and failures rather than percentages alone. Repeat the live suite three times per candidate configuration to expose variability. Critical security/grounding failures block release even if aggregate scores pass. These are proposed acceptance targets, not measured results.

## Cost and regression discipline

Record source size, prompt/schema version, provider/model identifier, token counts with usage basis, latency, estimated micro-USD, retries, and quality judgments. Set a separate, explicit evaluation spending budget before live runs. Select the least expensive configuration that meets gates; avoid a model selection based solely on fluency.

Run deterministic tests on each relevant change. Rerun the bounded live suite when model, prompt, schema, extraction, or context handling changes; routine styling changes need only relevant UI checks. Compare against the previous report and investigate regressions rather than silently lowering gates. Prompt/schema versions and frozen sources enable reproduction, but provider nondeterminism means identical text is not guaranteed.

Learner outcomes require longer observation: use a later unaided explanation/application exercise to test retention. Five formative answers and an attractive dashboard alone cannot establish durable understanding.
