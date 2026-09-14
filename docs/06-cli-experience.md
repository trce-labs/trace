# CLI Experience

The CLI should be the first complete interface because it is fast to build, scriptable, and natural for a Rust project.

## Design Goal

The CLI should feel calm and minimal.

It should avoid exposing database concepts. Users should not need to understand storage, schema, sync internals, or worker metadata to get value.

## First Commands

Suggested commands:

```text
trace new "Fix login redirect"
trace stop <thread> --summary "..." --next "..."
trace resume <thread>
trace list
trace history <thread>
trace done <thread>
```

Short aliases can come later.

## Resume Display

`trace resume` should present the latest checkpoint as a focused handoff:

```text
Fix login redirect

Last stopped: 2026-09-15 18:41
Worker: Ayush

State
OAuth callback now reaches the app, but session creation fails after provider redirect.

Changed
Added callback route and verified provider config.

Next
Inspect session cookie creation in auth middleware.

References
src/auth/callback.rs
commit abc123
```

This output is the product.

## Stop Flow

Recording a checkpoint should be fast.

At minimum:

```text
trace stop <thread> --summary "..." --next "..."
```

Later, support editor-based input:

```text
trace stop <thread> --edit
```

Do not require users to fill every field.

## Thread Selection

Early version:

- use thread ID
- allow title search once list grows

Polished version:

- fuzzy selection
- recent threads first
- clear status labels

## Output Modes

Support:

- human-readable text
- JSON for agents and scripts

Example:

```text
trace resume <thread> --json
```

This gives agents a stable interface without making the product agent-first.

## CLI Polish

Small details matter:

- aligned labels
- short success messages
- no noisy stack traces
- useful validation messages
- consistent date formatting
- color only when output is a terminal
- no color in JSON

The CLI should feel designed, not dumped.

