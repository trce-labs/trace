# Local Storage

The first storage backend should be local, inspectable, and reliable.

## Recommended First Backend

Use SQLite.

SQLite is the best first serious backend because it gives Trace:

- transactions
- indexes
- durability
- simple local files
- good Rust support
- future sync staging tables
- easy inspection during development

Plain JSON files are simpler for the first hour, but SQLite becomes the better no-compromise foundation quickly.

## Storage Location

Use platform-appropriate data directories.

Examples:

- macOS: `~/Library/Application Support/Trace/trace.db`
- Linux: `~/.local/share/trace/trace.db`
- Windows: `%APPDATA%\Trace\trace.db`

Allow an override through an environment variable for tests and advanced users.

Suggested:

- `TRACE_HOME`
- `TRACE_DB`

## Tables

Initial tables:

- `threads`
- `checkpoints`
- `references`

Later sync tables:

- `sync_state`
- `sync_outbox`
- `remote_records`
- `device_keys`

## Durability Rules

Creating a checkpoint should be transactional.

One transaction should:

1. insert checkpoint
2. insert references
3. update thread current checkpoint
4. update thread timestamp

If any step fails, none of it should persist.

## Immutability Enforcement

The application should never update checkpoint content.

At the database level, you can also enforce this through conventions:

- no update path in the store trait
- tests that prove checkpoint update is impossible through public APIs
- optional triggers later if needed

The cleanest first implementation is API-level immutability.

## Indexes

Minimum indexes:

- checkpoints by `thread_id`
- checkpoints by `created_at`
- references by `checkpoint_id`
- threads by `status`

The most common query is "latest checkpoint for this thread."

## Backups

Local backup should remain simple:

- SQLite database file can be copied when closed
- later use SQLite online backup API

Do not build a backup product before Trace has a stable local model.

