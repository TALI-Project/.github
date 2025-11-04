# TALI · Task Adaptive Learning Interface

> Home automation that learns, explains, and acts safely.  
> *“Home Assistant knows what happens. TALI learns why.”*

![Status](https://img.shields.io/badge/status-private--preview-inactive) 
![License](https://img.shields.io/badge/license-All%20Rights%20Reserved-critical)
![Stack](https://img.shields.io/badge/stack-Java%2025%20LTS%20%7C%20Spring%20Boot%203.5%20%7C%20MQTT-blue)
[![Docs](https://img.shields.io/badge/docs-Compendium%20%26%20ADRs-informational)]([docs-repo])

---

## About TALI

**TALI (Task Adaptive Learning Interface)** is a local‑first, sandboxed, self‑evolving automation system that observes real activity in your home, learns patterns, and turns them into safe, explainable automations. TALI integrates with Home Assistant, MQTT, and local databases to build a causal picture of your environment and then synthesizes reusable “tools” to perform actions with guardrails and auditability.

**Highlights**
- **Local‑first privacy.** All learning runs on your hardware. Cloud use is opt‑in and vetted.
- **Sandboxed intelligence.** Learning, testing, and tools execute in isolated runtimes with quotas and kill switches.
- **Explainable actions.** Every suggestion and command traces back to inputs, hypotheses, and tool versions.
- **Self‑evolving.** From observed device traffic, TALI infers intent and auto‑generates parameterized tools for reuse.
- **Human‑friendly.** A consistent, professional persona for natural interaction across text and voice.

**Non‑goals (for now)**
- Always‑on cloud dependency
- Distributed multi‑home learning
- Full conversational AI beyond structured persona responses

> Not affiliated with Home Assistant. TALI simply learns alongside it.

---

## Architecture at a glance

Core modules (see Compendium for details):

- **Core Orchestrator**: lifecycle, scheduling, configuration, health
- **Sandbox Manager**: classloader/process isolation, quotas, snapshots, recovery
- **Message Bus**: in‑process pub/sub; MQTT for external observation and actions
- **Integration Layer**: HA API, MQTT, and database connectors; normalization
- **Learning Engine**: pattern mining, hypothesis generation and evaluation
- **Persona Engine**: tone strategy and user interaction surfaces
- **Toolbox Runtime**: executes generated tools; capability registry, versioning
- **Persistence**: PostgreSQL, Redis cache, Neo4j graph, DuckDB analytics, MinIO artifacts
- **Observability**: Prometheus, Grafana, Loki, OpenTelemetry

**Runtime model:** single process with multiple isolation domains; external infra (MQTT, DB, observability) in separate containers. See Compendium in the docs repo.

---

## Organization repositories

Planned modules and adapters under this org:

- `tali-core` — central orchestrator and event backbone
- `tali-learning` — learning engine, sandbox evaluation, hypothesis scoring
- `tali-persona` — persona logic and interaction policies
- `tali-messenger` — text I/O bridge; intent parsing to structured payloads
- `tali-voice` — ASR/TTS pipeline management, voice session control
- `tali-dataservice` — Postgres/Redis/Neo4j/DuckDB abstractions and migrations
- `tali-analytics` — metrics, tracing, anomaly detection and dashboards
- `tali-ingress` — Home Assistant/MQTT/DB ingestion and normalization
- `tali-actuator` — command dispatch with policy and safety checks
- `.github` — org profile, issue templates, and automation
- `docs` — **separate repository** housing the Compendium and ADRs

Repository names and boundaries may evolve as the system stabilizes.

---

## Documentation

- **TALI Docs repository:** [Compendium and ADRs]([docs-repo])  
  Current Compendium: **1.0.0-LD** (28th Oct 2025, Adam Nicholls)

Planned additions in the docs repo:
- Quickstart and deployment guides (Hybrid vs Containerized)
- API references (Sandbox Contract, Capability Registry)
- Security & privacy whitepaper

---

## Status and access

- **Visibility:** Code is private for now. Read‑only access may be granted to selected collaborators.
- **Contributions:** External contributions are paused until the first public milestone. Internal development follows an RFC‑based process.
- **Releases:** Versioning will follow SemVer once repositories are public.

---

## Security & privacy

TALI is designed to be safe by default:
- Local‑first computation, with explicit consent for any cloud offload.
- Capability‑based sandboxing with per‑sandbox quotas, timeouts, and circuit breakers.
- Full audit trail of actions including hypothesis and tool versioning.
- Data retention policies and HA backfill duration are configurable.

**Responsible disclosure:** until public launch, report security concerns to the maintainers via private channels listed below.

---

## Licensing

**All Rights Reserved.** Copyright © 2025 Adam Nicholls.  
Unless otherwise noted, no permission is granted to copy, modify, merge, publish, distribute, sublicense, create derivative works, or publicly display any part of the code or documentation. Forks and redistributions are prohibited without prior written permission.

> The team may relicense some components under an open‑source license in a future release. Until that happens, the above terms apply.

---

## Getting started (internal)

Internal developers can use the dev stack while the code remains private.

**Prerequisites**
- JDK 25 (LTS)
- Docker and Docker Compose
- Home Assistant with an MQTT broker (EMQX or Mosquitto)
- Postgres, Redis, Neo4j, DuckDB, MinIO, Prometheus, Grafana, Loki

**Typical flow**
```bash
# 1) Start local infrastructure
docker compose -f dev/docker-compose.yml up -d

# 2) Run Core during development
./gradlew :tali-core:bootRun

# 3) Watch metrics and logs
open http://localhost:3000   # Grafana
```

Refer to the Compendium for hardware sizing and sandbox policies.

---

## Trademarks

“TALI” and “Task Adaptive Learning Interface” are trademarks of their respective owner(s). Home Assistant is a trademark of its respective owner. No affiliation or endorsement is implied.

---

## Contact

- General: to be announced at public launch
- Security: private channel during preview
- Press/Partnerships: private channel during preview

---

<sub>Org profile README updated 2025-11-04. Compendium reference: 1.0.0-LD (28th Oct 2025).</sub>


<!-- Update the link below to your dedicated docs repository URL -->
[docs-repo]: https://github.com/INSERT-ORG/INSERT-DOCS-REPO

