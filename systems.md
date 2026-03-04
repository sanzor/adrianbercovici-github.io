---
layout: default
title: Distributed Systems Notes
permalink: /systems/
---

# Distributed Systems Notes

Practical notes and checklists for designing **real-time, low-latency distributed systems**.

These patterns frequently appear in systems such as:

- WebSocket messaging platforms
- multiplayer backends
- trading / exchange infrastructure
- collaborative real-time applications
- streaming and event-driven platforms

The notes below summarize recurring design patterns from working with
actor-based systems, event-driven architectures, and real-time APIs.

---

## Actor Model for Distributed Systems

The **actor model** provides strong isolation between components and enables highly concurrent systems.

Actors communicate via asynchronous messages and encapsulate their state,
making them well-suited for distributed systems where failure is expected.

### Benefits

- fault isolation
- location transparency
- natural concurrency model
- scalable partitioning of stateful workloads

### Technologies

- **Erlang/OTP** – supervision trees, message passing, distributed nodes
- **Microsoft Orleans** – virtual actors (grains), automatic placement and scaling
- **Rust actor frameworks** (e.g. Kameo) + async runtimes (Tokio)

### Practical notes

- Use actors to isolate **stateful workflows** (per user, per room, per instrument, per account).
- Supervision/restarts allow failures to be treated as **normal control flow**.
- Decide early where state lives: **in-memory actor state vs external storage vs event log**.

---

## Event-Driven Architecture

Event-driven systems decouple producers and consumers using messaging infrastructure.

Instead of tightly coupled request/response flows, systems communicate through events
that can be consumed asynchronously by multiple services.

### Common components

- Kafka
- Redis Streams
- RabbitMQ
- Redis Pub/Sub (useful for fanout patterns, but understand delivery guarantees)

### Advantages

- scalability
- loose coupling between services
- natural support for real-time processing

### Operational checklist

- Define **message contracts and schema versioning rules**.
- Plan for **idempotency and retries** (exactly-once delivery is rare).
- Decide what **ordering guarantees** mean for correctness.
- Build **dead-letter / poison-message handling** from day one.

---

## WebSockets at Scale (Chat / Streaming / Multiplayer)

Real-time products tend to converge on the same architectural concerns:

- connection lifecycle and backpressure
- fanout patterns (room / topic / user)
- presence and state reconciliation
- horizontal scaling (sticky sessions vs stateless gateways)
- pub/sub vs durable streams depending on delivery guarantees

### Common building blocks

- WebSocket gateways + internal pub/sub layer
- actor-per-room / actor-per-user models for isolation
- message fanout through Redis, Kafka, or RabbitMQ

### Observability signals

Real-time systems require deep observability.

Important metrics include:

- active connection counts
- connection churn / disconnect rates
- queue depths and backpressure
- publish latency
- **p99 end-to-end message latency**

---

## Workflow Orchestration (Temporal.io)

Workflow engines provide **durability, retries, and long-running coordination**.

Typical use cases:

- infrastructure operations (VM restarts, DB upgrades)
- multi-step business processes
- distributed sagas and compensating actions
- reliable timers and retry policies

### Design tips

- Keep activities **idempotent**.
- Store side-effects behind **idempotency keys**.
- Model workflow state transitions explicitly using **events, signals, and queries**.
- Avoid hidden coupling between workflow code and external services.

---

## Real-Time APIs (Low Latency)

Designing APIs for latency-sensitive systems requires careful attention
to tail latency and resource contention.

### Goals

- low latency
- high throughput
- predictable performance

### Techniques

- async runtimes
- layered caching strategies
- connection pooling
- batching and backpressure control

### What to measure

- p50 / p95 / **p99 latency**
- queueing time vs compute time vs I/O time
- cache hit rates by tier
- tail latency amplification under load
- per-user rate limiting effectiveness