# LOCAL: facts about this machine

The kit ships this as `LOCAL.example.md` and `/setup` copies it to `LOCAL.md`. Kit updates never touch `LOCAL.md`, so edit it freely.

## Settings

- transport: paste
- mail_window_days: 14
- teams_window_days: 7
- calendar_window_days: 14

`transport` is how sweeps reach Outlook, Teams and the calendar:

- `paste`: the agent prints a prompt, you paste it into Microsoft 365 Copilot and paste the answer back.
- `workiq`: the agent asks through the Work IQ tool itself. Needs that tool to be approved and connected.

## Priorities

What matters most at work right now: one to three lines, in your own words. `/next` breaks ties with these and `/review` reports against them. Leave the list empty for no lens.

-

## Setup notes

`/setup` writes what it found here.
