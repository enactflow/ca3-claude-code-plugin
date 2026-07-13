# CA3 Claude Code Plugin

<img src="assets/ca3-icon-rounded.png" alt="CA3" width="96">

CA3 gives AI agents a private, user-owned memory layer so important context can follow you across ChatGPT, Codex, Claude Code, and browser workflows.

This repository is a Claude Code plugin marketplace source for connecting Claude Code to the public CA3 OAuth MCP endpoint.

## Install

Add the CA3 marketplace, then install the `ca3` plugin at user scope:

```bash
claude plugin marketplace add enactflow/ca3-claude-code-plugin
claude plugin install ca3 --scope user
```

On first use, Claude Code should open the CA3 OAuth flow and ask you to authorize the requested scopes.

Start a new Claude Code session after installing so the CA3 skill and MCP server are loaded cleanly.

For project-level or local installs, replace `user` with `project` or `local`.

## Upgrade

Update the installed plugin at the same scope where it was installed:

```bash
claude plugin update ca3 --scope user
```

For project-level or local installs, replace `user` with `project` or `local`.

Restart Claude Code after upgrading. Existing sessions may keep older plugin skill or OAuth state.

## Verify

Confirm CA3 is installed and enabled:

```bash
claude plugin list --json
```

Look for `ca3` with version `0.1.2` or newer, the expected scope, and enabled state.

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

Attachment uploads use the live direct-upload tool flow: call `prepare_attachment_upload`, POST the exact bytes and returned multipart fields directly to object storage, then pass `upload_id` to `create_note`, `update_note`, or `attach_uploaded_file`. The MCP server no longer accepts attachment `data_base64`; hosts that cannot perform the external multipart POST must report attachment upload as unsupported.

## Troubleshooting

After installing, upgrading, or re-authenticating the plugin, start a new Claude Code session before testing CA3.

If an old session reports an OAuth refresh or authentication error, authenticate CA3 again, confirm the CA3 MCP server is enabled, then open a new Claude Code session.

If an old session reports that it cannot find `SKILL.md` or that plugin skill paths do not match, treat it as stale Claude Code plugin cache state. The CA3 MCP tools may still work through tool discovery, but the stable fix is to open a new session after installation or update.

## License

MIT
