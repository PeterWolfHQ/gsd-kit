---
name: setup
description: One-time setup of a fresh GSD work repo after cloning the kit. Cuts the push link to the kit, creates LOCAL.md, picks the sweep transport, and walks through a first sweep and a first capture. Use when the user types /setup.
---

# Setup

You are the Setup Agent. Turn a fresh clone of the kit into the user's own work system. Every step is safe to repeat: check first, change only what is not already done. `AGENTS.md` is canon.

## Procedure

1. **Cut the push link to the kit.** Run `git remote -v`.
   - If there is a remote named `origin` and none named `kit`: `git remote rename origin kit`.
   - Then `git remote set-url --push kit DISABLED`.
   - Run `git remote -v` again and confirm the `kit` line marked `(push)` reads `DISABLED`. From now on kit updates arrive with `git pull kit main` and nothing can be pushed back.
   - If there is no remote at all, skip this step and say so.

2. **Create `LOCAL.md`.** If it does not exist, create it with the exact contents of `LOCAL.example.md`. If it exists, leave it alone.

3. **Pick the transport.** Look at the tools available to you for one that reaches Microsoft 365 (Work IQ).
   - None: keep `transport: paste`. This is the normal case.
   - One exists: ask the user whether to try it. On yes, ask it "What is on my calendar tomorrow?" If it answers, set `transport: workiq` in `LOCAL.md`; if it fails, keep `paste` and note the error.

4. **Priorities.** Ask the user for one to three current work priorities, in their own words, and wait for the answer. They may skip. Write what they give under `## Priorities` in `LOCAL.md`.

5. **First sweep.** Tell the user to flag one or two emails in Outlook first if none are flagged, and go straight on without waiting: open `.github/skills/sweep/SKILL.md` and follow it to the end. The sweep pauses for a paste; when it has finished, come back here and continue with step 6.

6. **First capture.** Ask the user for one real thing that is on their mind. Capture it by following `.github/skills/capture/SKILL.md`, then follow `.github/skills/process/SKILL.md` so they see an item travel from inbox to a decision.

7. **Write the setup notes.** Under `## Setup notes` in `LOCAL.md`, record, one line each:
   - today's date, and the agent and model you are, if you know
   - the transport chosen, and why
   - whether `/setup` appeared in the chat's command menu or had to be typed (ask the user)
   - anything that went wrong in the first sweep (format drift, a part Copilot could not do)

8. **Commit.** `git add LOCAL.md`, then commit: `setup: done`. If git refuses for lack of a name or email, ask the user for the ones to use and set them for this repo only with `git config user.name` and `git config user.email`.

9. **Hand over.** Print this card and nothing after it:

   ```
   You're set up.

   /capture <anything>   get it out of your head
   /sweep                flagged mail and Teams asks into the inbox
   /process              inbox to zero
   /next                 what to do right now
   /agenda <name>        before a 1:1
   Friday: /calsweep, then /review
   ```

## Hard limits

- Never push, and never re-enable pushing to the kit.
- Never overwrite an existing `LOCAL.md`.
- Sweeps stay read-only, as everywhere else.
