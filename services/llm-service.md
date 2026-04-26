---
type: service
id: llm-service
title: LLM Service
description: "Language model service for context analysis, prep document synthesis, and language polish"
tags: [Production, Tested]
connections: []
metadata:
  serviceType: llm
  auth_type: api_key
---

## LLM Service

This skrpt uses a language model for analytical and generative tasks. The LLM handles context gathering analysis, prep document synthesis, and language polish.

### Configuration

- **Temperature:** 0.3 for context gathering, 0.5 for prep synthesis
- **Max tokens:** 4,000 for context, 6,000 for synthesis

### Requirements

- A configured LLM provider in skrptiq settings
- No external network access required beyond your AI provider's endpoint
