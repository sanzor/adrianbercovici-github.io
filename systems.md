---
layout: default
title: Distributed Systems Notes
permalink: /systems/
---

# Distributed Systems Notes

This section contains architectural notes on building real-time platforms.

---

## Actor Model for Distributed Systems

The actor model provides strong isolation between components
and enables highly concurrent systems.

Benefits:

- fault isolation
- location transparency
- natural concurrency model

Technologies:

- Erlang OTP
- Microsoft Orleans
- Rust actor frameworks

---

## Event-Driven Architecture

Event-driven systems decouple producers and consumers
using messaging infrastructure.

Common components:

- Kafka
- Redis streams
- RabbitMQ

Advantages:

- scalability
- loose coupling
- real-time processing

---

## Real-Time APIs

Key design goals:

- low latency
- high throughput
- predictable performance

Techniques:

- async runtimes
- caching layers
- connection pooling
