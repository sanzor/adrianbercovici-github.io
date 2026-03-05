---
layout: default
title: Projects — Adrian Bercovici
permalink: /projects/
description: Portfolio of Adrian Bercovici — real-time distributed systems projects including high-throughput APIs in Rust, Erlang/OTP actor systems, WebSocket infrastructure, and workflow orchestration with Temporal.io.
---

# Projects

This page highlights open-source work and portfolio projects related to **real-time**, **low-latency**,
and **event-driven** distributed systems (WebSockets, actors, messaging, orchestration).

## Selected Work (High-Level)

### High-Performance IP Intelligence & Scoring API (Rust)

- Built for real-time fraud detection / risk assessment with a multi-tier caching strategy and async background workers.
- Performance: **4,000 req/s** with **25ms p99** latency under load.
- Focus areas: cache efficiency, per-user rate limiting, observability dashboards, tail latency.

---

### Payment Processing Engine Re-Architecture (Erlang/OTP + Microsoft Orleans)

- Actor-based redesign of a high-performance payment engine achieving **25× throughput** improvement.
- Event-driven services and infrastructure (Kafka/Redis), plus event sourcing where appropriate.

---

### Workflow Orchestration Platform (Temporal.io)

- Built Temporal.io workflows to orchestrate long-running platform operations (e.g. VM restarts, DB upgrades).

---

### Adi-Chat (Erlang/OTP) — Real-time chat server with WebSocket clustering

- Scalable Erlang/OTP chat server design with WebSocket clustering and pub/sub fanout patterns.

---

## Open Source & Portfolio

## Audio DSP (Rust) — Real-time audio processing pipeline

Repo: https://github.com/sanzor/audio-dsp

Highlights:

- async Rust architecture
- actor-based backend design for real-time control (play/pause/record/seek)
- built with Rust async ecosystem (Tokio) + HTTP/WebSocket APIs

---

## Nova WebSocket Server (.NET) — WebSocket platform building block

Repo: https://github.com/sanzor/NovaWebsocketServer

Highlights:

- WebSocket server foundation for real-time systems
- relevant patterns: connection lifecycle, pub/sub fanout, horizontal scalability

---

## Ctesiphon (.NET) — Event-driven chat with Redis pub/sub + WebSockets

Write-up: https://bercovici-adrian-simon.medium.com/ctesiphon-chat-application-using-net-redis-pub-sub-and-websockets-bd12b8032f8b

Highlights:

- event-driven architecture
- Redis pub/sub message distribution
- WebSocket messaging patterns (fanout, backpressure considerations, scaling)

---

## Oituz Framework — Native Erlang WebRTC signalling

Repo: https://github.com/Oituz/Signalling

Highlights:

- Erlang signalling building blocks for real-time communication
- emphasis on concurrency, fault-tolerance, and distributed messaging

---

## Banking System (Erlang) — Actor-based account management

Repo: https://github.com/sanzor/Banking-Application

Highlights:

- concurrent account operations with isolation via actors
- foundations for distributed processing and fault isolation

---

## Publication — Real-time architecture research

IEEE: https://ieeexplore.ieee.org/document/8885509
