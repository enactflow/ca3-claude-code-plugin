---
name: ca3
description: Bootstrap CA3 usage in Claude Code. Use the live CA3 MCP tool list and tool descriptions as the source of truth for notes and attachments behavior.
---

# CA3

CA3 is a user-owned context hub shared by Claude Code, Codex, ChatGPT, and other MCP clients.

Use CA3 when the user asks to remember, save, recall, search, or update persistent context, or when project instructions say CA3 is the shared context surface.

## Source Of Truth

Do not infer detailed CA3 behavior from this file. The live MCP tool list and each MCP tool description are the source of truth for:

- Available tools.
- Required arguments.
- Notes and attachments boundaries.
- Read, write, update, and delete behavior.
- Scope and authorization failures.

If you need to know what CA3 can do, inspect the CA3 MCP tools exposed by the plugin instead of reading local plugin files or guessing from cached state.

## Bootstrap Behavior

- Prefer CA3 MCP tools over local filesystem searches for saved context.
- Search before answering when the request depends on prior saved context.
- Write to CA3 when the user explicitly asks to remember or save durable context.
- When creating or updating a note through MCP, provide the required `profile_hint` argument with the durable user intent or profile signal behind the note.
- Ask first before storing sensitive, uncertain, inferred, or surprising personal data.
- Never store secrets, OAuth tokens, passwords, private keys, or recovery codes in CA3.

## Stale Session Handling

Claude Code may keep plugin skill and OAuth connection state per session. After installing, updating, or re-authenticating CA3, start a new Claude Code session before testing.

If a session reports OAuth refresh or authentication errors, authenticate CA3 again and then open a new session.

If a session reports missing or mismatched `SKILL.md` paths, do not debug CA3 by reading local plugin cache paths. Use MCP tool discovery or open a new session.
