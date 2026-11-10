---
name: setup
description: Use when the user runs "/memen:setup" or asks to set up memen with Claude ("set up memen", "start the nightly memen insight"). Checks the memen connection, registers the nightly insight task at 23:00, and writes today's insight card right away so the first one arrives without waiting for the night.
---

# Set up memen

Reply in the user's language. Report each step in one short line as you finish it (done / skipped and why).

## 1. Check the connection

Call memen's `get_day` for today.

- If the memen tools are missing or return an authentication error, stop here and tell the user:
  - Claude Code: in a terminal, run `claude`, open `/mcp`, choose memen, and authenticate. Sign in to memen in the browser and press Allow. Then run `/memen:setup` again.
  - Codex: run `codex mcp login memen`, then run setup again.
- If it fails for another reason (for example an internal error), report the error in one line and continue; the nightly run will read the day again.
- Otherwise report that memen is connected.

## 2. Check the materials

Call `get_ai_work` for today.

- If it returns AI prompts, report that this Mac's AI work is reaching memen.
- If it returns none, tell the user that insights get more concrete when the Memen Mac app sends AI work: open Memen on the Mac and turn on "AI work" (AIでの作業) in the Recording (記録) tab. Do not change the app's settings yourself; this record is off by default and stays the user's choice. Continue either way.

## 3. Register the nightly task

The nightly task runs only in the Claude desktop app (Code tab), through its scheduled-tasks tools (`list_scheduled_tasks`, `create_scheduled_task`).

- If those tools are not available (terminal Claude Code, Codex), skip this step and tell the user: open the Claude desktop app, go to the Code tab, and run `/memen:setup` there to register it. Continue to step 4.
- Call `list_scheduled_tasks`. If a task whose ID or title mentions memen and insight (for example `memen-daily-insight`) already exists, do not create another; report it with its schedule and continue.
- Otherwise call `create_scheduled_task` with:
  - `taskId`: `memen-daily-insight`
  - `title`: "memen: today's insight" in the user's language (Japanese: 「memen 今日の気づき」)
  - `description`: Every night at 23:00, read today's records and AI work logs and save one insight card to memen
  - `cronExpression`: `0 23 * * *`
  - `prompt`: the body of this plugin's `daily-insight` skill (`../daily-insight/SKILL.md`, everything below its front matter, leaving out HTML comments) copied verbatim, followed by the block below. Read that file; do not rewrite its steps from memory.

```text
Notes for this scheduled run:
- Today's local Claude Code logs are the *.jsonl files under ~/.claude/projects/ updated today. Skip this task's own conversation.
- If save_day_learning returns saved: false, the user deleted today's card. Do not retry.
- Do not change or delete to-dos, plans, or notes.
- If the memen tools are missing or return an authentication error, save nothing and end with: "memen's MCP is not connected. Open /mcp in Claude Code and authenticate memen."
```

Tell the user the task runs while the Claude app is open and the Mac is awake; if the app was closed at 23:00, it runs the next time the app opens.

## 4. Write today's card now

Follow this plugin's `daily-insight` skill for today, as written there. Do not wait for the night.

- If it saves a card, tell the user to open memen and look at the Insights (気づき) tab next to To-dos (on iPhone, at the top of the To-dos tab).
- If there was too little to read and nothing was saved, say so and that the first card will come tonight at 23:00.

## Rules

- Do not change to-dos, plans, notes, or memen settings during setup.
- Never send raw logs to memen; only the finished card goes there.
