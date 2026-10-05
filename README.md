# marketing-skills

Judgment, written down so an agent can run it.

These are the instruction files I use with Claude to do recurring marketing and career work the same way every time. Each one is a `SKILL.md`: a short description of when it applies, then the procedure, the rules, and the output format. They run inside Claude (Cowork, Claude Code, or the API) and most would port to any agent that takes a system prompt.

The point is not the prompts. It's that the decisions are made once, in writing, and then held to.

## The skills

**[interview-read](skills/interview-read/SKILL.md)** reads an interview transcript where you are the candidate and does two jobs: logs the one to four moments that actually tested you, and matches each to a standing set of coaching patterns. The hard rule is to under-create patterns. A behavior earns a name when it shows up across calls, not once.

**[interview-prep](skills/interview-prep/SKILL.md)** takes a job description plus your FAQ bank, your patterns and your recent moments, and writes the eight to twelve questions that interview is most likely to ask, with answers in your voice. It identifies the gap this particular role exposes and writes the three-sentence bridge for it.

**[writing-style](skills/writing-style/SKILL.md)** is the profile that keeps drafts sounding like me rather than like a model. Included as a worked example of how to build one: the through-line, hard rules, the words I reach for, and what to avoid sounding like. Replace the specifics with yours.

## Using them

Drop a skill folder into your Claude skills directory, or paste the `SKILL.md` body as a system prompt. Each file says what it needs as input. None of them need a database; the interview skills are written against a simple schema (moments, patterns, a processed ledger) that you can keep in a spreadsheet if you want.

The interview skills run live inside [the-ad-standard](https://github.com/anshudaswani/the-ad-standard), where they're wired to Supabase edge functions.

[Anshu Daswani](https://anshudaswani.com)
