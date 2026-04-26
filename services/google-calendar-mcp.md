---
type: service
id: google-calendar-mcp
title: Google Calendar MCP
description: "Google Calendar MCP server for fetching meeting details, attendees, and event descriptions"
tags: [Production, Calendar]
connections: []
metadata:
  provider: google-calendar
  protocol: mcp
  auth_type: oauth
  env_var: GOOGLE_OAUTH_CREDENTIALS
  required_scopes: [calendar.readonly]
---

## Service Description

Provides access to Google Calendar via the Model Context Protocol (MCP). This service is used to fetch the target meeting's details: attendees, description, location, and time.

## Configuration

### Authentication

Requires OAuth 2.0 credentials for Google. Set `GOOGLE_OAUTH_CREDENTIALS` to the path of your credentials JSON file.

### MCP Server Setup

```json
{
  "mcpServers": {
    "google-calendar": {
      "command": "npx",
      "args": ["-y", "google-calendar-mcp"],
      "env": {
        "GOOGLE_OAUTH_CREDENTIALS": "{GOOGLE_OAUTH_CREDENTIALS}"
      }
    }
  }
}
```

## Capabilities Used

- `search-events` — find the meeting by name or topic
- `get-event` — retrieve full event details including attendees, description, and conferencing links
- `list-events` — list today's events if searching by name
