# LinkedNav MCP

**Run your LinkedIn outreach from your AI chat.**

LinkedNav MCP connects AI assistants (Claude, Cursor, and any other MCP app) to your
[LinkedNav](https://www.linkednav.com?utm_source=github&utm_campaign=mcp-registry) account.
Once it's connected, you just ask your assistant to find the right people, launch
campaigns, send connection requests and messages, answer replies, and check results. It
does the outreach for you.

- **Server:** `https://mcp.linkednav.com/`
- **Works with:** Claude Code, Claude Desktop, claude.ai, Cursor, and any MCP client
- **Sign up (free trial):** [linkednav.com](https://www.linkednav.com?utm_source=github&utm_campaign=mcp-registry)

## What you can do with it

Ask your assistant things like:

- "Who should I target on LinkedIn, and what should I say?"
- "Find people who just changed jobs at companies like these."
- "Set up a campaign and turn it on."
- "What replies came in, and what should I say back?"
- "How is my outreach doing, and what should I fix?"

Under the hood it gives your assistant tools for:

- **Setup and targeting** (your business and your ideal customer)
- **Finding leads** (buying-signal search, competitor and influencer engagers, social listening)
- **Campaigns** (create, launch, pause, schedule)
- **Messages** (write and save your connection note and follow-ups)
- **Sending and inbox** (send connects and messages, read and answer replies)
- **Enrichment** (find emails, phones, and profile details)
- **Analytics** (audit your setup, see your funnel, find what to fix)

## Connect it (about 2 minutes)

1. Sign up at [linkednav.com](https://www.linkednav.com?utm_source=github&utm_campaign=mcp-registry)
   and create an API key at [/app/api-keys](https://www.linkednav.com/app/api-keys?utm_source=github&utm_campaign=mcp-registry).
2. Add the server to your app.

**Claude Code:**
```bash
claude mcp add --transport http linkednav https://mcp.linkednav.com/ \
  --header "Authorization: Bearer YOUR_KEY"
```

**Claude Desktop or claude.ai:** Settings, then Connectors, then Add custom connector.
Name it `LinkedNav`, URL `https://mcp.linkednav.com/`, then sign in with your browser
(OAuth) or add an `Authorization: Bearer YOUR_KEY` header.

**Cursor / Cline / other MCP apps** (`~/.cursor/mcp.json`):
```json
{
  "mcpServers": {
    "linkednav": {
      "url": "https://mcp.linkednav.com/",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```

## Pairs with the open-source skill

Want a ready-made outreach team that uses this MCP? Install the free, open-source
**[LinkedIn Outreach OS](https://github.com/linglistack/linkedin-outreach-os)** skill.
The skill writes your plan and messages; this MCP does the real work.

## About this repo

This repo holds the public info and the MCP registry manifest (`server.json`) for the
LinkedNav MCP server. The server itself is hosted at `mcp.linkednav.com` and runs on your
own LinkedNav account. The server's source code is not part of this repo.

## License

[MIT](./LICENSE) for the contents of this repo. LinkedNav is a hosted service.
