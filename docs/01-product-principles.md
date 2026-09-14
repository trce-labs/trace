# Product Principles

## Core Definition

Trace remembers where you left off.

That sentence is the product boundary. Any feature that does not help a worker resume from a stopping point should be deferred.

## The User Promise

When a worker stops, Trace captures enough context that the next worker can continue without reconstructing the situation from memory, history, terminal scrollback, chats, browser tabs, or commit diffs.

The next worker may be:

- the same human
- a different human
- the same AI agent
- a different AI agent
- an automation

The product should not expose that complexity. At the interface level, Trace should simply answer:

- What was being worked on?
- What was true when work stopped?
- What changed?
- What should happen next?
- Where is the supporting evidence?

## Design Standard

The end-user experience should be Apple-level simple:

- few visible concepts
- elegant defaults
- no configuration before value
- no noisy terminology
- no raw database thinking exposed to users
- no AI-branded complexity unless the user explicitly needs it

The internal system may be rigorous, but the surface should feel calm.

## Product Vocabulary

Use plain words.

Preferred:

- work
- thread
- checkpoint
- resume
- reference
- worker

Avoid:

- memory graph
- vector memory
- agent brain
- knowledge substrate
- orchestration layer
- semantic index

## Core Product Loop

Trace has one core loop:

1. A worker works.
2. The worker stops.
3. Trace records a checkpoint.
4. Later, a worker resumes from the latest checkpoint.
5. The worker creates another checkpoint when stopping again.

Everything else exists to improve that loop.

## First Product Boundary

The first complete product should do this locally:

- create a work thread
- append immutable checkpoints
- show the latest checkpoint clearly
- show checkpoint history
- attach simple references
- compare the latest checkpoint to the previous one

Cloud sync comes later, after the local data model is boring and correct.

