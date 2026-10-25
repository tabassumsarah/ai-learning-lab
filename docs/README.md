# AI Learning Lab — MVP design

Status: proposed for review. No application implementation is included.

1. [Product requirements](./product-requirements.md)
2. [Architecture and decisions](./architecture.md)
3. [Minimal database schema](./database-schema.md)
4. [First implementation milestone](./milestone-1.md)
5. [Testing and AI evaluation](./testing-and-evaluation.md)
6. [M1 first practice slice specification](./m1-first-practice-slice.md)
7. [Published ticket breakdown for the first practice slice](./m1-practice-tickets/README.md)

Assumptions: one learner, a local Node server, public English-language HTML articles, one configured learning AI provider, turn-based transcription, and scheduled external email reminders. Practice remains local and laptop-based; no human practice buddy is required. “SvelteKit 5” is interpreted as **Svelte 5 with a compatible SvelteKit release**, because the projects have independent version numbers. Exact runtime and package versions will be pinned during implementation after compatibility checks.

The revised baseline incorporates the requirements interview: reasoning and audience-aware explanation, spoken or typed practice, AI-led probing/assessment, fresh-example retries, and concept reviews across days. It supersedes the fixed five-question assessment, article-only prerequisite help, single-attempt schema, and deferral of scheduling. English fluency coaching and full blog drafting remain deferred.

Review decisions: approve the revised architecture and limits/cost controls before application work begins. OpenAI is selected as the learning AI provider. The exact model, transcription/email providers, supported audio limits and retention, review intervals and uncertainty rules, recipient/time zone settings, and evaluation budget remain to be resolved. Provider selection does not approve paid calls or the remaining architecture; no final ADR is created by this revision.
