# Tools

List the MCP tools this skill uses from the Mermail agent-inbox profile. All tools are accessed via the Mermail MCP server with the agent-inbox profile.

## Conventions

- Pass structured arguments as **native JSON objects**. Never stringify an object into a string field such as `query`.
- Use the exact tool identifier exposed by the current host (for example `list_emails` or a host-qualified form like `Mermail:list_emails`). Do not manually add, strip, or invent prefixes inconsistently.
- Prefer mailbox `public_id` as `mailboxId` when the list tools return it.

## Tools Used

| Tool | Purpose | Access Type |
|------|---------|-------------|
| `list_workspaces` | Get current workspace ID | read |
| `list_mailboxes` | Find existing mailboxes for service | read |
| `get_mailbox` | Get specific mailbox details | read |
| `create_mailbox` | Provision new service-scoped mailbox | write |
| `search_emails` | Search for verification emails with filters | read |
| `get_email` | Fetch email content and metadata | read |
| `get_email_context` | Get conversation context for understanding | read |

## Tool Notes

- All tools use the `https://console.mermail.app/mcp?profile=agent-inbox` endpoint
- The agent-inbox profile provides exactly 12 tools optimized for mailbox provisioning and safe email reading
- In the agent-inbox profile, `list_emails` and `search_emails` return metadata-only results by default for security
- `get_email` in agent-inbox profile returns `agent_safe_content` and `metadata_only` when available
- Never pass `"query": "{\"sortColumn\":\"date\"}"` - always pass native JSON objects

## Examples

```json
{
  "query": {
    "sender": "no-reply@service.com",
    "recipient": "user@service.com", 
    "subject": "Verify your signup",
    "date_start": "2026-09-30T10:00:00Z"
  }
}
```

Do not pass `"query": "{\"sender\":\"no-reply@service.com\"}"`.