---
type: workflow
id: meeting-prep
title: Meeting Prep
description: "Fetches meeting details and related emails via MCP, then produces a personalised prep document"
tags: [Production, Calendar, Email]
connections:
  - target: event-fetch
    type: uses
  - target: context-gather
    type: uses
  - target: prep-synthesis
    type: uses
  - target: language-polish
    type: uses
  - target: gmail-mcp
    type: runs_on
  - target: google-calendar-mcp
    type: runs_on
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "20-60 seconds"
  avg_tokens: 12000
  trigger: manual
output_step: "language-polish"
composite_steps:
  - "event-fetch"
  - "context-gather"
  - "prep-synthesis"
  - "language-polish"
execution:
  - skill: "event-fetch"
    step_type: "generation"
    prompt: "fetch-event"
  - skill: "context-gather"
    step_type: "generation"
    prompt: "gather-context"
  - skill: "prep-synthesis"
    step_type: "synthesis"
    prompt: "synthesise-prep"
    context:
      voice_profile: "Neutral professional tone"
      prep_depth: "Standard"
  - skill: "language-polish"
    step_type: "content"
    prompt: "polish-prep"
    context:
      voice_profile: "Neutral professional tone"
      grammar_strictness: "Professional"
---

## Overview

This workflow produces a personalised meeting prep document. Give it a meeting name or calendar event ID, and it fetches the event details, searches your email for related threads with each attendee, and synthesises everything into a prep document with context, talking points, and questions to ask.

Run it before any important meeting to walk in prepared.

## Pipeline Stages

### Stage 1: Event Fetch

**Input:** Meeting name or calendar event ID

Using the Google Calendar MCP service, find the meeting and retrieve full details: attendees, description, location, and topic keywords.

### Stage 2: Context Gather

Using the Gmail MCP service, search for recent email threads with each attendee and topic-related discussions. Identifies open questions, pending actions, and relevant decisions.

### Stage 3: Prep Synthesis

Combines event details and email context into a structured prep document. Depth controlled by the `prep_depth` persona dial (Quick, Standard, Thorough).

### Stage 4: Language Polish

Final cleanup and Voice Profile alignment.

**Output:** Meeting prep document, ready to review.

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.meeting_name}}` | No | Meeting name or topic | `Q2 Planning Review` |
| `{{input.event_id}}` | No | Calendar event ID (if known) | `` |

At least one of `meeting_name` or `event_id` is needed.

## Setup

1. **Gmail MCP server** — OAuth 2.0 with `gmail.readonly` scope
2. **Google Calendar MCP server** — OAuth 2.0 with `calendar.readonly` scope

## Example Input

```
Meeting name: Q2 Planning Review
```
