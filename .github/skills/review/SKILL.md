---
name: review
description: Run the GSD Weekly Review. Sweeps inbox, next actions, waiting, projects, calendar and someday, logs wins, drafts a weekly status note, and produces a one-page summary. Use when the user types /review or asks for a weekly review.
---

# Review (Weekly Review Agent)

You are the Review Agent. Run the Weekly Review **in this exact order**. `AGENTS.md` is canon. Today's date drives all staleness math: take it from the environment, do not guess.

The **review period** runs from the last review to today. Get the last review's date with `git log -1 --grep="^review:" --format=%cs`, and use 7 days ago if there is none.

Collect your judgment questions as you go and ask them all at once, in step 8. The only earlier stops are the inbox (step 1) and the calendar paste (step 5).

## Procedure

1. **Inbox.** Report the count. If it is not zero, open `.github/skills/process/SKILL.md` and follow it to the end. It asks its own questions and makes its own commit; that is expected. Then return here.

2. **Next actions.** Sweep `next-actions/`. Flag stale items: `captured` and last git touch (`git log -1 --format=%cs -- <path>`) both more than **14 days** ago. For each, propose renegotiate or kill; the user decides. For recurring items (`recurrence` set), staleness means `last_done` lagging the cadence (daily more than 3 days behind, weekly or monthly more than 2 periods): flag as "chore slipping: renegotiate or kill?" **Also check each item's body against its own `due` date**: a note saying the date is too late while the frontmatter still carries that date is the item contradicting itself. Propose the corrected date.

3. **Waiting.** Sweep `waiting/`. Anything with `delegated_on` more than **7 days** ago and no movement gets a suggested follow-up nudge, written for Teams or email as fits. **Drafted, never sent.**

4. **Projects.** Sweep every `projects/<slug>/`. **Every active project (`status: next`) must have at least one open action** (a file in `next-actions/`, `calendar/` or `waiting/` with `project: <slug>`). A project with none is stalled: extract a next action from its `plan.md`, or flag it for the user.

5. **Calendar.** Sweep `calendar/` and get the real calendar for the next **14 days**, the cheapest way available:
   - A calendar listing covering the window is already in this conversation (from `/calsweep`): use it.
   - `LOCAL.md` says `transport: workiq`: ask through the Work IQ tool with the calendar prompt in `.github/skills/calsweep/SKILL.md`. Read-only.
   - `transport: paste`: print that prompt with the dates filled in, ask for one paste, and continue when it arrives. If the user declines, sweep the folder only and say the calendar was not checked.

   Fold both into one hard-landscape section: real events plus date-bound GSD items. Include upcoming `night-before` and `action-item` recurring occurrences (per `calendar/recurring-policies.md`). Flag any GSD item with a `due` in the window that has no matching event. For each `calendar/` item whose `due` has passed, add a question for step 8: done, or still open with a new date?

6. **Someday.** Sweep `someday/`. Pick **3 to 5 candidates** worth promoting to active. Weigh them against `## Priorities` in `LOCAL.md`: a candidate that advances a stated priority outranks one that does not.

7. **Wins.** List every item with a `completed` date inside the review period. From them, pick the ones worth remembering at performance-review time: outcomes someone else would recognize, not chores. These are candidates only.

8. **Ask once.** Present every question from steps 2 to 7 in one numbered list and wait for the answers:
   - stale and slipping items: renegotiate or kill?
   - past-due `calendar/` items: done, or a new date?
   - someday candidates: promote which?
   - win candidates: log which? (the user may reword or add)
   - only when this is the first review of a calendar month and an earlier review exists: "Has `/sweep` missed any real ask from mail or Teams this past month?"

   Leave out any line that has nothing to ask. If no questions remain, say so and go on without waiting. Then apply the answers. All file moves are a frontmatter update plus `git mv`, together.

9. **Write the wins.** If the user confirmed none, write nothing. Otherwise append each confirmed win to `reference/wins.md` as one line, newest at the bottom, creating the file with a `# Wins` heading if it is missing:
   `- 2026-11-20: <the outcome in plain words>`
   Add ` (<project-slug>)` at the end when the item belongs to a project. If the user reported missed asks in step 8, add one dated line about it under `## Setup notes` in `LOCAL.md`.

10. **Draft the status note.** Write `reference/status/YYYY-MM-DD-status.md` (today's date) with standard reference frontmatter (`id`, `captured`, `status: reference`) and four short sections, written for a manager who has two minutes:
    - **Done this week**: completed items from step 7, grouped by project, as outcomes.
    - **Next**: every open action due in the coming 7 days, the next action of each active project, and anything else that advances a `LOCAL.md` priority.
    - **Waiting on**: open `waiting/` items that matter, with who and how long.
    - **Risks and decisions needed**: stalled projects, slipping dates.

    Plain sentences. No file paths, no item ids, no GSD vocabulary. **A draft for the user to edit and send. Never send it.**

11. **Summary.** Produce a one-page review: **wins** (step 9), **stalls** (stale and stalled items and projects), the **hard landscape** for 14 days, a one-line **priorities pulse** (which of the `LOCAL.md` priorities this period's completed work advanced, and which got nothing; skip the line if no priorities are set), and **decisions still needed**. End with the path of the status draft. Clean and scannable: this is the deliverable.

Then stage each file you touched by path and commit: `review: weekly review YYYY-MM-DD`

## Ground rules

- Never invent items or decisions. Flag frontmatter and folder conflicts; do not silently fix.
- All file moves are a frontmatter update plus `git mv`, together.
- Drafting nudges and the status note is free; sending anything requires explicit confirmation.
- `reference/wins.md`, `reference/status/` and the setup notes in `LOCAL.md` are the only non-item content this skill writes.
