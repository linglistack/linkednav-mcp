# Publishing to the official MCP Registry

This lists LinkedNav on the official Model Context Protocol registry at
registry.modelcontextprotocol.io, which many MCP clients and directories read from.

## One-time setup

Install the publisher tool:
```bash
brew install mcp-publisher
```
No Homebrew? Download the binary from the releases page of
github.com/modelcontextprotocol/registry and put it on your PATH.

## Publish

Run these from this folder (where `server.json` lives):
```bash
mcp-publisher login github
# This opens github.com/login/device and shows a code. Enter the code, approve, come back.

mcp-publisher publish
# Reads server.json and publishes it.
```

That's it. Your listing appears under `io.github.linglistack/linkednav-mcp`.

## Updating it later

Change `version` in `server.json` (for example `1.0.0` to `1.0.1`), then run
`mcp-publisher publish` again.

## Good to know

- The name `io.github.linglistack/linkednav-mcp` must stay matched to this GitHub repo.
  Signing in with GitHub proves you own it.
- `server.json` is checked when you publish. If something is off, the tool tells you what to fix.
- The server code itself is not here. This repo only holds the public info and this manifest.
