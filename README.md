# SlopeSense AI connector

Connect **your own AI assistant** — Claude, ChatGPT, Claude Code, Gemini CLI,
or any MCP client — to your [SlopeSense](https://www.slopesense.ca) season
planner. The assistant signs in as *you* (OAuth) and gets the same planner
surface you have: teams, racers, Strive scorecards, season plans, practices,
races, attendance and official results. Inside your club only.

> Requires a SlopeSense coaching account on the plan that includes the AI
> connector. Open **Settings → AI** in SlopeSense to check, and to see your
> personal instruction block.

## 1 · Give your AI its instructions

Copy the block from **Settings → AI → "Paste this into your AI"** into a
Claude Project, a Custom GPT, a Gem, or just the chat. It tells the assistant
to read [`SKILL.md`](./SKILL.md) (how to behave with your data) and where your
MCP server is.

## 2 · Add the connector

| Client | How |
|---|---|
| **Claude** (claude.ai, desktop) | Settings → Connectors → *Add custom connector* → URL `https://www.slopesense.ca/mcp` → Connect → approve the SlopeSense consent screen. |
| **ChatGPT** | Settings → Connectors → *Create* (developer mode) → MCP server URL `https://www.slopesense.ca/mcp`, Authentication **OAuth** → approve the consent screen. |
| **Claude Code** | `claude mcp add --transport http slopesense https://www.slopesense.ca/mcp` then `/mcp` to sign in. |
| **Gemini CLI** | Add to `~/.gemini/settings.json`: `{"mcpServers":{"slopesense":{"httpUrl":"https://www.slopesense.ca/mcp"}}}` then `/mcp auth slopesense`. |
| Any MCP client | Streamable HTTP at `/mcp`, OAuth 2.1 with PKCE and dynamic client registration — metadata at `/.well-known/oauth-authorization-server`. |

The consent screen shows which app is asking and what it gets. You can
disconnect an app any time from **Settings → AI → Connected apps**.

## 3 · Talk to your planner

Things that work well:

- "What's next for U12 Rockets, and who hasn't been graded on level 2?"
- "Draft a GS-focused practice for Saturday on the Collingwood plan, 2 hours,
  gates in the main part. Keep it a draft for me to review."
- "Move the hop turns drill from warm-up to cool-down in practice 42."
- "Grade Isabelle gold on Skiing a rocking traverse and add a note."
- "Make me a parent message for Saturday's practice."

What the assistant will **not** do without asking you first: publish to
Strive, push grades to Strive, or delete anything. (See `SKILL.md`.)

## Your own AI for SlopeSense's helpers

Separately, **Settings → AI → Your AI** lets you store your own Anthropic /
OpenAI / Gemini API key so SlopeSense's in-app helpers (practice drafting,
chat edits, season vision) run on your provider and your account.

## Files

- [`SKILL.md`](./SKILL.md) — the behaviour guide your assistant reads.
- [`examples/`](./examples) — client config snippets.
- Full contract: `product_management/api/ai-connector.md` in the SlopeSense repo.
