# ADR 0001 — Monorepo First

## Context
Order Signal has two main processes (API, Worker) and shared event contracts.  
We could split into multiple repositories or keep everything in a single repository.

## Decision
Adopt a **monorepo** for API, Worker and Contracts.

## Consequences
- ✅ Simplifies setup (one clone, one solution, one docker-compose).
- ✅ Easier for learning and showcasing in interviews.
- ✅ Contracts can be referenced directly by API and Worker.
- ⚠️ If the system grows, we can extract services and publish `OrderSignal.Contracts` as a NuGet package.
