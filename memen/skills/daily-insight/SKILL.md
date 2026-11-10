---
name: daily-insight
description: Use when the user runs the nightly memen insight routine ("/memen:daily-insight", "summarize today's insights to memen"). Reads the day from memen and the local AI work logs, then saves one insight card with save_day_learning.
---

# Daily insight

<!-- 手順の正は web/lib/shared/i18n/messages/en.ts の aiConnections.learningPrompt。ここはその写しで、
     web/tests/day-learning-prompts.test.mjs が一致を見る。守ること(数字を作らない・診断しない・根拠)は
     MCP の save_day_learning の説明が正。 -->

Reply and write in the user's language.

Summarize today's insights and save them to memen.
1. Read today with memen's get_day, today's AI prompts with get_ai_work, and the learning field for the past 14 days with get_analysis (two 7-day reads). On Sundays, also read the last 28 days with get_patterns.
2. If you can read today's local Claude Code logs, read them too (never send raw logs to memen).
3. Work out what I did and which criteria I used to choose.
4. Find one place where work got stuck: gaps between plans and actual work (focusSessions, hourlySummaries), focus broken by detours, and the same request repeated to the AI. On Sundays, name one recurring bottleneck from the 28 days as a hypothesis.
5. Save with save_day_learning. Write the bottleneck as one of the insights, with its evidence and one thing to try next.
- Give every insight its evidence (which record, when). Note when a past decision or bottleneck repeats.
- At most one question and one next step per insight. Copy minutes, counts, and totals exactly as memen returned them (no re-rounding or re-adding), and do not diagnose personality or ability. Do not state the cause of a bottleneck as fact.
- If there is too little to read, end without saving.
