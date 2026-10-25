# Product requirements

Status: revised after the requirements interview. OpenAI is selected as the learning AI provider. Architecture, the exact model, transcription/email providers, detailed scheduling rules, and cost limits remain proposed for review; this document does not authorize implementation.

## Purpose and evidence of learning

Help one learner strengthen reasoning, explain emerging AI ideas clearly to others, and develop confidence grounded in demonstrated understanding. Short written explanations build toward future blog writing. Completing a summary, recalling terminology, sounding fluent, or receiving a high AI score is not sufficient evidence of learning.

Meaningful learning includes explaining a mechanism, applying it when an assumption changes, and recognising a limitation. Distinguish improvement with help, an unaided changed-example attempt, and a later unaided review. These are observations about particular attempts, not certified or permanent mastery. Record optional self-reported confidence separately from demonstrated reasoning.

## MVP journey

1. Submit a public technical article URL. Show extraction progress and errors. Review its title, source URL, readable content, and numbered passages; confirm extraction before paid analysis. Show provider disclosure and estimated cost before sending content.
2. Explore a small set of source-backed concepts and choose one. The AI asks for a brief explanation of prior knowledge and, where needed, a targeted follow-up. Its starting-level judgment is provisional and correctable by the learner.
3. Choose an audience, defaulting to a technically curious software colleague unfamiliar with the topic. Answer a focused AI prompt by speaking or typing. Let the learner correct transcription errors before explicit submission. Aim for a 10–15 minute initial practice loop, with save and resume.
4. The AI listens to the complete explanation before responding. It probes reasoning with a why/how question or changed assumption. If there is a misconception, offer one targeted question before a direct explanation, unless the learner asks for the explanation immediately.
5. AI assessment identifies sound reasoning, specific gaps, evidence, and a next action. Assess reasoning separately from explanation clarity. Keep expected answers and private criteria hidden before submission. Let the learner challenge feedback; ask for clarification and preserve both original and revised judgments. Unresolved ambiguity stays uncertain.
6. After help, ask for a fresh explanation or changed application example. Record what help was available. An immediate repetition of the correction is limited evidence; do not label it independent understanding. Optionally practise a short written passage in the learner's own words, revising reasoning and organisation before offering a sample rewrite.
7. Save attempts and feedback, choose the next concept review date, and schedule one email reminder. The home view shows due/overdue concepts and attempt evidence. At a later review, ask an unaided explanation or application question before showing earlier answers or feedback. Reload restores the journey.

## Assessment and adaptation

- Practice and assessment are AI-led. No human practice buddy is needed. Separate tutor and evaluator responsibilities and instructions; neither is assumed infallible.
- Reasoning feedback covers conceptual accuracy, causal explanation, application, and limitations. Accept equivalent explanations and justified critique rather than matching wording.
- Explanation-clarity feedback covers logical order, explicit connections, useful examples, and suitability for the chosen audience. Grammar, accent, pauses, vocabulary sophistication, and English fluency do not lower reasoning judgments. Ask when meaning is unclear rather than infer a misconception.
- Adapt questions and prerequisite help using prior attempts for the selected concept and relevant session context. Keep the provisional basis visible and let the learner correct it. Do not infer a stable learner level from one answer or unassessed concepts.
- Keep article claims distinct from illustrative scenarios and supplementary prerequisite explanations. The tutor may explain prerequisites beyond the article, clearly labelled as supplementary and not externally verified. They do not silently become assessment criteria. If a fair judgment needs unsupported knowledge, narrow the question or mark it uncertain. Provider-generated knowledge is not independent verification.
- Evidence descriptions remain tied to the attempt, task, assistance, and date. No aggregate numerical score or permanent “understood” label is required.

## Reinforcement and reminders

- Reviews target concepts, not entire article assessments, and require explanation or application before rereading feedback.
- Use a simple visible schedule that adapts to unaided reasoning and assistance; successful unaided reasoning lengthens intervals, while misconceptions or substantial help shorten them. Let the learner override the date. Tomorrow, three days, and a week are illustrative starting intervals, not settled rules or a retention guarantee.
- Schedule one email for the next review. Cancel or replace it when the date changes or the concept is reviewed early. Missed reviews remain overdue in the app; repeated overdue messages and SMS are deferred.
- Reminder emails contain only a short concept title and a prompt to practise, never answers, scores, or corrections. Email reaches the learner while the app is closed; practice still requires opening the local app on the laptop. Do not promise an internet-accessible practice link.
- Show scheduling/cancellation failures and allow explicit retry. A reminder failure must not lose learning progress. Precise scheduling rules, provider, delivery time/time zone settings, and costs must be resolved before implementation.

## Scope and behavior

- Single local learner, one immutable article snapshot per learning session, with repeatable concept attempts across days. Persist concepts, dialogue, prompts, drafts, submitted responses, assistance, feedback revisions, review state, and external-operation usage.
- Spoken and typed answers use the same reasoning criteria. Use turn-based recording and transcription, not live voice conversation. Discard app-held audio after transcription or failure; retain corrected transcripts. Disclose external audio processing and provider retention separately; local deletion is not a claim about provider deletion.
- No model browsing or tools. Application services fetch articles, transcribe audio, and send reminders through explicit boundaries.
- Display estimated USD spend by operation and session, reported/estimated/unknown usage, and configurable caps. Include transcription and disclose email cost separately. No silent paid retries.
- Accessible keyboard navigation, labelled controls, readable code blocks, clear loading/error states, and responsive layouts. Text input remains available if recording fails or is unsuitable.
- Invalid model output never advances learning state. Failed external operations remain retryable without losing prior work.

## Non-goals

GitHub repository ingestion, PDFs, paywalls, login-protected or JavaScript-only pages, multi-source research, autonomous agents, remote hosting, multiple users, vector search, code execution, mandatory five-question assessments, aggregate score dashboards, comprehensive article coverage, full blog drafting, pronunciation/English coaching, retained audio playback, live voice conversation, SMS, and repeated overdue notifications are deferred. Code scenarios may be discussed as text.

## Success criteria

- A supported article completes URL → source review → one concept → prior-knowledge probe → spoken or typed explanation → feedback → changed-example retry → scheduled email → later unaided review. Work survives reload and retry.
- Every article-backed claim and assessment criterion cites valid supporting snapshot passages. Supplementary explanations are visibly distinct; unsupported or ambiguous judgments are flagged.
- Weak explanations receive a specific reasoning gap and a relevant passage/action; sound informal explanations are accepted. Explanation structure is assessed without English-fluency penalties.
- The learner can challenge feedback, see assistance recorded, and inspect dated evidence rather than a blanket mastery claim.
- All release gates in [testing and evaluation](./testing-and-evaluation.md) pass.
- In a pilot across three personally relevant concepts, inspect whether feedback corrects a misconception and enables reasoning on a fresh example and a later unaided review. Record remaining gaps, review attendance, and optional confidence separately. Session completion and AI praise alone do not establish success.
