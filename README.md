# TokenPilot

Local-first monitoring of AI coding-tool token usage, context and costs, starting with **Codex on Windows**.

> Status: **Phase 1A — Codex data-source discovery**. No collector or dashboard has been implemented yet.

## Goals
- Measure Codex token usage by session, model and project without double counting.
- Distinguish **observed**, **estimated** and **unavailable** values.
- Inspect context indicators and account limits only when a reliable data source exists.
- Later extend to safe output optimization, API spending/budgets, and local models (Ollama).

## Phase 1 scope
- Read-only, metadata-only access to Codex session logs and supported account APIs.
- Bounded discovery first (at most five recent sessions), then design the collector around verified schemas.
- Incremental ingestion, restart-safe checkpoints and idempotent accounting.
- Run locally on Windows; no Docker, proxy or service installation for the first version.

## Planned stack
C# / ASP.NET Core (.NET 10), SQLite; React + TypeScript and SignalR only when a dashboard is warranted. Keep the implementation a small modular monolith.

## Project documents
- [Roadmap](docs/roadmap.md) — phases and acceptance gates
- [Architecture](docs/architecture.md) — boundaries and data rules
- [Current status](docs/current-status.md) — source-of-truth progress log
- [Collaboration rules](AGENTS.md) — how Codex and reviewers should work
- [Architecture decisions](docs/decisions/0001-local-first-read-only.md)

## Privacy and data integrity
**Never commit** Codex session logs, prompts, model responses, source code from other projects, credentials, or raw usage exports. This repository may be public. Only sanitized schemas and aggregate metadata may appear in examples. Account subscription limits and API billable costs must never be presented as the same metric.

## Immediate next task
Run the bounded **Phase 1A discovery** on the developer's Windows machine, document verified findings in `docs/codex-discovery.md`, and do not build the collector until the report has been reviewed.
