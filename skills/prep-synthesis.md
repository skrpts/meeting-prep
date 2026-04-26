---
type: skill
id: prep-synthesis
title: Prep Synthesis
description: "Produces a meeting prep document with context, talking points, and questions to ask"
tags: [Production, Calendar]
connections:
  - target: llm-service
    type: runs_on
context_params:
  voice_profile:
    label: "Voice Profile"
    description: "Your writing style for the prep document"
    required: false
  prep_depth:
    label: "Prep Depth"
    description: "How detailed the prep should be — Quick, Standard, or Thorough"
    default: "Standard"
    required: false
---

## Capability

Combines the event details and email context into a structured prep document. Tailored to the meeting type and your preferences.

## What It Does

1. **Meeting overview** — what, when, who, where
2. **Attendee context** — what you've been discussing with each attendee recently
3. **Background** — relevant email threads and decisions leading up to this meeting
4. **Talking points** — suggested topics to raise based on the context
5. **Questions to ask** — specific questions identified from open threads and pending items
6. **Preparation tasks** — anything you should do before the meeting (review a document, prepare numbers, etc.)

## Prep Depth Levels

- **Quick** — overview + talking points only. 200–300 words. Glance before walking in.
- **Standard** — overview + attendee context + talking points + questions. 400–700 words.
- **Thorough** — everything including background, preparation tasks, and related thread excerpts. 700–1,200 words.

## Outputs

Formatted prep document in markdown.
