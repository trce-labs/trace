# Domain Model

The domain model should be small, stable, and easy to explain.

## Work Thread

A work thread is the thing that continues over time.

It represents an ongoing line of work such as:

- "Fix login redirect"
- "Draft launch post"
- "Investigate flaky CI"
- "Continue Rust storage layer"

Suggested fields:

- `id`
- `title`
- `status`
- `created_at`
- `updated_at`
- `current_checkpoint_id`

Mutable fields:

- `title`
- `status`
- `updated_at`
- `current_checkpoint_id`

The thread is mutable because it is a convenience object.

## Checkpoint

A checkpoint is a stopping point.

It records what a future worker needs to resume. It should be immutable once written.

Suggested fields:

- `id`
- `thread_id`
- `parent_checkpoint_id`
- `created_at`
- `worker`
- `summary`
- `next_action`
- `changed`
- `references`
- `schema_version`

Immutable fields:

- all checkpoint fields

If a checkpoint is wrong, create a new checkpoint that corrects it.

## Worker

A worker is whoever or whatever produced a checkpoint.

Suggested fields:

- `kind`
- `name`
- `id`

Initial worker kinds:

- `human`
- `agent`
- `system`

Keep this simple. Do not model agent vendors, model names, prompts, or tool permissions in the core checkpoint yet.

## Reference

A reference points to supporting evidence.

Suggested fields:

- `kind`
- `target`
- `label`
- `metadata`

Initial reference kinds:

- `file`
- `url`
- `command`
- `commit`
- `issue`
- `note`

References should not be required. A checkpoint with no references can still be useful.

## Thread Status

Start with:

- `active`
- `paused`
- `done`
- `archived`

Avoid complex workflow states. Trace tracks continuity, not project management.

## Identity

Use stable opaque IDs.

Recommended:

- UUIDv7 or ULID for sortable IDs
- canonical string representation

Sortable IDs are helpful because checkpoints are naturally time-ordered, but do not rely on ID order as the only source of truth. Store `created_at`.

## Schema Versioning

Every persisted record should include a schema version from the start.

This is cheap early and valuable later.

Use versions to migrate records intentionally instead of guessing shapes from missing fields.

