---
layout: default
title: Distributed Systems Notes
permalink: /systems/
---

# Distributed Systems Notes

These are practical notes and checklists for building **real-time, low-latency, event-driven** systems:
WebSocket platforms, actor-based services, messaging pipelines, and workflow orchestration.

---

## Actor Model for Distributed Systems

The actor model provides strong isolation between components
and enables highly concurrent systems.

Benefits:

- fault isolation
- location transparency
- natural concurrency model

Technologies:

- Erlang/OTP (supervision trees, message passing, distribution)
- Microsoft Orleans (virtual actors, grains, scalability, reliability)
- Rust actor frameworks (e.g. Kameo) + async runtimes (Tokio)

Practical notes:

- Use actors to isolate stateful workflows (per user, per room, per instrument, per account).
- Use supervision/restarts to treat failure as a normal control-flow mechanism.
- Decide early where state lives: in-memory actor state vs external storage vs event log.

---

## Event-Driven Architecture

Event-driven systems decouple producers and consumers
using messaging infrastructure.

Common components:

- Kafka
- Redis streams
- RabbitMQ
- Redis pub/sub (fanout patterns, but know the trade-offs)

Advantages:

- scalability
- loose coupling
- real-time processing

Operational checklist:

- Define message contracts and versioning rules (schema evolution).
- Plan for idempotency and retries (exactly-once is rare; design for at-least-once).
- Decide on ordering guarantees per key/partition and what it means for correctness.
- Build dead-letter / poison-message handling from day 1.

---

## WebSockets at Scale (Chat/Streaming/Multiplayer)

Real-time products tend to converge on the same concerns:

- connection lifecycle and backpressure
- fanout patterns (room/topic/user)
- presence and state reconciliation
- horizontal scaling (sticky vs stateless gateways)
- pub/sub vs durable streams depending on delivery guarantees

Common building blocks:

- WebSocket gateways + internal pub/sub (Redis/RabbitMQ/Kafka depending on needs)
- actor-per-room / actor-per-user models for isolation and locality
- observability: connection counts, drops, queue depths, publish latency, p99 end-to-end

---

## Workflow Orchestration (Temporal.io)

Use a workflow engine when you need durability + retries + long-running coordination:

- infrastructure operations (VM restarts, DB upgrades)
- multi-step business processes with human-in-the-loop
- reliable timers and backoff policies

Design tips:

- keep activities idempotent; store side-effects behind idempotency keys
- model workflow state transitions explicitly (events, signals, queries)
- avoid hidden coupling between workflow code and external systems

---

## Real-Time APIs (Low Latency)

Key design goals:

- low latency
- high throughput
- predictable performance

Techniques:

- async runtimes
- caching layers
- connection pooling

What to measure (and publish internally):

- p50/p95/p99 latency, tail amplification under load
- queueing time vs compute time vs I/O time
- cache hit rates by tier + stampede behavior
- per-user rate limiting effectiveness and abuse patterns
