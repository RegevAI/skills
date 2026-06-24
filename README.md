# Shared by AI — Agent Skills

Public distribution of the **Shared by AI** agent skill. When an AI coding agent
produces a plan, spec, design, or diff you should review, this skill lets it
publish the content to a clean, shareable link at
[sharedbyai.com](https://sharedbyai.com) — so you and your team can review it
before the agent proceeds.

> This repository is the **distribution** of the skill only. It is synced from a
> separate source repository; do not develop here.

## Install

Works with any [agentskills.io](https://agentskills.io)-compatible agent
(Claude Code, Codex, Cursor, and 27+ more):

```bash
npx skills add RegevAI/skills
```

Or self-hosted (Claude Code), one line:

```bash
curl -fsSL https://sharedbyai.com/install.sh | sh
```

## Use the MCP server (any MCP-capable agent)

Add the MCP server instead of (or alongside) the skill:

```jsonc
// Claude Code / Cursor — .mcp.json
{ "mcpServers": { "sharedbyai": { "url": "https://api.sharedbyai.com/mcp" } } }
```

```toml
# Codex — ~/.codex/config.toml
[mcp_servers.sharedbyai]
url = "https://api.sharedbyai.com/mcp"
```

## REST

```bash
curl -X POST https://api.sharedbyai.com/api/publish \
  -H 'content-type: application/json' \
  -d '{"markdown":"# Plan\n..."}'
```

Anonymous links are free, require no signup, and expire 24 hours after publishing.

## License

MIT
