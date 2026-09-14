# Change Detection

Trace should begin with explicit change descriptions and add inference later.

## First Version

The worker supplies `changed`.

Example:

```text
Changed: Added SQLite schema and implemented checkpoint insert transaction.
```

This is simple, reliable, and keeps the first system understandable.

## Previous Checkpoint Comparison

Trace can show:

- current checkpoint
- previous checkpoint
- explicit `changed` field

This gives basic continuity without trying to infer truth from external systems.

## Local Project Change Detection

After the manual version works, add optional project-aware detection.

For Git repositories:

- current branch
- HEAD commit
- dirty files
- staged files
- untracked files

Do not store full diffs by default. Store enough to orient the worker and link to the repository state.

## Non-Git Change Detection

For non-Git work:

- file modification times
- selected watched paths
- manually attached references

Avoid building a full filesystem indexer early.

## Agent Work Change Detection

For AI agents:

- checkpoint before work begins
- checkpoint after work stops
- changed files
- commands run
- test results
- explicit final handoff

The agent should still produce a human-readable checkpoint. Machine evidence supports continuity, but does not replace the handoff.

## Rule

Inferred change should never silently overwrite explicit checkpoint text.

If inference disagrees with a checkpoint, show it as supporting context or a warning.

