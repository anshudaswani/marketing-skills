---
name: interview-prep
description: Given a job description, the user's FAQ bank, their coaching patterns and recent interview moments, writes the 8 to 12 questions that interview is most likely to ask, with answers in the user's voice. Run before every interview.
---

# Interview Prep

Job description in, likely questions and answers out. The answers are not generic. They come from a standing bank of the questions the candidate keeps getting (with the answer that should have come out), from the coaching patterns the interview-read skill has built up, and from the last forty logged moments.

## Inputs

- The company, role, stage, and a short company blurb.
- The job description, in full. No job description, no prep. Do not guess from a funding announcement.
- `faq_answers`: the standing bank. Each row: `question`, `asked_by` (where it has come up), `what_came_out` (how the candidate has been answering), `better_answer`, `notes`.
- `patterns` and the most recent `moments` from the interview-read skill.
- The candidate's writing-style profile.

## Procedure

1. Start with the FAQ questions the brief makes likely. The usual six: why are you leaving, walk me through your background, comp expectations, the gap question in this role's costume, what would you do if you started Monday, do you actually own the number. Tailor each FAQ answer's final sentence to this company. Keep the rest as written; the bank is the candidate's settled language.
2. Add role-specific questions from the job description and the company: the proof question behind its headline requirement, its named competitor, its buyer, its growth motion, why this company over the others.
3. For the gap question, identify the gap this particular job description exposes and write the three-sentence bridge: name the gap plainly, bridge with the closest real thing from the candidate's history, then say what they'd do in this company's motion. Never answer a mechanics question with adaptability ("I'm a quick learner").
4. For the Monday question, write a hypothesis the interviewer can argue with, not a discovery checklist: one bet, one reason, one thing to check first. End with "tell me where I'm wrong."
5. Include one question the candidate should ask rather than answer, when the brief suggests one: a predecessor who left, an unclear reporting line, a title that doesn't match the scope.
6. Mark each question's source: `faq` (carry the id), `moment` (name the pattern or moment it rests on), or `role`.

## Voice

Short sentences. Plain words. One idea at a time, said once. The point lands in the first line. Specifics over adjectives: numbers, names, tools. At most one contrast pair per answer. No em dashes. Avoid: genuinely, honestly, leverage, unlock, delve, game-changer, agentic.

Answers are 40 to 120 words, spoken length. `why_asked` is one sentence.

## Output

```json
{ "questions": [ { "question": "", "why_asked": "", "suggested_answer": "", "source": "faq|role|moment", "faq_id": null } ] }
```

Ordered as they are likely to come up: FAQ first, then role-specific, the question to ask last.

## After the call

The interview-read skill logs what was actually asked. Any new question, or a sharper answer, goes back into `faq_answers`. The prep is per company. The bank is the source it pulls from.
