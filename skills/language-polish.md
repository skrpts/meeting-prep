---
type: skill
id: language-polish
title: Language Polish
description: "Spelling, grammar, punctuation, sentence clarity, and minor wording cleanup"
tags: [Production, Quality]
connections:
  - target: llm-service
    type: runs_on
context_params:
  voice_profile:
    label: "Voice Profile"
    description: "Creator's writing style, vocabulary, sentence patterns, and banned words"
    required: false
  grammar_strictness:
    label: "Grammar Strictness"
    description: "How strict to be with grammar rules — Casual, Conversational, Professional, or Academic"
    default: "Professional"
    required: false
---

## Capability

Corrects spelling, grammar, and punctuation errors. Improves sentence clarity. Standardises British English throughout.

## What It Does

1. **Spelling and grammar** — corrects errors
2. **Punctuation** — fixes missing or misplaced punctuation
3. **Sentence clarity** — simplifies convoluted phrasing without changing meaning
4. **Consistency** — standardises British English spelling throughout

## Outputs

Polished text with corrections applied.
