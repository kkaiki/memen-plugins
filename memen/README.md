# Memen plugin

[日本語](README.ja.md)

Use [memen](https://memen.app) from Claude Code and Codex. Ask your AI about your day, and keep a record of the work you did together.

## What you can do

Ask in plain words:

- "Show me today in memen"
- "Check memen for what I did yesterday afternoon"
- "Add 'send the estimate' to my to-dos in memen"
- "Log the work we just did to memen"

## Before you start

You need a memen account you can sign in to on the web. Right now, that means an account that signs in with Google. Accounts created on iPhone with Apple only can't connect yet.

## Install

### Claude Code

1. Run this inside Claude Code:

   ```text
   /plugin install memen --marketplace kkaiki/memen-plugins
   ```

2. Open `/mcp`, choose memen, and press Authenticate.
3. In the browser, sign in to memen and press Allow.

### Codex

1. Run these in your terminal:

   ```bash
   codex plugin marketplace add kkaiki/memen-plugins
   codex plugin add memen@memen
   codex mcp login memen
   ```

2. In the browser, sign in to memen and press Allow.

After you allow access, the browser returns to a `localhost` page. That is normal: it is how Claude Code or Codex on your computer receives the result.

## What your AI can and can't do

| Your AI can | Your AI can't |
| --- | --- |
| Read your days and weeks (to-dos, notes, plans, time summaries) | Read raw transcripts |
| Log work to your timeline | Delete records or notes |
| Add and move to-dos and plans | Change screen time or site-block limits |
| Delete a to-do or plan, one at a time, after you confirm | |

## Your data

Records your AI reads are sent to the company behind that AI (Anthropic for Claude, OpenAI for Codex) and handled under its terms. memen removes API keys and other secrets from the text it returns. The plugin stores no keys: sign-in uses OAuth only.

See [Connect your AI](https://memen.app/ai) and the [privacy policy](https://memen.app/privacy) for details.

## Stop using it

Sign in to memen and disconnect the AI under "Connected AI" in the menu. It loses access right away.
