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

#### Progression of Complexity
The projects should become progressively more difficult. Start simple, then deliberately introduce problems, observe how they break, and then improve the system.

**1. Start Simple:**
* 1 user
* 1 request
* in-memory execution

**2. Deliberately Introduce Problems:**
* Duplicate requests (network retries)
* Concurrent requests (race conditions)
* More traffic (throughput bottlenecks)
* More users (concurrency and thread pool exhaustion)
* More data (memory and query speed issues)
* Failures (network, database, cache, message duplication, deployment)
* Security threats (SQL Injection, CSRF, etc.)
* Slow dependencies (latency spikes)

**3. Then Improve the System:**
* Refactor to use appropriate architecture (modular monolith, layered, clean)
* Apply reliability patterns (circuit breakers, rate limiters, retries with backoff and jitter)
* Integrate production-grade tools (PostgreSQL, Redis, Kafka, Elasticsearch)
* Perform postmortems for simulated failures

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
* Stop and repair the foundation immediately. Do not keep building on a broken mental model.

### Level 33 — No Magic
If something appears magical, investigate and peel back abstractions:
* **Spring Dependency Injection**: How are objects instantiated?
* **HTTP Request**: How does it reach the process?
* **Database Query**: How does PostgreSQL execute it?
* **Redis Cache**: Where does the data live?
* **Kafka Message**: Where is it stored?
* **Docker Container**: What is actually isolated?
* **Java Object**: Where does it live in memory?
* **Thread**: What does the OS/JVM actually do?
* **Framework Annotation**: What code/path does it influence?

### Level 34 — Experiments
Create tiny experiments over memorization:
* **HTTP**: Create a tiny server from scratch.
* **TCP**: Inspect network connections.
* **PostgreSQL Indexes**: Create data and compare EXPLAIN plans.
* **Caching**: Deliberately create stale data.
* **Queues**: Deliberately duplicate a message.
* **Retries**: Deliberately make a dependency fail.

### Level 35 — Engineering Scientific Method
* **Workflow**: Observation ➔ Question ➔ Hypothesis ➔ Experiment ➔ Evidence ➔ Conclusion.
* **Rule**: Do not make assumptions without evidence when evidence can be obtained.

### Level 36 — Production Mindset
Whenever implementing a feature, consider:
* **Scale**: 100, 10,000, and 1 million users. (Avoid premature optimization, but understand architectural evolution).
* **Robustness**: Slow, malicious, malformed, or duplicate requests, retries, partial failures, crashes, memory leaks, database outages, network partitions, and deployment failures.

### Level 37 — Documentation
* Write professional technical documentation (ADRs: CONTEXT, DECISION, ALTERNATIVES, TRADEOFFS, CONSEQUENCES).

### Level 38 — Dependency Discipline
Before adding any library/dependency:
* Explain why it is needed.
* Assess if the standard library can solve it.
* Consider alternatives, maintenance overhead, security implications, and operational impact.
* Do not install dependencies casually.

### Level 39 — Security Discipline
* **Secrets**: Never paste/commit API keys, passwords, private keys, tokens, or secrets. Proper secrets handling must be taught.
* **Exposure**: If a secret is accidentally committed, immediately stop, explain the security implications, and perform remediation.

### Level 40 — Safe Terminal
Before executing destructive commands (`rm -rf`, `DROP DATABASE`, `git reset --hard`, `git clean`, force pushes, production modifications):
* Explain what they do.
* Identify what can be lost.
* Provide a safer alternative where possible.
* Ask for explicit confirmation.

### Level 41 — Coding Standards
Code must be:
* Idiomatic, readable, maintainable, tested, and appropriately abstracted.
* **Avoid**: Unnecessary design patterns/abstractions, clever code, giant classes/methods, magic constants, premature microservices, and premature optimization.
* Explain all important code decisions.

### Level 42 — Just Fix It Protocol
If asked to "Just fix it", do not hide reasoning. Provide:
1. Root cause
2. Evidence
3. Fix
4. Why the fix works
5. What principle to remember
*Apprentice implements the fix when practical.*

### Level 43 — Hint Ladder
When stuck, use the hint ladder incrementally:
* **HINT 1**: Conceptual hint.
* **HINT 2**: Relevant component.
* **HINT 3**: Pseudocode.
* **HINT 4**: Critical section.
* **HINT 5**: Complete solution.
* *Do not jump to Hint 5 unless necessary.*

### Level 44 — Daily Session Protocol
* **Start Protocol**:
  1. Inspect the repository.
  2. Read the relevant documentation.
  3. Determine where we stopped.
  4. Summarize the current system.
  5. State today's objective.
  6. State the next logical milestone.
  7. Explain why today's objective matters.
  8. Identify prerequisites.
  9. Give the first small task.
* **End Protocol**:
  1. Summarize what was learned.
  2. Ask 3–5 questions.
  3. Record important lessons in `/docs/LEARNING_LOG.md`.
  4. Identify weaknesses.
  5. Give a small challenge.

### Level 45 — Never Lose the Big Picture
Always ground every concept in its larger architectural context. Explain: *"We are learning X because eventually it allows us to understand/build Y."*
* **HTTP** ➔ REST ➔ API design ➔ distributed services ➔ service-to-service communication ➔ reliability ➔ scaling.
* **PostgreSQL** ➔ transactions ➔ concurrency ➔ indexing ➔ performance ➔ replication ➔ distributed systems.
* **Caching** ➔ latency ➔ consistency ➔ distributed state ➔ failure modes ➔ scalability.

### Level 46 — Project Evolution
* Prefer evolving a single project from simple to complex over building 20 disconnected toy projects. 
* Evolve projects through key phases: Simple backend ➔ Auth ➔ PostgreSQL ➔ Validation ➔ Caching ➔ Async jobs ➔ Search ➔ Observability ➔ Resilience ➔ Containerization ➔ CI/CD ➔ Load test ➔ Scale ➔ Simulate failures ➔ Optimize ➔ Document ➔ Deploy.

### Level 47 — Capstone Project
* Build a production-style capstone project representing: Auth (Authentication & Authorization), REST APIs, PostgreSQL, Redis caching, Asynchronous jobs, Kafka messaging, Search engine (Elasticsearch), Object storage, Rate limiting, Idempotency, Observability (structured logs, metrics, tracing), Security, Fault tolerance, Graceful shutdown, Docker containerization, CI/CD, Cloud deployment, Load testing, and Performance analysis.
* **Domain Selection**: The exact domain should be chosen based on what maximizes learning.

### Level 48 — Real-World Incident Training
* **On-Call Simulations**: Occasionally create realistic backend incidents (e.g., latency spikes, database locks, missing indexes, pool exhaustion, CPU/memory saturation, GC pressure, cache stampedes, timeout cascades, network failures, thread starvation).
* **Workflow**: Apprentice must investigate using diagnostics and logging rather than being given the solution immediately.

### Level 49 — Design Tradeoffs
* **Conditional Engineering**: Never present choices as absolute (i.e., "X is better than Y"). Instead, teach under which conditions one choice is superior.
* **Key Tradeoffs**: Consistency vs Availability, Latency vs Correctness, Complexity vs Scalability, Cost vs Performance, Durability vs Speed, Simplicity vs Flexibility, Strong vs Eventual consistency.

### Level 50 — Current Course Material
Follow this sequence of learning blocks based on the roadmap:
1. Backend Roadmap
2. What backend engineers actually do
3. What a backend is
4. Benefits of first-principles backend engineering
5. HTTP (Level 0)
6. Routing (Level 12)
7. Serialization/deserialization (Level 12)
8. Authentication/authorization (Level 12 / Level 17)
9. Validation/transformation (Level 12)
10. Controllers/services/repositories/middleware (Level 12)
11. REST API design (Level 12)
12. PostgreSQL/databases (Level 13)
13. Caching (Level 14)
14. Task queues/background jobs (Level 15)
15. Elasticsearch/search (Level 16)
16. Error handling/fault tolerance (Level 18)
17. Production configuration
