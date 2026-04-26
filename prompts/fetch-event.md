---
type: prompt
id: fetch-event
title: Fetch Event
description: "Retrieves meeting details from Google Calendar via MCP"
tags: [Production, Calendar]
inputs:
  meeting_name:
    label: "Meeting Name"
    description: "The name or topic of the meeting to prepare for"
    example: "Q2 Planning Review"
    required: false
    type: text
  event_id:
    label: "Calendar Event ID"
    description: "The calendar event ID if known — otherwise we search by name"
    example: ""
    required: false
    type: text
connections:
  - target: event-fetch
    type: derived_from
metadata:
  output_format: structured
  prompt_type: task
---

## Purpose

Finds the target meeting on the calendar and retrieves full details for context gathering.

## Prompt

You are a data retrieval agent. Using the Google Calendar MCP server, find and fetch the meeting details.

### Steps

1. If `{{input.event_id}}` is provided, call `get-event` directly with that ID.
2. If only `{{input.meeting_name}}` is provided, call `search-events` with that name. If multiple results, pick the next upcoming occurrence.
3. Retrieve full event details: title, start/end time, attendees (names and emails), description, location, and conferencing links.
4. Extract topic keywords from the title and description for the email search step.

### Output Format

```
event:
  title: "Q2 Planning Review"
  start: "2026-04-28T14:00:00Z"
  end: "2026-04-28T15:00:00Z"
  duration_minutes: 60
  attendees:
    - name: "Sarah Chen"
      email: "sarah@example.com"
    - name: "Mike Johnson"
      email: "mike@example.com"
  location: "Room 3A / Zoom"
  description: "Review Q2 roadmap progress and plan Q3 priorities"
  topic_keywords: ["Q2 roadmap", "Q3 priorities", "planning"]
```

### Error Handling

- If the event is not found, report the error and suggest checking the name
- If multiple events match, list them and pick the next upcoming one
