---
name: interview-read
description: Reads one interview transcript where the user is the candidate, logs the notable moments, and matches them to a standing set of coaching patterns. Run after every interview-type call.
---

# Interview Read

Every interview call is read once and does two jobs: it logs the notable moments from that specific call, and it updates the standing set of coaching patterns those moments support. The output feeds an "Interview Read" view: a synthesis of what the candidate keeps doing well, what keeps tripping them up, and one concrete thing to try next. It is not a transcript archive.

## Data model

Three tables (or three tabs in a spreadsheet):

- `moments`: one row per notable exchange. `date`, `company`, `role`, `interviewer`, `stage`, `moment`, `how_answered`, `what_worked`, `what_was_weak`, `pattern_id`.
- `patterns`: `id`, `category` (strength | improvement | experiment), `label`, `description`, `direction` (new | recurring | improving | resolved), `user_feedback` (the candidate's own reaction, never written by this skill).
- `processed`: one row per transcript already read, so nothing is read twice.

## Scope filter

Only calls where the user is the candidate being evaluated: recruiter screens, hiring-manager conversations, panels, case studies, founder conversations inside a hiring process. Skip internal meetings, calls where the user is evaluating someone else, and networking calls with no evaluative component. If the call can't be tied to a specific company and role, skip it and say why.

## Procedure

1. Check the transcript against `processed`. Never read one twice.
2. Load every existing pattern.
3. Extract moments.
4. Match each moment against the patterns.
5. Write: new patterns first (capture ids), then moments, then the processed row.
6. Report.

## Extraction

One moment per genuinely notable exchange, not a full transcript walk. Aim for one to four per call. Eight or more means the bar is too low. A moment is notable when it is a real test of the candidate: a hard question, a place they clearly nailed or fumbled an answer, a moment that reveals how they handle pushback or ambiguity. Small talk, scheduling, and the interviewer narrating the company are not moments.

Only the candidate's own lines may be captured if the transcript came from their recorder. Infer the interviewer's question from the answer when needed and say so.

For each moment: `moment` (the question or situation, one clean sentence), `how_answered` (what they actually said, briefly), `what_worked` (specific, or blank), `what_was_weak` (specific, or blank). A moment can have both, either, or neither. Leave blank rather than pad.

## Matching against patterns (the most important rule)

Under-creating patterns is the goal. A pattern is a real, repeatable behavior, not a one-off anecdote wearing a label.

1. For each moment, ask: does this support an existing pattern's label and description, the same underlying behavior and not merely a similar topic? If yes, attach it. Do not create a new one.
2. Create a new pattern only when the moment reveals a behavior that isn't already named. `category` is "strength" if it worked and is worth repeating, "improvement" if it is a recurring friction point, "experiment" only when proposing something concrete and untried, and rarely. `label` is short and behavior-named ("Leads with setup before the point", not "Communication"). `description` is one coaching sentence in second person, written as a read: "Your strongest example often arrives after too much setup." `direction` starts as "new".
3. When a moment matches an existing pattern that already has prior linked moments and its direction is "new", move it to "recurring". Never touch a pattern whose direction is "improving" or "resolved"; that judgment belongs to the candidate, or to a later read across multiple calls.
4. Never write `user_feedback`. Never flip a pattern to "resolved". Those are the candidate's controls.
5. Ambiguous match: do not create. Attach to the closest existing pattern and flag the judgment call in the report. A false merge is cheaper to undo than a duplicate pattern diluting a real signal.

## Rules

- Never invent comp, outcome, or next-step details that aren't in the transcript.
- A call with zero qualifying moments still gets a processed row.
- No em dashes in anything written.

## Report, in this order

1. Calls processed: company, role, date, moments extracted.
2. New patterns created: label, category, the moment that prompted it.
3. Existing patterns reinforced: label, which call, one line on why it matched.
4. Direction changes: new to recurring only. Anything else is flagged, not changed.
5. Skipped calls and why.
6. Ambiguous matches worth the candidate's eyes.
7. If nothing new, say so in one line and skip the rest.
