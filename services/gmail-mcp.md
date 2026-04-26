---
type: service
id: gmail-mcp
title: Gmail MCP
description: "Gmail MCP server for searching email threads related to meeting attendees and topics"
tags: [Production, Email]
connections: []
metadata:
  provider: gmail
  protocol: mcp
  auth_type: oauth
  env_var: GMAIL_OAUTH_CREDENTIALS
  required_scopes: [gmail.readonly]
---

## Service Description

Provides access to Gmail via the Model Context Protocol (MCP). This service is used to search for email threads related to meeting attendees and topics, providing context for the prep document.

## Configuration

### Authentication

Requires OAuth 2.0 credentials for Google. Set `GMAIL_OAUTH_CREDENTIALS` to the path of your credentials JSON file.

### MCP Server Setup

```json
{
  "mcpServers": {
    "gmail": {
      "command": "npx",
      "args": ["-y", "gmail-mcp-server"],
      "env": {
        "GMAIL_OAUTH_CREDENTIALS": "{GMAIL_OAUTH_CREDENTIALS}"
      }
    }
  }
}
```

## Capabilities Used

- `search_emails` — search for emails by attendee name/address and meeting topic
- `read_email` — read full email content for relevant threads
