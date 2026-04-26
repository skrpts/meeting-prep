---
type: skill
id: event-fetch
title: Event Fetch
description: "Retrieves meeting details from Google Calendar via MCP — attendees, description, time, and location"
tags: [Production, Calendar]
connections:
  - target: google-calendar-mcp
    type: runs_on
  - target: llm-service
    type: runs_on
---

## Capability

Finds a calendar event by name or ID and retrieves full details: time, duration, attendees, description, location, and conferencing links.

## What It Does

1. **Find event** — calls `search-events` with the meeting name, or `get-event` with the event ID if provided
2. **Enrich details** — retrieves attendee list with names and email addresses, full event description, and location/conferencing info
3. **Extract topics** — identifies keywords and topics from the event title and description for downstream email search

## Outputs

Structured event data: time, duration, attendees (names + emails), description, location, and extracted topic keywords.
