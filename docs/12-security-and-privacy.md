# Security And Privacy

Trace will hold sensitive context. Treat privacy as part of the core product, not a later checkbox.

## Local Privacy

Local data should live in the user's app data directory with normal OS file protections.

Do not write checkpoints to world-readable temp directories.

## Secrets

Checkpoints and references may accidentally include secrets.

Mitigations:

- avoid storing full command output by default
- avoid automatic environment capture
- avoid automatic clipboard capture
- provide clear delete/export controls later
- support redaction before sync

## Cloud Transport

Cloud sync must use TLS.

Authentication tokens should be stored using platform credential storage where possible.

## Cloud Storage

Minimum expectation:

- encrypted storage at rest
- access scoped to authenticated account
- audit-friendly server logs
- no public object URLs for private artifacts

## End-To-End Encryption Decision

E2EE is desirable for a product like Trace, but it affects:

- search
- recovery
- web access
- support
- sharing
- sync conflict tooling

Keep the architecture open for E2EE by separating:

- plaintext domain model
- serialization
- encryption envelope
- transport record

## Deletion

Deletion semantics should be explicit.

Early local product:

- archive threads
- avoid hard delete unless user explicitly asks

Cloud product:

- tombstones for synced deletes
- retention policy
- eventual remote deletion

Do not let sync resurrect data the user intentionally deleted.

## Agent Safety

Agents should only receive the context required to continue the selected thread.

Do not dump the entire Trace database into an agent by default.

Agent-facing output should be scoped, structured, and auditable.

