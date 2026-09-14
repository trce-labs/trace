# Trace Implementation Documentation

Trace remembers where you left off.

This documentation describes a complete path from the smallest local Rust implementation to cloud-backed context sync between machines for any kind of worker: human, AI agent, automation, or system process.

The product must stay simple at the surface. Trace should feel like a quiet continuity layer: record the point where work stopped, then make resuming obvious.

## Reading Order

1. [Product Principles](./01-product-principles.md)
2. [System Shape](./02-system-shape.md)
3. [Domain Model](./03-domain-model.md)
4. [Local Storage](./04-local-storage.md)
5. [Core Library API](./05-core-library-api.md)
6. [CLI Experience](./06-cli-experience.md)
7. [References And Artifacts](./07-references-and-artifacts.md)
8. [Change Detection](./08-change-detection.md)
9. [Worker Continuity](./09-worker-continuity.md)
10. [Local UX Polish](./10-local-ux-polish.md)
11. [Cloud Sync Model](./11-cloud-sync-model.md)
12. [Security And Privacy](./12-security-and-privacy.md)
13. [Testing Strategy](./13-testing-strategy.md)
14. [Implementation Roadmap](./14-implementation-roadmap.md)

## Non-Negotiables

- Trace is not a generic AI memory system.
- Trace is not a vector database.
- Trace is not an agent framework.
- Trace is not a personal data platform.
- Trace is a continuity product.

The implementation can grow into powerful infrastructure, but every module should justify itself by improving the ability to resume work.

