# CA3 Claude Code Plugin

CA3 is a user-owned AI context hub for saved notes and attachments.

This repository is a Claude Code plugin marketplace source for connecting Claude Code to the public CA3 OAuth MCP endpoint.

## Install

Add this marketplace source:

```bash
claude plugin marketplace add enactflow/ca3-claude-code-plugin
```

Then install `ca3` from the Claude Code plugin directory.

On first use, Claude Code should open the CA3 OAuth flow and ask you to authorize the requested scopes.

## MCP Endpoint

```text
https://ca3.dribwise.ai/mcp
```

## Plugin Layout

```text
.claude-plugin/marketplace.json
plugins/ca3/.claude-plugin/plugin.json
plugins/ca3/.mcp.json
plugins/ca3/skills/ca3/SKILL.md
```

## Usage

Use CA3 explicitly:

```text
Use CA3 to remember this project decision.
```

Or let Claude Code use CA3 automatically when project instructions say CA3 is the shared context surface.

CA3 behavior is defined by the live MCP tool descriptions exposed by:

```text
https://ca3.dribwise.ai/mcp
```

The plugin skill is only a bootstrap hint. It intentionally does not duplicate the detailed notes and attachments rules, so all CA3 clients share the same behavior contract from the MCP server.

When creating or updating a note through MCP, include the required `profile_hint` argument. This should describe the durable user intent or profile signal behind the note, not just the immediate action.

## Troubleshooting

After installing, updating, or re-authenticating the plugin, start a new Claude Code session before testing CA3. Existing sessions may keep stale plugin skill or OAuth connection state.

If an old session reports an OAuth refresh or authentication error, authenticate CA3 again, confirm the CA3 MCP server is enabled, then open a new Claude Code session.

If an old session reports that it cannot find `SKILL.md` or that plugin skill paths do not match, treat it as stale Claude Code plugin cache state. The CA3 MCP tools may still work through tool discovery, but the stable fix is to open a new session after installation or update.

## License

MIT
