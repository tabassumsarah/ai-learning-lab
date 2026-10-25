# Minimal database schema

This is a proposed logical SQLite schema, not an applied migration. IDs are application-generated UUID text; timestamps are UTC ISO 8601 text. JSON columns are validated with Zod before persistence. Enable `PRAGMA foreign_keys = ON` on every connection; SQLite foreign key enforcement is connection-specific ([SQLite documentation](https://www.sqlite.org/foreignkeys.html)).

| Table | Columns and constraints |
| --- | --- |
| `sources` | `id` PK; `requested_url`, `final_url`, `title`, `content_text`, `content_sha256`, `extractor_version`, `fetched_at` NOT NULL. Immutable once accepted. |
| `passages` | `id` PK; `source_id` FK sources; `ordinal`, `start_offset`, `end_offset`, `text` NOT NULL; UNIQUE(source_id, ordinal). Offsets are Unicode code-point offsets in normalized content, start inclusive/end exclusive. |
| `sessions` | `id` PK; `source_id` FK sources UNIQUE; `status` CHECK (`source_ready`, `exploring`, `assessing`, `submitted`, `complete`); `budget_usd_micros` nonnegative; `assisted` integer CHECK 0/1; `created_at`, `updated_at`. |
| `concepts` | `id` PK; `session_id` FK sessions; `name`, `explanation`, `prerequisites_json`, `passage_ids_json` NOT NULL. |
| `messages` | `id` PK; `session_id` FK sessions; `ordinal`, `role` CHECK (`user`, `assistant`); `content`, `passage_ids_json`, `created_at`; UNIQUE(session_id, ordinal). Only accepted tutor responses are assistant messages. |
| `assessments` | `id` PK; `session_id` FK sessions UNIQUE; `status` CHECK (`draft`, `submitted`, `evaluated`); `created_at`; nullable `submitted_at`. One assessment per MVP session. |
| `questions` | `id` PK; `assessment_id` FK assessments; `ordinal` CHECK 1–5; `kind`, `prompt`, `concept_ids_json`, `rubric_json`, `passage_ids_json`; UNIQUE(assessment_id, ordinal). Rubric has exactly two criteria, each with concept mapping and evidence. Frozen at creation. |
| `answers` | `question_id` PK/FK questions; `content`, `updated_at` NOT NULL. Editable until submission, then immutable. |
| `evaluations` | `id` PK; `assessment_id` FK assessments UNIQUE; `result_json`, `evaluator_version`, `created_at` NOT NULL. Result holds five question IDs, two criterion judgments each, feedback, evidence, ambiguity flags, and derived scores. Immutable accepted result. |
| `ai_operations` | `id` PK; `session_id` FK sessions; `idempotency_key` UNIQUE; `task` CHECK (`concepts`, `tutor`, `questions`, `evaluate`); `status` CHECK (`pending`, `succeeded`, `failed`, `interrupted`); `input_hash`, `prompt_version`, `schema_version`, `created_at`; nullable `completed_at`, `error_code`. |
| `ai_calls` | `id` PK; `operation_id` FK ai_operations; `attempt` positive integer; `provider`, `model`, `pricing_json`, `reserved_usd_micros`, `status`, `started_at`; nullable `provider_request_id`, `input_tokens`, `output_tokens`, `estimated_cost_usd_micros`, `finished_at`, `error_code`; `usage_basis` CHECK (`reported`, `estimated`, `unknown`); UNIQUE(operation_id, attempt). Cost arithmetic uses integer micro-USD, rounded upward. |

Use NOT NULL for required fields described above, CHECK constraints for nonnegative usage/costs and ordered offsets, and indexes on child foreign keys. `ai_calls.status` uses `pending`, `succeeded`, `failed`, or `unknown`. `pricing_json` freezes currency, per-token rates, pricing date, and any supported cached-token rates. Initially avoid provider features with unsupported billing units.

Relations: source → passages and one session; session → concepts/messages/one assessment/AI operations; assessment → five questions/one evaluation; question → one answer; AI operation → individual provider attempts. Child FKs use ON DELETE CASCADE. Deleting a source is the session deletion operation; run it transactionally and prohibit deletion while calls are active. No user table is required for one local learner.

JSON keeps the formative rubric small without a large grading schema. Application transactions must enforce membership: cited passages belong to the session's source, mapped concepts belong to that session, evaluation question IDs match exactly, and each criterion score is in 0–2. The database cannot enforce JSON references as foreign keys. Normalize these relations if reporting or integrity requirements grow.

Transitions and atomicity:

- Failed URL fetching/extraction creates no accepted source; return a structured error. Accepted source, passages, and session are written together.
- Accepted concept generation writes 3–8 concepts and advances `source_ready → exploring` atomically.
- Assessment creation writes exactly five validated questions and advances `exploring → assessing` atomically. Never persist a partially valid assessment.
- Submission verifies five nonblank answers and freezes them with `assessing → submitted` in one transaction. Retry grading against those exact answers.
- Evaluation inserts one validated result and advances `submitted → complete` atomically. A failed evaluation leaves the submitted attempt intact.
- Record each AI attempt even when it fails. Persist operation completion and domain results in one transaction. Use a partial unique index allowing only one pending operation per session, plus transactional reservations for local daily and session caps.
- A repair attempt belongs to the original operation but has its own call row. A user retry after failure uses a new operation/key, linked in request metadata if needed.

No dashboard table: derive views from frozen questions, answers, evaluation, concept mappings, and usage. This avoids stale duplicated scores. Future repeat attempts can remove the unique session-assessment constraint and introduce explicit attempt numbers.
