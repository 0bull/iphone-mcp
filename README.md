# iPhone MCP server: real, hosted iPhones for AI agents

**0bull** is a remote MCP server that gives an AI agent (Claude, ChatGPT, Codex, Cursor, OpenCode, OpenClaw and other MCP clients) control of **real, physical iPhones**. They are not simulators or Android emulators. They are rented by the month and hosted in 0bull's rack, so you don't need a Mac, a USB cable, Xcode or WebDriverAgent.

- Endpoint: `https://0bull.net/mcp` (streamable HTTP, OAuth)
- Registry name: `net.0bull/phone-farm` ([official MCP Registry](https://registry.modelcontextprotocol.io), Smithery, Glama)
- Docs: <https://docs.0bull.net/mcp/overview> · Tool reference: <https://docs.0bull.net/mcp/tools>
- Phones: <https://0bull.net/pricing>
- Demo video: [ChatGPT controls a real iPhone with the 0bull MCP server](https://www.youtube.com/watch?v=SN7vgcsE_tk)

## What an agent can do on the phone

| Area | Tools |
|---|---|
| See the screen | `phone-snapshot-tool` (screenshot), `phone-ocr-tool` (on-screen text) |
| Act on the screen | `phone-control-tool` (tap, swipe, hotkey, type), `phone-command-tool` (device commands) |
| Hand off a whole task | `run-phone-agent-tool` (one plain-language task for 0bull's AI phone agent), `run-macro-tool` (replay a recorded macro) |
| Track phone work | `list-phone-runs-tool`, `get-phone-run-tool` |
| Post video | `create-submission-tool`, `get-submission-tool`, `list-submissions-tool`, `cancel-submission-tool` for TikTok, Instagram and YouTube |
| Posting accounts | `list-accounts-tool`, `create-account-tool`, `update-account-tool`, `get-account-tool`, `delete-account-tool` |
| Phones and billing | `list-phones-tool`, `get-billing-tool`, `start-rental-tool`, `request-phones-tool` (these return a link a human approves, nothing is charged by the agent) |

24 tools in all. Anything that touches a phone is queued and returns at once; poll the run or submission for the result. Snapshots, OCR and raw input run synchronously.

## Connect

**Claude Code**

```bash
claude mcp add --transport http 0bull https://0bull.net/mcp
```

Then run `/mcp`, pick `0bull` and sign in. A browser window handles OAuth, so there are no tokens to paste.

**Claude Desktop / Cursor** (`claude_desktop_config.json`, `.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "0bull": { "type": "http", "url": "https://0bull.net/mcp" }
  }
}
```

**Codex**

```bash
codex mcp add 0bull --url https://0bull.net/mcp
```

**OpenCode** (`opencode.json`)

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": { "0bull": { "type": "remote", "url": "https://0bull.net/mcp", "enabled": true } }
}
```

Check the connection by asking your client to "list my posting accounts". It's a read-only call that touches no phone.

## How it compares to local iPhone MCP servers

Open-source servers such as ios-control-mcp, iphone-mcp and iphone-control drive **your own** iPhone over USB from a Mac or Linux machine. They work well if the phone sits on your desk.

0bull is for when it doesn't: the iPhones are hosted and always on, each with its own connection, and they are shared with your team and your agents over one URL. You don't run a host machine, and nothing goes into Developer Mode on your personal phone.

| | Local USB MCP servers | 0bull |
|---|---|---|
| Device | your own iPhone | rented iPhone, hosted by 0bull |
| Host | your Mac or Linux box, USB | none, remote HTTP |
| Setup | Xcode / WebDriverAgent / pymobiledevice3, Developer Mode | add a URL, sign in with OAuth |
| Many phones and teammates | manual | phones, seats and per-phone access in the dashboard |
| Cost | free (you own the hardware) | from $100 per phone per month, down to $75 at volume ([pricing](https://0bull.net/pricing)) |

## Also available

- REST API: <https://docs.0bull.net/api>
- SDKs: [TypeScript](https://github.com/0bull/0bull-typescript-sdk), [Python](https://github.com/0bull/0bull-python-sdk)
- Plugins: [Claude](https://github.com/0bull/claude-plugin), [Agent Plugins / OpenClaw](https://github.com/0bull/agent-plugin)

## Support

hey@0bull.net · <https://0bull.net/contact>

Operated by NANIMAD SL (Madrid, Spain).
