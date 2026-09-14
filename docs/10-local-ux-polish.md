# Local UX Polish

Apple-level sleekness means the product removes friction while preserving clarity.

## Minimal Surface

Users should only need a few concepts:

- thread
- stop
- resume
- history

Everything else should feel secondary.

## First-Run Experience

First run should create local storage automatically.

The user should not see setup unless something fails.

Good first experience:

```text
trace new "Write storage layer"
Created thread: Write storage layer
```

Bad first experience:

```text
No config found. Please initialize a Trace database and choose a backend.
```

## Error Messages

Errors should be direct and helpful.

Examples:

- `No thread found for "auth". Run trace list to see active work.`
- `A checkpoint needs both --summary and --next.`
- `Could not open Trace database at ...`

Avoid raw internals unless debug mode is enabled.

## Defaults

Strong defaults:

- local SQLite storage
- human-readable output
- current user as worker name if known
- active threads shown first
- latest checkpoint shown by default

## Visual Simplicity

CLI formatting should use:

- whitespace
- short labels
- restrained color
- stable ordering

Do not overdecorate output.

## Speed

Common operations should feel instant:

- `trace resume`
- `trace stop`
- `trace list`

If sync is enabled later, local operations should not wait on the network unless explicitly requested.

## Trust

The user should feel that Trace is reliable.

That means:

- no lost checkpoints
- no silent overwrites
- clear sync state later
- honest conflict handling
- exportable local data

Sleekness without trust is just gloss.

