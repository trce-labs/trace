# System Shape

Trace should be built as a small Rust core with thin interfaces around it.

## Layers

The system should separate into these layers:

1. Domain model
2. Local storage
3. Core service API
4. CLI or UI surface
5. Worker integrations
6. Sync engine
7. Cloud transport

The first four layers are enough for the first local product.

## Recommended Crate Shape

Start as one crate. Split later only when real pressure appears.

Suggested internal modules:

- `domain`: types such as threads, checkpoints, workers, references
- `store`: persistence traits and local implementation
- `service`: user-facing operations
- `cli`: command handling and presentation
- `sync`: later, cloud synchronization

Do not begin with a workspace unless the codebase actually needs multiple crates.

## Dependency Direction

Keep dependencies flowing inward:

- CLI depends on service.
- Service depends on domain and store.
- Store depends on domain.
- Domain depends on almost nothing.
- Sync depends on service/store contracts, not CLI.

This keeps Trace portable across CLI, desktop app, daemon, and agent usage.

## First Complete Local Flow

The first useful flow should be:

1. User creates a thread.
2. User records a checkpoint.
3. User asks what to resume.
4. Trace displays the latest checkpoint.

No background process is required at first.

## Later Complete Sync Flow

The cloud-backed flow should be:

1. Machine A appends a checkpoint locally.
2. Sync uploads the immutable checkpoint.
3. Machine B downloads missing checkpoints.
4. Machine B recomputes latest thread state.
5. Worker resumes from the same continuity point.

The sync layer should move facts, not reinterpret them.

## Architectural Rule

Append-only checkpoint history is the foundation. Mutable thread state is a convenience view.

Do not put critical continuity data only in mutable fields.

