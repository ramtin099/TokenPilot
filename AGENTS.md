# AI Collaboration Rules

The repository is the source of truth for TokenPilot. Read `README.md`, `docs/roadmap.md`, `docs/architecture.md`, and `docs/current-status.md` before working.

## Roles
- **Owner:** decides scope, accepts milestones, and runs local checks.
- **ChatGPT (architect/reviewer):** sets a small next task, reviews changes against real code and evidence, identifies risks, and chooses the next step.
- **Codex (implementer):** inspects the actual environment, implements the agreed task, runs bounded tests, and records results and remaining limitations.

## Workflow
1. Begin with the next *single* unchecked task in the roadmap/status document. Check actual repository contents first; do not assume files or integrations exist.
2. Make the minimum change needed to satisfy explicit acceptance criteria. Avoid speculative abstractions, premature frameworks and unrelated refactors.
3. For any statement about Codex logs, capabilities, usage semantics, or limits, cite the observed version/sample or authoritative specification in the discovery report. Unknown means **unknown**, not zero.
4. Document changes in `docs/current-status.md` with commit, what was verified, and next action. Update architecture decisions only when decisions actually change.
5. Report concise evidence (commands and results), scope changes, and blockers. Do not claim tests passed unless run.

## Privacy
- Never commit or print raw Codex JSONL sessions, prompts, responses, tool outputs, credentials, full environment dumps, or code from unrelated projects.
- For schema discovery, inspect at most five recent session files by default, process streams in bounded chunks, and produce sanitized event-shape examples only.
- Read-only discovery: do not change Codex configuration or authentication, create proxy routes, or require network services.
- Keep local state, databases, logs, export files and secrets ignored by Git.
- This repository is currently **public**. Treat all committed content as public.

## Technical rules
- Distinguish session totals from incremental events; never sum cumulative counters blindly.
- Context-window occupancy is **not** lifetime token usage.
- API-priced estimates are not ChatGPT subscription quota consumption.
- Keep observed, estimated and unavailable metrics separate, including source and timestamp.
- Start with Windows + Codex, .NET 10 + SQLite. Add React, SignalR, RTK, LiteLLM and Ollama only in their respective phases.
- Prefer clear methods and small modules; no god methods, no method-per-line fragmentation.
