# Domain docs

Use a single-context layout:

- `docs/GLOSSARY.md`: shared domain vocabulary, when useful.
- `docs/adr/`: explicitly approved architecture decision records, when useful.
- Other technical documentation stays under `docs/`.

Read relevant existing design documents listed in `AGENTS.md` before planning or implementing changes. They are the current design baseline; preserve their stated approval status. Extend them rather than duplicating or replacing them unnecessarily, and identify inconsistencies between new proposals and existing decisions.

Before exploring an area, read the glossary and relevant ADRs when they exist. Proceed if they are absent. Keep both optional until they provide real value. Proposed architectural choices require explicit approval before being recorded as final ADRs.

Use glossary terms consistently in code, issues, and documentation. Surface conflicts with existing ADRs explicitly before changing course.
