# gsd-kit

A portable Getting Things Done system for work, run by an AI coding agent. Plain Markdown and git, nothing else.

You capture and decide. The agent clarifies, files, surfaces and nags.

This repo is the **kit**: instructions, skills and empty folders. It holds no tasks and no data. You clone it once, and your clone becomes your own private work system.

## What you need

- git
- VS Code with GitHub Copilot in **Agent** mode (pick the strongest model you have)
- For the sweeps: Microsoft 365 Copilot. Without it, everything else still works; you paste things into `/capture` yourself.

## Install

1. Clone this repo into a folder named `gsd`. Keep it **outside** any OneDrive-synced folder; sync tools and git do not mix.

   ```
   git clone <this repo's URL> gsd
   ```

2. Open the `gsd` folder itself in VS Code (the top folder, not a subfolder).
3. In Copilot Chat, in Agent mode, type:

   ```
   /setup
   ```

Setup cuts the link back to this repo for pushes, creates your `LOCAL.md`, and walks you through a first sweep and a first capture.

## Daily use

| When | Type |
|---|---|
| Anything lands in your head | `/capture <whatever it is>` |
| Flags have piled up in Outlook | `/sweep` |
| Inbox has items | `/process` |
| Starting a work block | `/next` (say your context, time and energy) |
| Before a 1:1 | `/agenda <name>` |
| Friday afternoon | `/calsweep`, then `/review` |

If a command does not appear in the chat's command menu, type it anyway. `AGENTS.md` tells the agent what each one means.

## How the sweeps work

Flag an email in Outlook and it means "GSD, take this." `/sweep` prints one prompt. Paste it into Microsoft 365 Copilot, paste the answer back, and the flagged emails and unanswered Teams asks become inbox items, each with a link to its source. `/calsweep` does the same for calendar events that need prep.

Sweeps only read. They never send, reply, or change anything in Outlook, Teams or your calendar.

## The rules that matter

- **Work only.** Personal life stays out.
- **Nothing leaves your machine for this repo.** After setup the `kit` remote cannot be pushed to.
- **Pointer-first.** Items link to the email, thread, notebook or ticket. Passwords, customer data and personnel details are never copied into an item.
- **Nothing is deleted.** Done and trashed items move to `archive/`.

## Updating the kit

```
git pull kit main
```

Kit updates touch `AGENTS.md` and the skills. Your items, `LOCAL.md` and `calendar/recurring-policies.md` are yours and are left alone.

## What's inside

```
AGENTS.md                 the canon: method, item format, rules, command table
LOCAL.example.md          template for your machine's settings and priorities
.github/skills/           one folder per command, each with a SKILL.md
inbox/ next-actions/ waiting/ calendar/ projects/ someday/ reference/ archive/
```
