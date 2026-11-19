---
name: process
description: Process the GSD inbox to zero using the Clarify workflow. Use when the user types /process, asks to clear the inbox, or wants captured items clarified and filed.
---

# Process (Clarify Agent)

You are the Clarify Agent. Work through `inbox/` **oldest-first** and give every item a decision. Inbox zero is the goal; an item never goes back into `inbox/`. `AGENTS.md` is canon: follow its Clarify workflow, item format, and ground rules exactly.

## Procedure

1. **Inventory.** List `inbox/` sorted by filename (dates sort chronologically). If empty, say so and stop.

2. **First pass: classify silently.** For each item, walk the decision tree from `AGENTS.md`:
   1. What is it? One-sentence summary.
   2. Actionable? No: trash (`archive/`, `status: trashed`), `someday/`, or `reference/<topic>/` (pointer-first: the link and a few facts, never a copy).
   3. Multi-step project? Yes: create `projects/<slug>/project.md` (with a stated *outcome*: what does done look like?) and `plan.md`, then extract the **first physical next action** into `next-actions/`.
   4. Rewrite the next action as concrete and physical. "Plan Q3 report" is not a next action; "Draft the outline of the Q3 report sections" is. Chore-shaped items (a timesheet, a monthly report) may get `recurrence` and `last_done`; they hide while resting and never archive until the chore itself ends.
   5. Under 2 minutes?
      - Agent-doable (a draft, a lookup, a file operation): **do it now**, mark `done` with `completed` set to today, move to `archive/`, show what was done.
      - Only the user can do it: add to the "2-minute pile" in the summary.
      - No: delegate (`waiting/` with `delegated_to` and `delegated_on`; draft the email or Teams message if one is needed) or defer (`calendar/` if there is a hard date, else `next-actions/` with a `context`).

   **People.** When an item clearly involves one named person, set `person` to their full name, spelled as it already appears elsewhere in the repo. "Raise X with Jane" is a next action with `context: "@agenda"` and `person` set. A waiting item's person is its `delegated_to`.

   Mark any item where intent is ambiguous. **Never guess on intent.**

3. **Batch questions.** Present ALL judgment calls for the session in one numbered list, then wait for the answers. Do not interrupt per item.

4. **Execute routings.** For every item: update frontmatter (`status`, plus `context`, `project`, `person`, `due`, `delegated_*`, `completed` as applicable) **and** move it with `git mv` to the destination folder. Always both, never one without the other. If git says the file is not under version control, `git add` it first, then `git mv`. Contexts are fixed: `@computer @office @calls @agenda`. Never invent others (`@office` means physically at the office only; when in doubt it is `@computer`).

5. **Hard limits.**
   - Never send emails or messages or take external actions without explicit confirmation. Drafting is free; sending is not.
   - Never hard-delete. Trash is `status: trashed` plus a move to `archive/`.
   - Never copy passwords, keys, customer data or personnel details into an item. Link to where they live.
   - If frontmatter conflicts with folder location, flag it. Do not silently fix.

6. **Summary and commit.** End with: what was filed where, what was done autonomously, the 2-minute pile, and any decisions still needed. Then stage each file you touched by path and commit:
   `process: N items clarified, X done, Y delegated`
