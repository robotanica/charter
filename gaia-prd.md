# Gaia — Product Requirements Document

**System:** Gaia, the epistemic platform of Robotanica
**Version:** 0.1
**Status:** Draft for review
**Companion document:** Robotanica White Paper v0.2

---

## 1. Overview

Gaia is the integrated record of the biosphere as Robotanica observes it and understands it. It is one platform with two tightly-coupled layers:

- The **twin** — a planetary-scale spatial and temporal record of every parcel, cohort, tree, sensor reading, and remote-sensing observation under Robotanica stewardship. Canonical for *what is true on the ground*.
- The **codex** — a versioned, citable, contestable knowledge graph of species, ecosystems, intervention recipes, and their outcomes. Canonical for *what is known about how the biosphere works*.

The two layers are one platform because the feedback loop between them is the highest-leverage loop in the company: an observation in the twin is evidence that may update the codex; a recipe in the codex is a hypothesis the twin tests on the ground. Gaia is built so that this loop has the lowest possible latency and the strongest possible provenance.

Gaia is read by A3 (which selects recipes and verifies contract performance), by OpenFactory (which receives recipes and dispatches operations), and by every tier of agent. Gaia is written to by field robots and human operators (observations), satellites and sensors (telemetry), scientists and federation partners (codex contributions), and by Gaia's own derived-data pipelines.

---

## 2. Problem Statement

Robotanica's mission requires holding three things together over decades:

1. A continuously updated, planetary-scale spatial record of ecological state.
2. A living body of ecological knowledge — species, ecosystems, recipes — that evolves with evidence.
3. A high-fidelity feedback loop between the two, so that what happens on the ground updates what is believed, and what is believed updates what happens next.

No existing open-source platform integrates these three. GIS systems hold state but not knowledge. Knowledge graphs hold knowledge but not state. Survey/monitoring platforms hold both at small scale but not federated, not multi-decade, not provenance-strict. Gaia is built because the gap is structural, not incremental.

The companion problem is durability. Most data infrastructure is designed for a horizon of months to a few years. Gaia must remain queryable, interpretable, and trustworthy for fifty-plus years, across schema evolutions, organizational changes, and infrastructure migrations.

---

## 3. Goals and Non-Goals

### 3.1 Goals

- Be the canonical, queryable, planetary-scale record of every parcel, cohort, tree, and ecological observation under Robotanica stewardship.
- Be the canonical, versioned, contestable knowledge graph of species, ecosystems, and intervention recipes, with provenance from authorship through revision.
- Make the feedback loop between observation and interpretation explicit, low-latency, and audit-able.
- Serve A3, OpenFactory, agents, federation partners, and the public via a unified query surface.
- Preserve queryability and reproducibility across multi-decade timescales.
- Honor data sovereignty (regional and indigenous) at the storage and access-control layer, not as policy overlay.
- Be open-source and built on open-source components.

### 3.2 Non-Goals

- Gaia is not the contract or coordination platform — that is A3.
- Gaia is not the actuation or fleet platform — that is OpenFactory.
- Gaia does not host real-time machine telemetry from the shop floor — that is UMH (which feeds aggregate state into Gaia).
- Gaia does not implement legal-financial instruments — those live in A3.
- Gaia is not a general-purpose Earth observation platform; it is scoped to Robotanica's stewarded land plus the contextual data needed to interpret it.
- Gaia does not seek to replace existing scientific knowledge graphs (GBIF, iNaturalist, EOL, Plantnet); it interoperates with them.

---

## 4. Users and Personas

| Persona | Primary interaction | Concerns |
|---|---|---|
| Site steward | Reads parcel/cohort state; records field observations; raises alerts | Mobile-first UX, offline operation, low latency |
| Regional coordinator | Cross-site queries, cohort comparisons, recipe selection support | Aggregations, dashboards, exception detection |
| Scientist / contributor | Authors and revises codex entries; reviews evidence | Citation, peer review, version history |
| Landowner | Reviews state of their parcel; verifies obligations | Trust, comprehensibility, transparency |
| Auditor / certifier | Reads provenance and outcome records | Immutability, reproducibility, evidence chains |
| Federation partner (org) | Reads and contributes within scope | Multi-tenancy, sovereignty, rate limits |
| Public viewer | Reads non-sensitive aggregates | Transparency without exposing sensitive locations |
| **System actors** | | |
| A3 service | Reads recipes; reads parcel state; writes contract events | Stable contract, low latency |
| OpenFactory service | Reads recipes and operational state; writes operation events | Stable contract, durable writes |
| Agent (Tier 1) | Reads broadly for grounding; writes recommendations | RAG-friendly retrieval, citation chains |
| Agent (Tier 2) | Reads operational state; writes proposed actions | Strong typing, audit trail |
| Agent (Tier 3) | Reads narrow context; writes high-frequency observations | High write throughput, edge-friendly |

---

## 5. Core Concepts and Domain Model

The domain model is shared across the twin and the codex; the layers differ in storage and update semantics, not in identity.

### 5.1 Twin entities

- **Parcel** — a spatial polygon with a stable URI; the unit of land stewardship. May nest (sub-parcels within parcels).
- **Cohort** — a group of plants of common provenance, planted in a common event, on a common parcel, under a common recipe instance.
- **Plant** — an individual tree or other organism with a stable URI, position, species, and lifecycle state. Cohort-aggregated when individual tracking is impractical.
- **Observation** — an immutable record of something witnessed or measured: a sensor reading, a satellite image, a field inspection, a robot perception event, a mortality event. Has a timestamp, a source, a method, and a payload.
- **Episode** — a bounded period of conditions or interventions on a parcel/cohort: a drought, an irrigation campaign, a grazing rotation, a fire.
- **Outcome** — a derived assessment over a parcel/cohort/recipe instance at a point in time: survival rate, biodiversity index, soil carbon delta.

Twin entities are append-only at the observation layer. Derived state (current plant lifecycle, current parcel state) is materialized from the observation log and is reproducible from it.

### 5.2 Codex entities

- **Species** — a taxonomic entry, linked to external authorities (GBIF, Catalogue of Life). Includes ecological role, native range, holobiont associations.
- **Ecosystem** — a named ecosystem type with characteristic species, structure, and successional dynamics.
- **Recipe** — a versioned intervention template: target ecosystem, species mix, planting density, succession plan, tending operations, monitoring cadence, expected outcomes. Recipes are typed by methodology (Miyawaki, Savory, FMNR, etc.) and by region.
- **RecipeInstance** — the application of a recipe to a specific parcel/cohort. Bridges codex (the recipe) and twin (the parcel and cohort it was applied to).
- **Evidence** — a link from a codex entry to twin observations or external publications that support, contest, or refine it.
- **Revision** — an immutable record of a change to a codex entry, with author, rationale, evidence, and review status.

Codex entries are mutable through the revision protocol; every state at every point in time is recoverable.

### 5.3 Identity model (shared)

Every entity has a stable URI of the form:

```
gaia://<type>/<region>/<id>[@<version>]
```

URIs are durable across schema evolution. Versions apply to codex entries; twin entities are immutable per observation but have lifecycle state derived from the observation log.

---

## 6. Functional Requirements

Each requirement has an ID for traceability. Priority levels: **MUST**, **SHOULD**, **MAY**.

### 6.1 Twin: Spatial and Parcel Management

- **GAIA-T-001 (MUST)** Ingest and store parcel polygons with sub-meter precision, supporting nesting and overlap.
- **GAIA-T-002 (MUST)** Maintain parcel lifecycle state (proposed, committed, active, in-restoration, mature, withdrawn).
- **GAIA-T-003 (MUST)** Synchronize parcel rights from A3 as the source of truth for ownership and lease state.
- **GAIA-T-004 (MUST)** Support spatial queries (within, intersects, nearest, buffer) across the full global parcel set.
- **GAIA-T-005 (SHOULD)** Support spatial joins against external datasets (administrative boundaries, protected areas, climate zones).

### 6.2 Twin: Observations and Telemetry

- **GAIA-T-010 (MUST)** Accept observations from heterogeneous sources (satellite, drone, ground sensor, robot, human).
- **GAIA-T-011 (MUST)** Store every observation as immutable, with full provenance (source, method, device, operator, time).
- **GAIA-T-012 (MUST)** Ingest Sentinel-2, Landsat, Planet, and Maxar imagery on a regular cadence; index via STAC.
- **GAIA-T-013 (MUST)** Compute and store derived indices (NDVI, EVI, canopy cover, biomass estimates) per parcel per time step.
- **GAIA-T-014 (MUST)** Support time-series queries on sensor data with sub-second resolution where source data permits.
- **GAIA-T-015 (SHOULD)** Detect anomalies in observation streams (sudden NDVI drop, sensor offline, unexpected mortality signal) and emit alerts.
- **GAIA-T-016 (MUST)** Accept telemetry summaries from UMH (greenhouse environmental aggregates, fleet activity) without subscribing to the raw firehose.

### 6.3 Twin: Plant and Cohort Lifecycle

- **GAIA-T-020 (MUST)** Track cohorts from establishment through maturity, with lifecycle states (planned, planted, established, juvenile, mature, deceased, harvested).
- **GAIA-T-021 (MUST)** Track individual plants where individual tracking is operationally feasible; otherwise, track at cohort level with statistical sampling.
- **GAIA-T-022 (MUST)** Compute survival rate per cohort per time step, with explicit treatment of unknown-fate plants.
- **GAIA-T-023 (MUST)** Record genealogy: seed source, nursery batch, mycorrhizal inoculant batch, planting event.
- **GAIA-T-024 (SHOULD)** Track holobiont associations: pollinators observed, mycorrhizal status, companion species recruitment.

### 6.4 Codex: Knowledge Graph

- **GAIA-C-001 (MUST)** Maintain a knowledge graph of species, ecosystems, and recipes with stable URIs and versioning.
- **GAIA-C-002 (MUST)** Link species to external authorities (GBIF, Catalogue of Life, World Flora Online).
- **GAIA-C-003 (MUST)** Support recipes with structured fields (target ecosystem, species mix with proportions, density, succession plan, tending operations, monitoring cadence, expected outcomes).
- **GAIA-C-004 (MUST)** Type recipes by methodology and by bioregion; allow inheritance (a regional Miyawaki variant inherits from a methodology template).
- **GAIA-C-005 (MUST)** Link every codex entry to evidence: twin observations, external publications, expert testimony, traditional knowledge attestations.
- **GAIA-C-006 (SHOULD)** Surface contradictions and gaps (a recipe with no recent outcome evidence; a species with conflicting ecological role claims).

### 6.5 Codex: Authoring and Revision

- **GAIA-C-010 (MUST)** Support proposal-review-merge workflow for codex entries: draft, submit, peer review, accept, publish.
- **GAIA-C-011 (MUST)** Record every revision with author, timestamp, rationale, and evidence delta.
- **GAIA-C-012 (MUST)** Support the Science Council's veto authority as a first-class workflow state.
- **GAIA-C-013 (MUST)** Support contestation: any federation member can propose a revision; established review thresholds determine acceptance.
- **GAIA-C-014 (MUST)** Surface the full revision history of every entry; support point-in-time queries (the recipe as it existed on date X).
- **GAIA-C-015 (SHOULD)** Support multilingual authoring with language-tagged content fields and translation provenance.

### 6.6 Integration: Twin ↔ Codex Feedback Loop

- **GAIA-I-001 (MUST)** When a recipe is applied to a parcel, create a `RecipeInstance` linking the codex entry (versioned) to twin entities (parcel, cohort).
- **GAIA-I-002 (MUST)** Compute outcome metrics per RecipeInstance on a defined cadence (annual minimum, finer where data supports it).
- **GAIA-I-003 (MUST)** Surface aggregate outcomes per recipe across all instances: success rate by recipe, by region, by cohort age.
- **GAIA-I-004 (SHOULD)** Generate proposed codex revisions when outcome evidence diverges from recipe expectations beyond defined thresholds.
- **GAIA-I-005 (MUST)** Make every outcome trace-able: from aggregate, to instance, to underlying observations.

### 6.7 Integration: External Systems

- **GAIA-X-001 (MUST)** Expose parcel and recipe data to A3 via stable APIs; receive parcel-rights and contract events.
- **GAIA-X-002 (MUST)** Expose operational state and recipes to OpenFactory; receive operation events and biological-batch events.
- **GAIA-X-003 (MUST)** Publish events to the Robotanica event bus (Kafka/Redpanda) for: new observation, recipe revision, lifecycle transition, anomaly detected, outcome computed.
- **GAIA-X-004 (SHOULD)** Federate with external scientific knowledge graphs (GBIF, iNaturalist) for species and observation interchange.
- **GAIA-X-005 (SHOULD)** Expose a public read-only API and bulk-export interface for non-sensitive data.

### 6.8 Agent Support

- **GAIA-A-001 (MUST)** Provide a retrieval-augmented-generation interface over the codex with citation-preserving chunking.
- **GAIA-A-002 (MUST)** Provide structured query interfaces (SQL on the twin, GraphQL or SPARQL on the codex) for Tier 2 agents.
- **GAIA-A-003 (MUST)** Accept agent-authored proposals (recommendations, draft contracts, alerts) as first-class entities with `agent` provenance and required human-review state.
- **GAIA-A-004 (MUST)** Log every agent read and write to support evaluation and improvement.

---

## 7. Non-Functional Requirements

### 7.1 Scale

- **GAIA-N-001** Support 10⁹ plant-level entities and 10¹² observations within five years.
- **GAIA-N-002** Support 10⁶ parcels at full deployment.
- **GAIA-N-003** Sustain ingest of 10⁷ observations per day at peak (satellite ingest cadence).
- **GAIA-N-004** Codex scale is small relative to the twin (10⁵–10⁶ entries), but query patterns are graph-traversal-heavy.

### 7.2 Performance

- **GAIA-N-010** P95 latency for parcel state queries: < 200 ms.
- **GAIA-N-011** P95 latency for codex entry retrieval: < 100 ms.
- **GAIA-N-012** P95 latency for spatial-temporal queries over a single parcel's history: < 1 s.
- **GAIA-N-013** Planetary aggregations (e.g., total surviving cohorts by region) run as scheduled jobs; P95 < 1 hour.

### 7.3 Durability

- **GAIA-N-020** Observations are append-only with cryptographic chaining; no observation can be silently altered or deleted.
- **GAIA-N-021** Codex revisions are immutable; only forward revisions, never overwrites.
- **GAIA-N-022** All data is replicated across at least three regions; loss tolerance is zero for any committed observation or revision.
- **GAIA-N-023** Schema evolution preserves the ability to query data at any prior schema version (point-in-time reproducibility).
- **GAIA-N-024** Long-term archival format is open and standards-based (Parquet, GeoParquet, RDF, JSON-LD); no proprietary serialization in archived state.

### 7.4 Multi-Decade Operability

- **GAIA-N-030** Every query result is reproducible at any future date given the same input parameters and timestamp.
- **GAIA-N-031** The system carries a documented migration story: any component must be replaceable without data loss or interpretation loss.
- **GAIA-N-032** All vocabularies and identifiers are stable URIs; no ID is reused.
- **GAIA-N-033** Provenance chains are complete: every derived value can be traced to the observations it was computed from, with the algorithm version and timestamp.

### 7.5 Federation and Sovereignty

- **GAIA-N-040** Multi-tenant from day one: federation partners operate within their scope (their parcels, their contributions) with strong isolation.
- **GAIA-N-041** Regional data residency: observations on a parcel default to storage in the parcel's jurisdiction; cross-region replication is policy-controlled.
- **GAIA-N-042** Indigenous data sovereignty: where a parcel is under indigenous stewardship, access controls and data flows respect the steward's policy, including possible exclusion of public APIs and external federation.
- **GAIA-N-043** Federation members can mirror their scope locally and operate on it during network partition.

### 7.6 Security

- **GAIA-N-050** All API access is authenticated (OIDC) and authorized (attribute-based, with parcel and codex scope).
- **GAIA-N-051** Service-to-service identity is SPIFFE-based.
- **GAIA-N-052** All write events are cryptographically signed by the writing principal.
- **GAIA-N-053** Sensitive parcel locations (where exposure would risk poaching, encroachment, or harm) are coarsened in public APIs.
- **GAIA-N-054** PII handling follows least-privilege; field operator identities are pseudonymous in non-administrative contexts.

### 7.7 Data Quality

- **GAIA-N-060** Every observation carries a confidence or uncertainty value, or a method specification from which it can be derived.
- **GAIA-N-061** Derived metrics carry their computation lineage.
- **GAIA-N-062** Quality regressions in incoming streams (sensor drift, satellite cloud cover, anomalous reporter rates) are detected and surfaced.

### 7.8 Observability

- **GAIA-N-070** All services emit OpenTelemetry traces, metrics, and logs.
- **GAIA-N-071** Ingest pipelines have end-to-end SLOs and dashboards.
- **GAIA-N-072** Every agent interaction is logged with input, output, retrieval set, and downstream action.

---

## 8. Architecture

### 8.1 Component overview

```
                ┌──────────────────────────────────────────────┐
                │                Gaia API Surface              │
                │ REST · GraphQL · SPARQL · STAC · Events Out  │
                └──────────────────────────────────────────────┘
                          ▲              ▲             ▲
                          │              │             │
        ┌─────────────────┴─┐   ┌────────┴────────┐   ┌┴──────────────────┐
        │   Twin Services    │   │ Codex Services  │   │ Integration Edge │
        │  (spatial, time,   │   │ (KG, revision,  │   │  (A3, OpenFactory│
        │   imagery, plant)  │   │   evidence)     │   │   UMH summaries) │
        └────────────────────┘   └─────────────────┘   └──────────────────┘
                  │                       │                       │
                  ▼                       ▼                       ▼
        ┌────────────────────┐   ┌─────────────────┐    ┌──────────────────┐
        │ PostGIS · Timescale│   │   Neo4j / RDF   │    │ Event bus (Kafka)│
        │ pgvector · STAC    │   │  Versioned blob │    │   Object storage │
        │ GeoParquet/DuckDB  │   │   store         │    │   for archival   │
        └────────────────────┘   └─────────────────┘    └──────────────────┘
                  │                       │
                  └───────────┬───────────┘
                              ▼
                    ┌───────────────────┐
                    │ Identity & Access │
                    │  OIDC · SPIFFE    │
                    │  Policy engine    │
                    └───────────────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │  Durable Workflows│
                    │  (Temporal)       │
                    └───────────────────┘
```

### 8.2 Storage layout

- **PostGIS** — parcels, cohorts, plant-level records, current lifecycle state, derived geometries.
- **TimescaleDB** — time-series observations (sensor readings, growth measurements, derived indices over time).
- **pgvector** — embeddings of satellite tiles, species descriptions, recipe text, observation notes for semantic retrieval.
- **STAC catalog** — imagery metadata across providers; imagery itself in object storage (Parquet/GeoTIFF/COG).
- **GeoParquet on object storage** — analytical and archival store; queried via DuckDB for planetary-scale analysis that PostGIS cannot accommodate.
- **Neo4j (or RDF triple store)** — codex knowledge graph; choice deferred to design phase based on federation requirements.
- **Versioned blob store** — codex content (full text of recipe descriptions, scientific notes, traditional knowledge attestations) with immutable revision history.
- **Object storage** — long-term archival of all observations in open formats; the system of last resort.

### 8.3 Identity and access

OIDC for human and partner identity; SPIFFE for service identity. A policy engine evaluates access decisions against parcel scope, codex scope, sovereignty rules, and persona role. Every decision is logged.

### 8.4 Durable workflows

Temporal (or Restate) hosts long-running workflows: cohort lifecycle, recipe-instance outcome computation cadences, multi-year monitoring obligations, scheduled archival. These are workflows that may run for years; they cannot be cron jobs.

### 8.5 Event bus

Kafka or Redpanda carries events between Gaia and the rest of Robotanica. Event schemas are versioned; consumers declare schema compatibility at subscription time.

---

## 9. APIs

### 9.1 External API surface

- **REST** for CRUD-style access to parcels, cohorts, plants, observations, codex entries, and revisions.
- **GraphQL** for federated reads where consumers compose across twin and codex.
- **STAC** for imagery catalog access.
- **SPARQL** (if RDF is selected) or **Cypher** (if Neo4j) for codex graph traversal.
- **Event subscriptions** on Kafka topics for: `parcel.lifecycle`, `cohort.lifecycle`, `observation.created`, `codex.revision`, `outcome.computed`, `anomaly.detected`.

### 9.2 Specifications

- All synchronous APIs specified in **OpenAPI 3.1**.
- All event APIs specified in **AsyncAPI 2.x**.
- All entity schemas specified in **JSON Schema** with stable `$id` URIs.
- Specifications are the contract; implementations are conformance-tested against them.

### 9.3 SDKs

Python and TypeScript SDKs are first-class. Other languages follow demand. SDKs are generated from specifications, not handwritten.

---

## 10. Integrations

| System | Direction | Interface | Data flowing |
|---|---|---|---|
| A3 | Bidirectional | REST + Events | Parcel rights (in), recipe references (out), contract events (in), outcome attestations (out) |
| OpenFactory | Bidirectional | REST + Events | Recipes and plans (out), operation events (in), biological-batch genealogy (in) |
| UMH | Inbound | Events (Kafka bridge) | Aggregated greenhouse and fleet telemetry; raw firehose stays in UMH |
| ERPNext (via OpenFactory) | Inbound (indirect) | Events | Production batch genealogy linked to cohorts |
| External KGs (GBIF, etc.) | Bidirectional | Federated query, periodic sync | Species records, observation interchange |
| Satellite providers | Inbound | STAC API + bulk download | Imagery |
| Agents (all tiers) | Bidirectional | REST + dedicated retrieval API | Reads for grounding; writes for proposals and observations |

---

## 11. Success Metrics

### 11.1 System health

- Ingest success rate (per source, daily): > 99.9%.
- Observation-to-query latency (P95): < 5 minutes.
- API availability (P95 over rolling 30 days): > 99.9%.

### 11.2 Data completeness

- Parcels under stewardship with current sensor coverage: > 95%.
- Cohorts with up-to-date lifecycle state (within 30 days): > 95%.
- RecipeInstances with computed outcome metrics on schedule: > 90%.

### 11.3 Knowledge quality

- Recipes with linked outcome evidence: > 80% within two years of first instance.
- Codex revision review SLA (median time from proposal to decision): < 30 days.
- Contradiction surfacing rate (newly detected per quarter): tracked, not bounded.

### 11.4 Mission-aligned outcomes

These are reported by Gaia but are the OKRs of Robotanica, not Gaia in isolation:

- Cohorts past year-5 survival threshold (cumulative, by region).
- Standing biomass under stewardship (annual delta).
- Biodiversity index trajectory (per parcel, multi-year).

---

## 12. Phasing

| Phase | Scope | Exit criteria |
|---|---|---|
| 0 — Foundations | Identity model, URI scheme, schema v0, single-region deployment | First parcel ingested; first codex entry authored; first observation recorded end-to-end |
| 1 — Pilot | Twin operational for pilot sites; codex with seed taxonomy and seed recipes; A3 and OpenFactory integration | All pilot-site operations grounded in Gaia; first RecipeInstance with computed outcomes |
| 2 — Federation | Multi-tenant, multi-region; external recipe contributors onboarded; public read API | First non-Robotanica recipe contributor merged; first sovereign-tenant deployment |
| 3 — Agents | Agent retrieval and writeback; outcome-evidence-driven recipe revision proposals | Tier 1 agents in production grounded entirely in Gaia; first agent-proposed revision merged |
| 4 — Scale | Planetary ingest cadence; full archival pipeline; cross-region replication | NFRs at section 7.1 sustained for 90 days |

Phase boundaries are exit criteria, not dates. The OKR's true horizon is decades; phases must not be compressed into quarters at the cost of the durability requirements.

---

## 13. Risks and Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Schema and vocabulary drift over decades | Loss of interpretability of old data | Stable URIs, versioned schemas, point-in-time query support, archival in open formats |
| Storage cost at planetary scale | Operational unsustainability | Tiered storage; cold archival in object storage; aggressive compression for time-series; selective retention policies for raw imagery |
| Codex capture by a single methodology or interest group | Loss of epistemic diversity | Open contribution protocol; Science Council multi-disciplinary composition; explicit support for traditional and indigenous knowledge as first-class |
| Sensitive location exposure | Harm to ecosystems and communities | Coarsening in public APIs; sovereignty-aware access controls; default-private for indigenous parcels |
| Vendor lock-in on storage or graph layer | Migration cost in 10+ years | All persistent state replicated in open formats; graph layer choice deferred and reversible |
| Agent feedback loops degrading data quality | Drift toward agent-preferred recipes | Agent writes always require human review for codex; agent observation writes carry distinct provenance and are excluded from training without explicit promotion |
| Multi-region partition during disaster | Loss of access during the event | Federation members operate locally during partition; reconciliation on rejoin via append-only logs |

---

## 14. Open Questions

- **Graph layer choice.** Neo4j is operationally simpler; an RDF triple store is more interoperable with external scientific KGs. The decision is deferred until federation requirements are clearer.
- **Plant-level vs. cohort-level granularity.** Tracking every individual tree at a trillion-tree scale is operationally implausible; a sampling and statistical-extrapolation strategy is needed but not yet specified.
- **Public API granularity.** How much of the twin should be public-readable? The transparency case is strong; the sensitive-location and indigenous-sovereignty cases push the other way. A per-parcel policy regime is likely.
- **Recipe contestation thresholds.** What number of reviewers, what evidence thresholds, what cool-down periods govern recipe revision? Policy must be codified before the codex opens to federation.
- **Long-term archival strategy.** Every component will be replaced over fifty years. The archival path (open formats, object storage, format-version migration) needs explicit design and exercise.
- **Holobiont data scope.** Mycorrhizal, pollinator, and microbial data dramatically expand storage and integration requirements. Phasing of holobiont coverage is not yet decided.

---

## Appendix A — Glossary (Gaia-specific)

- **Codex** — the interpretation layer of Gaia; a versioned knowledge graph of species, ecosystems, and recipes.
- **Cohort** — a group of plants of common provenance and planting event on a common parcel.
- **Episode** — a bounded period of conditions or interventions.
- **Evidence** — a link from a codex entry to supporting twin observations or external sources.
- **Holobiont** — a host organism considered together with its microbiota and symbionts.
- **Observation** — an immutable record of something witnessed or measured, with full provenance.
- **Outcome** — a derived assessment over a parcel/cohort/recipe instance.
- **Parcel** — a spatial polygon under Robotanica stewardship.
- **Recipe** — a versioned intervention template in the codex.
- **RecipeInstance** — the application of a recipe to a parcel/cohort; the bridge between codex and twin.
- **Revision** — an immutable record of a change to a codex entry.
- **STAC** — SpatioTemporal Asset Catalog.
- **Twin** — the observation layer of Gaia; the spatial, temporal, and remote-sensing record.

---

## Appendix B — Standards and References

- **OGC** standards: Simple Features, GeoPackage, STAC.
- **W3C** standards: RDF 1.1, SPARQL 1.1, JSON-LD 1.1.
- **OpenAPI** 3.1, **AsyncAPI** 2.x.
- **OIDC**, **SPIFFE**.
- **GBIF**, **Catalogue of Life**, **World Flora Online** for species authority.
- **ISO 19115** for geospatial metadata.
- **Darwin Core** for biodiversity records.
- **CARE Principles** (Collective benefit, Authority to control, Responsibility, Ethics) for indigenous data governance.
- **FAIR Principles** (Findable, Accessible, Interoperable, Reusable) for scientific data.

---

*This is v0.1 of the Gaia PRD. Sections 5 (domain model), 6 (functional requirements), and 7 (non-functional requirements) are the most stable; sections 11–13 (metrics, phasing, risks) will evolve substantially as the platform meets reality.*
