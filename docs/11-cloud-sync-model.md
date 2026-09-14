# Cloud Sync Model

Cloud sync should preserve the local-first product.

Trace should continue to work offline. The cloud should move continuity records between machines, not become the only source of truth for normal use.

## Sync Goal

Given two machines signed into the same Trace account, a checkpoint recorded on one machine should become available on the other machine.

The user should be able to stop work on one machine and resume on another.

## Sync Principles

- local writes first
- append-only checkpoints
- deterministic merge
- no silent data loss
- sync metadata separate from product metadata
- encrypted transport
- clear sync status

## Data To Sync

Sync:

- threads
- checkpoints
- references
- small owned artifacts, if introduced later

Do not sync:

- local absolute paths as authoritative truth
- transient CLI display state
- local cache internals
- raw command outputs unless explicitly captured

## Record Model

Use immutable records where possible.

Checkpoint records are append-only and sync cleanly.

Thread records are mutable and need conflict handling.

## Device Identity

Each machine should have a device identity:

- `device_id`
- creation time
- public key later if using end-to-end encryption

Each synced record should include:

- record ID
- record type
- schema version
- device ID
- created or updated timestamp
- content hash

## Sync State

Local sync state should track:

- last successful sync time
- remote cursor or version
- pending local records
- failed uploads
- failed downloads

This state is not product data. It can be rebuilt or repaired.

## Upload Flow

1. User creates checkpoint locally.
2. Store writes checkpoint in one transaction.
3. Store adds record to sync outbox.
4. Sync engine uploads pending records.
5. Cloud confirms receipt.
6. Local sync state marks record as uploaded.

The checkpoint exists locally even if upload fails.

## Download Flow

1. Sync engine asks cloud for records after last cursor.
2. Cloud returns records.
3. Local store validates schema and hashes.
4. Local store inserts missing immutable checkpoints.
5. Local store merges mutable thread updates.
6. Local store advances sync cursor.

## Conflict Handling

Checkpoint conflicts should be rare because checkpoints are immutable and uniquely identified.

Thread conflicts can happen when two machines edit the same title or status.

Initial conflict rule:

- latest update wins for thread metadata
- never delete checkpoint history
- preserve both sides if a destructive action conflicts

Later, expose conflicts in UI if needed.

## Cloud API

Conceptual endpoints:

```text
POST /records
GET /records?cursor=...
GET /devices
POST /devices
```

Keep the cloud API record-oriented. Do not mirror every local service method remotely.

## Account Model

Cloud sync requires identity, but the local product should not.

Initial account concepts:

- account ID
- device ID
- auth token

Do not build teams, organizations, sharing, or permissions in the first sync version.

## Sync UX

Sync status should be visible but quiet:

- `Synced just now`
- `Offline, 3 changes pending`
- `Sync failed: authentication expired`

The user should never need to understand cursors, outboxes, or merge algorithms.

## End-To-End Encryption

If Trace stores sensitive work context in the cloud, end-to-end encryption should be a serious design option.

Do not bolt this on casually.

If chosen, design around:

- device keys
- account recovery
- key rotation
- lost devices
- encrypted search limitations

Until this is designed properly, document cloud sync as trusted-server encrypted transport and encrypted storage, not E2EE.

