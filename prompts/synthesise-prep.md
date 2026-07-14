---
type: prompt
id: synthesise-prep
title: Synthesize Prep
description: "Produces a meeting prep document from event details and email context"
tags: [Production, Calendar]
connections:
  - target: prep-synthesis
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Combines the event details and email context into a structured meeting prep document.

## Voice Profile

{{step.context.voice_profile}}

If a voice profile is provided above, write the prep document in that voice. If not, use a clear, professional style.

## Configuration

- **Prep depth:** {{step.context.prep_depth}}

## Prompt

You are a meeting prep synthesis agent. Produce a prep document from the event details and email context below.

### Structure by Depth

**Quick** (200–300 words):
1. **Meeting** — title, time, attendees (one line)
2. **Talking points** — 3–5 bullets based on context

**Standard** (400–700 words):
1. **Meeting** — title, time, duration, attendees, location
2. **Attendee context** — one paragraph per attendee: what you've been discussing
3. **Talking points** — suggested topics with brief context
4. **Questions to ask** — specific questions from open threads

**Thorough** (700–1,200 words):
1. Everything in Standard
2. **Background** — summary of relevant email threads with key decisions
3. **Preparation tasks** — things to do before the meeting
4. **Related threads** — excerpts from the most relevant email conversations

### Input

- **Event:** {{steps.Event Fetch.output}}
- **Context:** {{steps.previous.output}}

### Formatting Rules

- Use British English throughout
- Use markdown headings and bullets for scannability
- Attendee names in bold on first mention
- Times in the event's timezone
- Lead with what you need to know walking into the room
