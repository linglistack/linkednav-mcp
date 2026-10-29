# LinkedNav MCP

[![M8ven Score](https://m8ven.ai/badge/mcp/linglistack-linkednav-mcp-1poutb?v=6cec32a7ede5c7a9694e71c46076123d)](https://m8ven.ai/mcp/linglistack-linkednav-mcp-1poutb?s=readme)

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
Or install the plugin in this repo, which signs in through your browser. See [The plugin](#the-plugin).

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

## The plugin

This repo is also a plugin for Claude Code. It holds two things:

- **The MCP server** `linkednav`, a pointer to `https://mcp.linkednav.com/`
  ([`.mcp.json`](.mcp.json)). Nothing is downloaded or run on your machine.
- **The skill** `linkednav` ([`skills/linkednav/SKILL.md`](skills/linkednav/SKILL.md)):
  how to use the tools well. It tells your assistant to ask you before anything is sent
  or changed on LinkedIn, and to report what the tools return instead of guessing.

To install it, run these in a terminal:

```bash
claude plugin marketplace add linglistack/linkednav-mcp
claude plugin install linkednav@linkednav
```

Then start Claude Code, run `/mcp`, choose `linkednav`, and sign in. The sign-in opens
LinkedNav's connect page in your browser, where you paste your API key once.

### Sign-in and network

The plugin connects to `https://mcp.linkednav.com` and reaches nothing else.

- `https://mcp.linkednav.com/`: the MCP server (Streamable HTTP).
- `https://mcp.linkednav.com/.well-known/oauth-protected-resource` and
  `/.well-known/oauth-authorization-server`: where your app finds the sign-in.
- `https://mcp.linkednav.com/register`, `/connect` and `/oauth/token`: the sign-in itself,
  OAuth with PKCE. Your app registers itself; there is no client secret.
- `https://mcp.linkednav.com/connect`: the page where you paste your API key.

What it needs from you: a LinkedNav account and an API key from
[/app/api-keys](https://www.linkednav.com/app/api-keys?utm_source=github&utm_campaign=mcp-registry).
No key is stored in the plugin, and it has no hooks and no scripts.

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
