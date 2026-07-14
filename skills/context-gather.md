---
type: skill
id: context-gather
title: Context Gather
description: "Searches Gmail for email threads related to meeting attendees and topics"
tags: [Production, Email]
connections:
  - target: gmail-mcp
    type: runs_on
  - target: llm-service
    type: runs_on
---

## Capability

Takes the meeting event data (attendees, topic keywords) and searches Gmail for related email threads. Provides context for each attendee and the meeting topic.

## What It Does

1. **Per-attendee search** — calls `search_emails` for each attendee (e.g. `from:jane@example.com newer_than:14d`) to find recent conversations
2. **Topic search** — calls `search_emails` with topic keywords from the event title and description
3. **Read relevant threads** — calls `read_email` on the most relevant results (up to 3 per attendee, 5 for the topic)
4. **Structure context** — organizes findings by attendee and by topic, noting key threads, open questions, and pending actions

## Outputs

Structured context: per-attendee email summaries, topic-related threads, and pending action items relevant to the meeting.
