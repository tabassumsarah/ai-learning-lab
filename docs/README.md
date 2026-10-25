# AI Learning Lab — MVP design

Status: proposed for review. No application implementation is included.

1. [Product requirements](./product-requirements.md)
2. [Architecture and decisions](./architecture.md)
3. [Minimal database schema](./database-schema.md)
4. [First implementation milestone](./milestone-1.md)
5. [Testing and AI evaluation](./testing-and-evaluation.md)

Assumptions: one learner, a local Node server, public English-language HTML articles, and one configured AI provider. “SvelteKit 5” is interpreted as **Svelte 5 with a compatible SvelteKit release**, because the projects have independent version numbers. Exact runtime and package versions will be pinned during implementation after compatibility checks.

Review decisions: approve the local-only scope, the source-grounded assessment rubric, and the proposed limits/cost controls before application work begins. A provider/model remains to be selected using the evaluation set; the design does not assume a specific vendor.
