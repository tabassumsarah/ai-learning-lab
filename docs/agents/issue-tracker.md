# Issue tracker: GitHub

Track work in GitHub Issues for `tabassumsarah/ai-learning-lab`.
Keep architecture decisions and technical documentation in `docs/`.

Use the `gh` CLI from this repository:

- Read: `gh issue view <number> --json number,title,body,labels,comments`
- List: `gh issue list --state open`
- Create: `gh issue create --title "..." --body-file <file>`
- Label: `gh issue edit <number> --add-label "..."`
- Comment: `gh issue comment <number> --body-file <file>`
- Close: `gh issue close <number>`

When a skill says to publish to the tracker, prepare a GitHub issue and show its proposed title and body for approval before creating it.

When a skill says to fetch a ticket, read the relevant GitHub issue.

PRs as a request surface: no.
