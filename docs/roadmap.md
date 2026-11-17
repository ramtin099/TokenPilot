# Roadmap

The guiding principle is **correct measurement before feature breadth**. Phases are sequential; only start the next after its acceptance gate.

## Phase 1 — Codex Monitoring

### 1A. Source discovery (CURRENT)
- [ ] Verify Windows, Codex installation/version, paths, .NET and Node availability.
- [ ] Safely inspect up to five recent JSONL sessions; identify usage records and cumulative vs incremental fields.
- [ ] Check app-server/account capabilities *only if supported by installed version*.
- [ ] Record the provenance, meaning and reliability of each desired metric.
- [ ] Write `docs/codex-discovery.md` with sanitized schema examples, known limitations and collector recommendation.

**Gate:** reviewed evidence that supports a safe, non-fictional accounting model. No production code in 1A.

### 1B. Minimal read-only collector
- [ ] Build a .NET 10 collector and SQLite persistence based on verified fields.
- [ ] Implement incremental ingestion, stable identities, checkpoints and restart recovery.
- [ ] Handle partial writes, duplicates, malformed/unknown records and log rotation without silently inventing usage.
- [ ] Tests prove idempotent ingest, exact tally semantics for fixtures and no raw message storage.

**Gate:** verified session/token totals for multiple concurrent sample sessions and a restart.

### 1C. Usable local reporting
- [ ] Show per-session, per-project and per-model usage from persisted records.
- [ ] Mark unavailable/estimated metrics explicitly; show source freshness.
- [ ] Expose only on loopback; choose CLI or lightweight local UI before committing to a dashboard.

**Gate:** owner can use the tool daily on Windows without Docker or proxy and reconcile selected numbers with evidence.

## Phase 2 — Context Intelligence
- [ ] Differentiate active-context metrics from lifetime/cumulative usage.
- [ ] Provide clearly labeled thresholds and suggestions, never automatic compaction.

## Phase 3 — Token Optimization
- [ ] Evaluate RTK integration and reversibility on representative tool outputs.
- [ ] Report tool-output reduction separately from *measured* change in model token usage.

## Phase 4 — API Costs & Budgets
- [ ] Collect documented API usage and price evidence; reconcile costs.
- [ ] Add an optional gateway only if hard spending limits are needed, and only for traffic that passes through it.

## Phase 5 — Ollama & Windows Integration
- [ ] Add observed local-model request metrics and optional Windows tray notifications.
- [ ] Keep the initial install simple; do not require Docker.

## Non-goals for the first release
- Proxying the Codex ChatGPT login flow.
- Automatic compaction or rewriting prompts.
- Treating ChatGPT subscription quotas as exact per-token currency costs.
- Saving prompt contents, raw sessions or other repositories' code.
