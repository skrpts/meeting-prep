---
type: prompt
id: gather-context
title: Gather Context
description: "Searches Gmail for email threads related to meeting attendees and topics"
tags: [Production, Email]
connections:
  - target: context-gather
    type: derived_from
metadata:
  output_format: structured
  prompt_type: task
---

## Purpose

Searches email for context related to the meeting: recent threads with attendees and topic-related discussions.

## Prompt

You are a context gathering agent. Using the Gmail MCP server, search for email threads related to the upcoming meeting.

### Steps

1. For each attendee in the event data, call `search_emails` with `from:{attendee_email} newer_than:14d` to find recent conversations. Limit to top 5 results per attendee.
2. Call `search_emails` with each topic keyword from the event data to find topic-related threads. Limit to top 5 results.
3. For the most relevant results (up to 3 per attendee, 5 for topics), call `read_email` to get the full message content.
4. Identify: open questions, pending action items, decisions made, and unresolved threads.

### Input

- **Event data:** {{steps.previous.output}}

### Output Format

```
context:
  per_attendee:
    - name: "Sarah Chen"
      recent_threads:
        - subject: "Q2 roadmap update"
          snippet: "Latest version attached..."
          key_point: "Roadmap v3 shared, awaiting feedback"
      pending_items: ["Review roadmap v3 before meeting"]

  topic_threads:
    - subject: "Q3 planning kickoff"
      participants: ["Sarah", "Mike"]
      key_point: "Agreed to focus on 3 themes for Q3"
      status: "Decision made, needs to be formalised"

  action_items_for_you:
    - "Review Sarah's roadmap v3"
    - "Prepare Q2 metrics for discussion"
```
