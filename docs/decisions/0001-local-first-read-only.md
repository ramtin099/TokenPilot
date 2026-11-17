# ADR-0001: Local-first, read-only Codex integration

- **Status:** Accepted for the initial release
- **Date:** 2026-11-17

## Context
TokenPilot should monitor token usage without disrupting the user's Windows Codex workflow. Codex subscription usage, API billing and local-model telemetry have different semantics and interfaces.

## Decision
Start with a local read-only Codex collector. Inspect available session metadata and supported account APIs. Use SQLite for normalized usage and checkpoints; do not require any proxy, Windows Service or Docker. Delay any UI and tool-output optimizer until usage fields and accounting behavior are verified.

## Consequences
- No interception of Codex login or requests.
- Certain metrics may be unavailable or only estimates; display them as such.
- Future API gateways and Ollama collectors are optional and independently gated.
- The reliability of event schemas and counters must be confirmed against the installed Codex version before choosing a stable storage schema.
