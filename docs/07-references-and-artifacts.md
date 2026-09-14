# References And Artifacts

References connect a checkpoint to evidence.

They let a future worker jump from the handoff note to the actual work surface.

## Principle

Trace should initially reference artifacts, not own them.

Do not copy every file, transcript, command output, or browser page into Trace by default.

## Reference Types

Start with a small set:

- `file`
- `url`
- `command`
- `commit`
- `issue`
- `note`

Each reference needs:

- kind
- target
- optional label
- optional metadata

## File References

A file reference should store:

- path
- optional line
- optional repository root

Prefer relative paths when inside a project. They survive machine-to-machine sync better than absolute paths.

## Command References

A command reference should store the command text and optional result summary.

Do not store full command output by default. Large outputs can become noise and may contain secrets.

## Commit References

For Git projects, a commit reference can store:

- repository identifier
- commit hash
- optional branch

Do not require Git. Trace must work outside code repositories.

## Notes

A note reference is inline supporting context that does not belong in the main checkpoint.

Use this sparingly. If the note is essential to resuming, it probably belongs in the checkpoint summary or next action.

## Artifact Ownership Later

Later Trace may own selected artifacts:

- screenshots
- command outputs
- generated summaries
- small text snapshots

When this happens, owned artifacts should be content-addressed and referenced by checkpoint records.

Do not build this until references prove insufficient.

