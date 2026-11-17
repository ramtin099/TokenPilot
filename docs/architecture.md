# Architecture (proposed; not implemented)

## Runtime concept
```text
Codex JSONL / supported account APIs
                 |
         Read-only Collector
                 |
       Normalization + Evidence
                 |
    Deduplication / Checkpointing
                 |
             SQLite
                 |
      Local reporting interface
```

The first release is a **single local process** on Windows. No service, proxy, Docker, distributed components or extra database. API and Ollama integrations are future independent adapters.

## Boundaries
1. **Source readers** inspect Codex session/event metadata and optionally account endpoints supported by the installed version. They must tolerate schema/version differences.
2. **Usage normalization** maps source records into explicit usage measurements with identity, provenance, timestamps, units, cumulative/incremental semantics and confidence.
3. **Accounting** selects the correct deltas/snapshots, deduplicates retries/overlapping records and attributes usage by session, project and model only when evidenced.
4. **Storage** retains normalized usage metadata, ingestion checkpoints and schema-version information. It does not retain message bodies.
5. **Reporting** exposes numbers with source and freshness. Unknowns remain visibly unknown.

## Core invariants
- **Idempotence:** importing the same unchanged file twice does not increase totals.
- **Monotonicity where valid:** cumulative counters may reset or change semantics; resets must be handled as source-specific events, not blindly subtracted.
- **Attribution integrity:** missing project/model attribution stays unassigned, not guessed.
- **Separation:** active context occupancy, lifetime tokens, account rate limits, API dollar estimates and optimization savings are different metric families.
- **Data minimization:** metadata-only local collection; do not commit raw customer or developer activity.
- **Resilience:** handle concurrent sessions, actively appended logs, incomplete trailing JSONL lines, unknown event types and unexpected format changes.

## Data model direction (subject to discovery)
Possible entities: SourceInstallation, Session, UsageObservation, IngestionCheckpoint and optional Project/Model attribution. Fields and keys are **not final** until `docs/codex-discovery.md` is reviewed; avoid defining persisted schemas based on guesses.

## Architecture choices
- C# / .NET 10 backend with SQLite for phase 1.
- React + TypeScript and SignalR are options for later, not prerequisites.
- RTK for optional tool-output optimization and LiteLLM for optional API gateway work only in later phases.
- Read-only access to Codex; never intercept authenticated ChatGPT subscription traffic.
