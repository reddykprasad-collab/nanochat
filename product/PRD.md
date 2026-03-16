# nanochat Production Readiness PRD

## Problem
nanochat is a research harness, not a production system. 
Gaps exist in observability, safety, and cost controls.

## Current State (v-today)
- No per-session token logging
- No content moderation layer
- No cost tracking or budget guardrails
- No conversation memory across sessions
- Single-user, no auth

## Feature 1: Token Usage Dashboard
User story: As an operator, I need to see token consumption 
per session so I can manage cost.
Acceptance criteria:
- Log input/output tokens per request to a local SQLite table
- Expose /metrics endpoint returning daily token totals
Success metric: Operator can see daily spend within 5 min 
of session end

## Feature 2: Safety Filter Layer
User story: As a deployer in a regulated context, I need 
requests screened before hitting the model.
Acceptance criteria:
- Pre-model hook checks prompt against blocked topic list
- Returns structured refusal with reason code, not model output
- Latency overhead < 50ms p95
Success metric: Zero unfiltered requests reach model for 
blocked categories in integration tests

## Feature 3: Conversation Memory
User story: As a user, I want the model to remember 
context across browser sessions.
Acceptance criteria:
- Session ID stored in cookie
- Last N turns retrieved from SQLite on new session load
- User can clear history via UI button
Success metric: 90% of returning users in usability test 
find context continuity useful

## What I'd Instrument
- Token count per request (input, output, total)
- Latency p50/p95 per request
- Refusal rate (safety filter hits / total requests)
- Session length (turns per conversation)
- Error rate by type (timeout, OOM, model error)