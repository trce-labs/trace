# Core Library API

Trace should have a clean Rust library API before it has a polished CLI or cloud sync.

## API Goals

The API should be:

- small
- explicit
- hard to misuse
- independent of CLI formatting
- usable by humans, agents, and tests

## Core Operations

Minimum operations:

- create thread
- list threads
- get thread
- update thread metadata
- add checkpoint
- get latest checkpoint
- list checkpoints

Conceptual shape:

```text
create_thread(input) -> Thread
update_thread(thread_id, input) -> Thread
add_checkpoint(thread_id, input) -> Checkpoint
latest_checkpoint(thread_id) -> Option<Checkpoint>
list_checkpoints(thread_id) -> Vec<Checkpoint>
```

## Checkpoint Input

Checkpoint creation should require:

- `summary`
- `next_action`

Optional:

- `changed`
- `references`
- `worker`

The product should make it difficult to create an empty checkpoint. Empty checkpoints are false continuity.

## Resume Output

A resume operation can be a convenience wrapper around latest checkpoint retrieval.

It should return:

- thread title
- latest checkpoint summary
- next action
- changes since previous checkpoint
- references
- timestamp
- worker

This can later power CLI, desktop UI, and agent prompts.

## Store Trait

Define storage behind an interface.

The service layer should not know whether records live in SQLite, a test in-memory store, or a future cloud-backed local cache.

The trait should express domain operations, not raw SQL.

## Error Model

Use typed errors.

Useful categories:

- not found
- validation failed
- storage failed
- conflict
- unauthorized
- sync unavailable

Do not expose database error strings directly through the user-facing layer.

## Validation

Validate at service boundaries:

- title is not blank
- summary is not blank
- next action is not blank
- reference targets are not blank
- timestamps are valid

Keep validation strict enough that Trace data remains useful.

