# Worker Continuity

Trace should support any worker without becoming an agent framework.

## Worker Definition

A worker is an actor that can stop and resume work.

Worker kinds:

- human
- agent
- system

Trace does not need to know how a worker thinks. It only needs to record enough context for continuity.

## Human To Human

Flow:

1. Human A records checkpoint.
2. Human B runs resume.
3. Human B follows next action and references.
4. Human B records a new checkpoint.

This should work with no AI-specific fields.

## Human To Agent

Flow:

1. Human records checkpoint.
2. Agent reads resume output in JSON.
3. Agent uses summary, next action, and references to continue.
4. Agent records a new checkpoint.

The agent should not need private internal Trace APIs.

## Agent To Human

Flow:

1. Agent records checkpoint.
2. Human runs resume.
3. Human sees what changed, what passed or failed, and what to do next.

Agent checkpoints must be written for humans, not just machines.

## Agent To Agent

Flow:

1. Agent A records checkpoint.
2. Agent B reads JSON resume output.
3. Agent B continues with the same thread.

This becomes possible if the checkpoint schema is stable and plain.

## Worker Metadata

Keep worker metadata minimal:

- kind
- name
- id

Optional later:

- tool version
- model name
- runtime environment
- permissions

Do not put these into the first user-facing mental model.

## Handoff Quality

A good checkpoint should be:

- specific
- short
- action-oriented
- grounded by references
- honest about uncertainty

Trace can later add quality checks, but the foundation is simply storing the handoff.

