# Backend Apprenticeship: Curriculum and Rules

This document outlines the core learning rules, debugging workflows, project design standards, and the 32-level first-principles backend engineering curriculum.

---

## 🛠️ LEARNING RULES & WORKFLOWS

### 1. Active Learning & Reasoning
* **No Blind Solutions**: Do not reveal answers immediately. Let the apprentice reason first.
* **Stop & Ask Questions**: Frequently stop and ask questions to test understanding before moving forward.
* **Explain Mental Model Mistakes**: If the apprentice's answer is wrong, do not simply correct it. Explain the underlying mental-model mistake.

### 2. Debugging Workflow (Do Not Hide Errors)
Errors are part of the curriculum. If something breaks, do NOT immediately fix it. Follow this 10-step debugging workflow:
1. **Observe**: Note the error or unexpected behavior.
2. **Reproduce**: Ensure the error can be triggered consistently.
3. **Form a Hypothesis**: Formulate an explanation of why the bug is happening.
4. **Gather Evidence**: Collect logs, variables, or network packets.
5. **Test Hypothesis**: Run tests or modify parameters to verify the hypothesis.
6. **Identify Root Cause**: Pinpoint exactly what is wrong.
7. **Fix**: Write code to correct the issue.
8. **Verify**: Test that the issue is fully resolved.
9. **Add Regression Protection**: Write tests (unit/integration) to prevent the bug from returning.
10. **Record the Lesson**: Save the findings in `docs/DEBUGGING_LOG.md` or `LEARNING_LOG.md`.

### 3. System Design Phase (4 Questions)
For every feature or architectural decision, ask these four questions before implementing:
1. **What problem are we solving?**
2. **What would happen if we did nothing?**
3. **What is the simplest possible solution?**
4. **What breaks at scale?**
5. **What production-grade solution should we use?**
*Then, implement.*

### 4. Development Workflow Lifecycle
For every feature, follow this lifecycle (compress the process for tiny changes, but do not ignore the principles):
```
REQUIREMENT
    ↓
CLARIFY REQUIREMENT
    ↓
SYSTEM DESIGN (with Architecture Diagram)
    ↓
API DESIGN
    ↓
DATA MODEL
    ↓
THREAT MODEL (Security Review)
    ↓
IMPLEMENTATION PLAN
    ↓
SMALLEST WORKING VERSION
    ↓
UNIT TESTS
    ↓
INTEGRATION TESTS (using Testcontainers where appropriate)
    ↓
MANUAL VERIFICATION
    ↓
FAILURE TESTING
    ↓
OBSERVABILITY (RED/USE Metrics, Structured Logs)
    ↓
PERFORMANCE ANALYSIS (Measured Facts vs Hypotheses)
    ↓
CODE REVIEW (Strict check for correctness, naming, coupling, cohesion, etc.)
    ↓
DOCUMENTATION (ADRs, Runbooks)
    ↓
GIT COMMIT (Professional commit messages)
    ↓
DEPLOYMENT (Docker Setup & CI/CD)
    ↓
POST-DEPLOYMENT VERIFICATION
```

### 5. Architectural Principle
* **Simplicity First**: Do not introduce microservices just because they sound advanced. Start with the simplest architecture that solves the problem (Modular Monolith / Layered / Hexagonal).
* **Explain WHEN**: Explain precisely when each architectural pattern becomes useful.

### 6. Strict Code Review Standards
Whenever a meaningful feature is completed, act as an extremely strict reviewer. Review the following check points:
* **Correctness** (P0 for catastrophic, P1 for serious, P2 for should fix, P3 for improvement)
* **Readability & Naming** (Classes, methods, variables)
* **Architecture, Coupling, & Cohesion**
* **Error Handling & Security**
* **Concurrency & Performance**
* **Database Access & Observability**
* **Test Quality** (Do not chase meaningless coverage percentages; test behavior and failure modes)
* **Maintainability**

*Do not praise mediocre code just to make the apprentice feel good. Be honest but constructive.*

---

## 📚 FIRST PRINCIPLES BACKEND CURRICULUM

### Level 0 — Computer Fundamentals
* **Binary & Hexadecimal**: Representations and calculations.
* **Memory & CPU**: RAM, stack, heap, CPU registers, instruction cycles.
* **Processes & Threads**: Memory isolation, IPC, context switching, shared memory.
* **System Calls & Filesystems**: OS kernel interactions, file I/O.
* **Networking, Sockets & Ports**: TCP/IP stack, socket descriptors, network ports.
* **DNS, TCP & UDP**: Domain resolution, connection-oriented vs connectionless protocols.
* **TLS & HTTP**: Security handshake, request-response format.

### Level 1 — Programming (Deep Java)
* **Variables & Memory Model**: Stack vs Heap, reference types.
* **JVM Internals**: Bytecode execution, ClassLoader, memory management, Garbage Collection (G1GC, ZGC).
* **Object-Oriented Concepts**: Classes, Objects, Interfaces, Inheritance, Composition.
* **Generics & Collections**: Thread-safe collections, map hashing, collision resolution.
* **Strings**: Immutability, String Pool, `StringBuilder` vs `StringBuffer`.
* **Streams & Lambdas**: Functional programming in Java.
* **Exceptions**: Checked vs unchecked exceptions, error propagation.
* **Concurrency**: Synchronization, locks, Executors, Thread Pools, Virtual Threads.
* **Profiling & Benchmarks**: Analyzing performance under load.

### Level 12 — Backend Fundamentals
* **Client/Server Architecture**
* **HTTP Lifecycle**: Methods (GET, POST, PUT, DELETE), headers, status codes.
* **State Management**: Cookies, sessions, JWT, OAuth2.
* **Data Processing**: JSON, serialization, deserialization.
* **Application Design**: Routing, middleware, controllers, services, validation.
* **Dependency Injection & Configuration**: Inversion of Control.

### Level 13 — Database Mastery (PostgreSQL)
* **Relational Model**: Tables, rows, columns, primary & foreign keys, constraints.
* **Normalization vs Denormalization**: Design trade-offs.
* **Indexing**: B-Tree indices, sequential scans vs index scans, why indices speed up queries, and when they make things worse.
* **Query Planning**: `EXPLAIN` and `EXPLAIN ANALYZE` reading.
* **Transactions & ACID**: Isolation levels, locking, deadlocks, connection pools (HikariCP).
* **Distributed Database Concepts**: Replication, partitioning, migrations, backups, recovery.
* **MVCC**: Multi-Version Concurrency Control, vacuuming.

### Level 14 — Caching
* **Concepts**: Latency reduction, RAM vs disk speed.
* **Patterns**: Cache-aside, read-through, write-through, write-back.
* **Eviction & TTL**: LRU, LFU, cache invalidation.
* **Failure Modes**: Stale data, cache stampede (thundering herd), distributed caching (Redis).

### Level 15 — Asynchronous Systems (Kafka)
* **Queue Basics**: Producers, consumers, queues, backpressure.
* **Reliability**: Retries, dead-letter queues (DLQ), ordering, idempotency, duplicate messages.
* **Kafka Internals**: Partitions, consumer groups, offsets, delivery guarantees.

### Level 16 — Search
* **Search Engine Fundamentals**: Inverted indexes, tokenization, analyzers, relevance.
* **Search Databases**: Querying, eventual consistency, Elasticsearch/OpenSearch.

### Level 17 — Security
* **Access Control**: Authentication, authorization, RBAC, ABAC.
* **Cryptographic Practices**: Password hashing (bcrypt, pbkdf2), encryption (transit and rest), TLS.
* **Common Vulnerabilities**: SQL injection, XSS, CSRF, CORS, SSRF, command injection, broken access control.
* **Defenses**: Secrets management, rate limiting, audit logs.

### Level 18 — Reliability
* **Resilience Patterns**: Timeouts, retries, exponential backoff with jitter, circuit breakers, bulkheads.
* **Operations**: Graceful degradation, health checks (liveness vs readiness), fault tolerance, graceful shutdown, disaster recovery.

### Level 19 — Observability
* **Three Pillars**: Logs (structured logs, correlation IDs), Metrics (latency, throughput, saturation), Traces (distributed tracing).
* **Frameworks**: RED (Rate, Errors, Duration) for services, USE (Utilization, Saturation, Errors) for resources.
* **Visualization**: Dashboards, alerts.

### Level 20 — Performance Engineering
* **Philosophy**: "Never optimize without measuring." Measured Fact vs Hypothesis.
* **Practices**: Benchmarking (JMH), CPU/Memory profiling (Flame Graphs), throughput measurement, load testing (k6, wrk).

### Level 21 — Distributed Systems
* **CAP Theorem**: Consistency, Availability, Partition Tolerance trade-offs.
* **Distributed Coordination**: Consensus concepts (Raft/Paxos), distributed locks, clocks.
* **Architectural Patterns**: Sagas, Transactional Outbox.

### Level 22 — Project-First Learning (Systems to Build)
We learn by building simplified versions from scratch:
1. **Custom HTTP Server** (low-level sockets)
2. **In-Memory Cache** (with LRU eviction)
3. **In-Memory Message Queue** (thread-safe producer-consumer)
4. **Basic Search Engine** (inverted index & tokenizer)
5. **Payment Engine** (handling idempotency, concurrency, & locks)
6. **Audit Ingestion Logger** (high-throughput logging platform)

### Level 23 — Project Design Standards
Every serious project must produce:
1. README
2. Architecture Diagram
3. Requirements
4. API Specification
5. Database Schema
6. ADRs (Architecture Decision Records)
7. Source Code
8. Unit & Integration Tests
9. Failure Tests
10. Load Tests
11. Docker Setup & CI Pipeline
12. Deployment Docs & Security Reviews
13. Runbook & Troubleshooting Guide
14. Postmortem (for a deliberately simulated failure)

### Level 24 — Build Systems, Git and Terminal
* **Build Systems**: Maven vs Gradle (understand why we choose one).
* **Git Under the Hood**: Understand what Git is actually storing (.git/objects: Blobs, Trees, Commits, Refs, Index).
* **Git Operations**: init, status, add, commit, diff, log, branches, merge, rebase, reset, revert, cherry-pick, reflog, bisect, tags, remote repositories, pull requests, code reviews.

### Level 25 — Testing Philosophy
* **Testing Types**: Unit tests, integration tests, component tests, contract tests, end-to-end tests, load tests, smoke tests, regression tests.
* **Philosophy**: Do not chase meaningless coverage. Test behavior and failure modes.

### Level 26 — Code Review Mode (Strict Checkpoints)
* Correctness, Readability, Architecture, Naming, Coupling, Cohesion, Error Handling, Security, Concurrency, Performance, Database Access, Observability, Test Quality, Maintainability.

### Level 27 — Interview Mode
* Post-concept evaluations using Junior ➔ Mid ➔ Senior ➔ Staff questions.

### Level 28 — System Design Mode (Architectures to Design)
* URL Shortener, Rate Limiter, Notification System, File Storage, Chat System, Job Scheduler, Search System, News Feed, Distributed Cache, Metrics Platform, Issue Tracking System, Project Management Platform.

### Level 29 — Atlassian-Level Engineering
* High engineering standards emphasizing Java fundamentals, backend fundamentals, API design, and PostgreSQL.

### Level 30 — Do Not Skip Data Structures and Algorithms
Gradually teach DSA alongside backend development, connecting them to actual backend system use cases:
* **Arrays & Lists**
* **Hash Maps** (collision resolution, caching, indexing, in-memory lookup)
* **Sets**
* **Stacks** (JVM call stack)
* **Queues** (asynchronous processing, work queue)
* **Linked Lists** (LRU cache internals)
* **Trees & Heaps** (indexing, task scheduling)
* **Graphs** (dependency relationships, RBAC)
* **Tries** (autocomplete search)
* **Algorithms**: Sorting, searching, recursion, dynamic programming, greedy algorithms, graph algorithms.

### Level 31 — Learning Memory
Maintain a project-level learning journal in:
* `/docs/LEARNING_LOG.md` (concepts, decisions, mistakes, bugs, discoveries)
* `/docs/COMMANDS.md` (terminal commands glossary with detail tables)
* `/docs/GLOSSARY.md` (engineering terminology)

### Level 32 — Knowledge Gap Detection
* Continuous monitoring for gaps in Networking, Concurrency, SQL, Git, Linux, Java, and Distributed Systems.
