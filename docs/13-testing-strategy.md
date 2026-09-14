# Testing Strategy

Trace should be tested around continuity guarantees.

## Unit Tests

Test domain validation:

- blank titles fail
- blank summaries fail
- blank next actions fail
- invalid references fail
- checkpoint IDs are stable

## Store Tests

Test persistence behavior:

- thread creation persists
- checkpoint append persists
- latest checkpoint returns newest checkpoint
- history returns stable order
- checkpoint creation updates thread current pointer
- failed checkpoint transaction rolls back

## Immutability Tests

Prove through public APIs that:

- checkpoint content cannot be updated
- a correction creates a new checkpoint
- history remains intact

## CLI Tests

Test user flows:

- create thread
- stop work
- resume work
- list active threads
- view history
- mark done

CLI tests should assert useful output without being too brittle about whitespace.

## Sync Tests

When sync exists, test:

- upload pending local records
- download remote records
- idempotent repeated sync
- offline local writes
- conflict handling for thread metadata
- no duplicate checkpoints
- cursor advancement only after successful import

## Migration Tests

Every schema migration should have tests.

Test:

- old database opens
- migration preserves data
- migrated records validate

## Golden Resume Tests

Keep golden examples for resume output.

This protects the core product experience.

If `trace resume` becomes noisy or confusing, a test should catch it.

