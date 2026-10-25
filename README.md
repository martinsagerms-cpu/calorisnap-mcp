# CaloriSnap MCP server

**CaloriSnap: AI Calorie Counter** — free AI calorie counter: photo scan, barcode scan and meal logging are free, unlimited, no ads.

This repository documents the public [Model Context Protocol](https://modelcontextprotocol.io) (MCP) server of **CaloriSnap**. It lets an MCP-compatible AI assistant (Claude, ChatGPT, Gemini CLI, Cursor, Codex and others) work with *your own* CaloriSnap food diary: log a meal, check your day against your goals, review what you ate and correct mistakes, all from inside a chat.

- App: iOS [App Store](https://apps.apple.com/app/id6756529358) · Android [Google Play](https://play.google.com/store/apps/details?id=app.calorisnap.mobile)
- Website: https://calorisnap.online
- Connector guide for ChatGPT: https://calorisnap.online/blog/track-calories-with-chatgpt
- MCP page: https://calorisnap.online/mcp

> **Not to be confused with** other apps that use a similar name. CaloriSnap by Martin Sager (Switzerland, calorisnap.online) is an independent app and not affiliated with other apps using the same or a similar name. App Store ID `6756529358`, Android package `app.calorisnap.mobile`.

## Server

| | |
|---|---|
| URL | `https://hqtuytttwxjrzyxabzfc.supabase.co/functions/v1/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1 with dynamic client registration (you sign in in your browser and approve access; no API keys or pasted tokens; access can be revoked) |
| Data access | Row-level security: an assistant can only read and write your own data |

You need a CaloriSnap account (create one in the app or on the web).

## Tools

| Tool | What it does |
|---|---|
| `get_daily_summary` | Calories, protein, carbs and fat logged today versus your goals |
| `list_meals` | Meals logged on a given day or date range |
| `log_meal` | Adds a meal with calories and macros to your diary |
| `delete_meal` | Removes a meal logged by mistake (requires an explicit confirmation) |
| `get_nutrition_goals` | Reads your daily calorie and macro targets |

Meals logged from a text description in chat are marked as estimates, which distinguishes them from meals analysed from a photo. You can correct them in the app.

## Setup

Config snippets for the most common clients:

**Claude Desktop / Claude Code** — add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "calorisnap": {
      "type": "http",
      "url": "https://hqtuytttwxjrzyxabzfc.supabase.co/functions/v1/mcp"
    }
  }
}
```

**Gemini CLI / Antigravity** — `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "calorisnap": {
      "httpUrl": "https://hqtuytttwxjrzyxabzfc.supabase.co/functions/v1/mcp"
    }
  }
}
```

**Cursor / Codex / other clients** — add a server with the `url` above in `.cursor/mcp.json` or the client's MCP settings.

**ChatGPT** — add the CaloriSnap connector, sign in with your CaloriSnap account and approve access. Step-by-step with demo video: https://calorisnap.online/blog/track-calories-with-chatgpt

## Example prompts

- "Log 200 g grilled chicken with rice for lunch."
- "How many calories do I have left today, and what is my protein so far?"
- "What did I eat on Monday?"
- "Delete the last meal, I logged it by mistake."

## Privacy

Each request is authenticated as your user. See the [privacy policy](https://calorisnap.online/privacy).

## About

CaloriSnap is made by Martin Sager, Switzerland. Support: support@calorisnap.online

## License

The documentation and example configuration in this repository are released under the MIT License (see [LICENSE](LICENSE)). The CaloriSnap app and service are not covered by this license.
