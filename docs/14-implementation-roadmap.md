# Implementation Roadmap

This roadmap builds Trace from a tiny local tool into cloud-synced continuity infrastructure without losing the original product definition.

## Phase 1: Local Foundation

Implement:

- domain types
- validation
- SQLite schema
- store trait
- SQLite store
- create thread
- append checkpoint
- latest checkpoint
- checkpoint history

Exit criteria:

- user can record where they stopped
- user can resume from the latest checkpoint
- checkpoints are immutable through public APIs

## Phase 2: CLI Product Loop

Implement:

- `trace new`
- `trace stop`
- `trace resume`
- `trace list`
- `trace history`
- `trace done`
- human-readable output
- JSON output

Exit criteria:

- the CLI is useful every day on one machine
- an agent can consume `--json`
- the output is quiet and polished

## Phase 3: References

Implement:

- file references
- URL references
- command references
- commit references
- reference display in resume output

Exit criteria:

- a checkpoint can point to the real work surface
- references are optional and easy to attach

## Phase 4: Project-Aware Context

Implement optional local helpers:

- detect Git repository
- record branch and HEAD
- record dirty file list
- attach changed files

Exit criteria:

- Trace can help with code projects without requiring Git
- inferred context supports the checkpoint instead of replacing it

## Phase 5: Worker-Neutral JSON Interface

Implement:

- stable JSON output for resume
- stable JSON input for checkpoint creation
- worker metadata
- agent-friendly error responses

Exit criteria:

- humans and agents can use the same core product
- no agent framework has been introduced

## Phase 6: Sync Preparation

Implement:

- device ID
- sync outbox
- record serialization
- content hashes
- idempotent import
- local sync state

Exit criteria:

- local database can produce and consume sync records
- repeated imports do not duplicate data

## Phase 7: Cloud Sync

Implement:

- account auth
- device registration
- record upload
- cursor-based download
- retry behavior
- sync status

Exit criteria:

- machine A can stop work
- machine B can resume it
- local use works while offline

## Phase 8: Security Hardening

Implement:

- credential storage
- redaction tools
- clear deletion behavior
- cloud storage hardening
- optional E2EE design prototype

Exit criteria:

- sensitive continuity data has a credible privacy story
- cloud sync is trustworthy enough for real work

## Phase 9: Native Sleekness

Only after the model is solid, consider:

- desktop menu bar app
- global shortcut
- polished native resume view
- background sync
- project detection
- editor integrations

Exit criteria:

- Trace feels invisible when not needed
- Trace is instantly available when work resumes

## Do Not Build Yet

Do not build these before Phase 7:

- vector search
- embeddings
- autonomous agents
- team permissions
- plugin marketplace
- generalized knowledge graph
- browser-wide capture
- always-on activity recording
- complex workflow states
- cloud-only mode

The first excellent version is local, focused, and reliable.

