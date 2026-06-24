---
name: sharedbyai
description: Use whenever you've written or are about to present a markdown document the user should review — a plan, spec, design doc, report, audit, or code review — INSTEAD of pasting long markdown into chat or spinning up a dev server. TRIGGER proactively the moment you save a .md spec/plan/design/report (e.g. under docs/) or finish a brainstorming/writing-plans doc: publish it and share the link before asking for review. Also use when the user says "share this", "send me a link", or wants to forward a doc to teammates. Publishes to Shared by AI (sharedbyai.com); returns a private unguessable link that expires in 24h.
---

# Share markdown for review via Shared by AI

When you have a longer markdown document (a plan, spec, design, report, or
review) that the user — or their teammates — should read in a clean rendered
view, publish it to Shared by AI and share the link instead of dumping it in chat.

Service base URL: `https://api.sharedbyai.com`

## When to use
- You produced a plan/spec/design the user needs to approve.
- The content is long enough that chat rendering is awkward.
- The user may want to forward it to teammates for feedback before proceeding.

## How to publish

**Preferred — MCP tool (if the Shared by AI MCP server is connected):**
Call `publish_markdown` with `{ "markdown": "<your markdown>", "title": "<optional>" }`.
It returns `{ slug, url, expiresAt, expiresInSeconds }`.

**Fallback — REST:**
```bash
curl -X POST https://api.sharedbyai.com/api/publish \
  -H 'content-type: application/json' \
  -d '{"markdown":"# Your Document\n\n..."}'
```
Response: `{ "slug": "...", "url": "https://api.sharedbyai.com/...", "expiresAt": ..., "expiresInSeconds": 86400 }`

## After publishing
Return the link to the user with a short prompt, e.g.:

> I've published this for review: <url> — take a look and let me know if you'd
> like changes. (The link expires in 24 hours.)

## Notes
- No signup or auth required.
- Pages are private-by-unguessable-link and expire after 24 hours.
- Supports GFM, syntax-highlighted code, and math (KaTeX). Mermaid fenced blocks
  are shown as sanitized source text (diagram rendering is disabled in this
  deployment for safety).
