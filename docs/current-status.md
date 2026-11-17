# Current Status

Last updated: 2026-11-17

## Current milestone
**Phase 1A — Codex data-source discovery (not yet executed on the user's PC).**

## Verified
- GitHub repository `ramtin099/TokenPilot` exists and is writable through the linked GitHub integration.
- The repository was initially empty and is currently public.
- Repository planning/documentation was initialized.

## Not yet verified
- Installed Codex version, event log schema or local session paths.
- Availability/behavior of app-server usage or rate-limit endpoints.
- Accuracy of token accounting, context metrics or project attribution.
- Presence of .NET 10, Node or any local TokenPilot runtime.

## Next action
Use Codex on the Windows development machine to perform a **bounded, metadata-only discovery** of at most five recent session files. Save the sanitized results to `docs/codex-discovery.md`. No application implementation until results are reviewed.

## Acceptance evidence
When phase 1A is complete, record the inspected Codex version, source paths in anonymized form, field semantics, any unsupported data, and the commit that contains the report. Never upload session logs.
