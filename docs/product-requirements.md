# Product requirements

## Purpose

Help a learner explain and apply emerging AI ideas through source-grounded dialogue, reasoning exercises, and actionable feedback. Completing an article summary is not evidence of understanding.

## MVP journey

1. Submit a public technical article URL. Show extraction progress, errors, and the estimated AI cost before sending content to the provider.
2. Review the extracted title, source URL, readable content, and numbered source passages. Confirm that the extraction is usable before analysis. Reject unsupported or incomplete content with a useful explanation.
3. Explore 3–8 key concepts, each with a concise explanation, prerequisite notes, and clickable source passages. Ask follow-up questions and request examples. Distinguish source-supported statements from illustrative examples and state when the article cannot answer a question.
4. Start an assessment with exactly five questions: one concept explanation, one mechanism explanation, one comparison/trade-off, one practical application scenario, and one critique/limitation question. All are open-ended; at least three explicitly require reasoning. Include a small implementation or debugging scenario without executing submitted code. Freeze questions and hidden rubrics before answering.
5. Save draft answers, then explicitly submit all five nonblank answers. Evaluate against the frozen article and rubric. Do not reveal model answers or private rubric details before submission. Results are formative feedback, not a certified mastery score.
6. See a dashboard with per-question scores, demonstrated understanding, missing or incorrect ideas, supporting passages, and specific revisit actions. Show which concepts were assessed, missed, or unassessed. Resume the journey after a reload.

## Scope and behavior

- Single local learner; one source per learning session. Persist article snapshots, concepts, dialogue, assessments, answers, feedback, and AI usage.
- Tutor answers use only this session's article and conversation; no browsing or tools. If the source is insufficient, say so and suggest a narrower question.
- Tutor help remains available during assessment, with a visible “assisted practice” label if used after assessment starts. Do not claim independent mastery.
- Display running estimated USD spend by operation and session, token usage when provided, and incomplete/unknown usage explicitly. Allow a session spending cap; do not silently retry paid requests.
- Accessible keyboard navigation, labelled controls, readable code blocks, clear loading/error states, and responsive layouts.
- Failed AI operations remain retryable without losing prior work. Invalid model output never becomes accepted learning content.

## Non-goals

GitHub repository ingestion, PDFs, paywalls, login-protected or JavaScript-only pages, multi-source research, autonomous agents, remote hosting, multiple users, spaced repetition scheduling, vector search, and code execution are deferred. A question about code can be answered as text.

## Success criteria

- A supported article completes the full URL → exploration → five answers → feedback journey and survives reload.
- Every accepted explanation, concept, question rubric, and evaluation references valid passages in the frozen source. Unsupported conclusions are flagged rather than presented as facts.
- Feedback identifies a concrete gap and a corresponding revisit passage for each weak answer; unassessed concepts are not marked understood.
- All release gates in [testing and evaluation](./testing-and-evaluation.md) pass.
- In a pilot with five representative articles, the learner can explain one previously missed concept after revisiting feedback. Record this as qualitative evidence, separately from test scores.
