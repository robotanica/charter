# Technical Architecture Plan

## Engineering Specification (v0)

**Document type:** Technical engineering specification
**Status:** Draft for engineering review
**Companion documents:** Robotanica Charter, Gaia PRD, A3 PRD, OpenFactory PRD, Protocol Specifications, Data Lifecycle Plan, AI Ethical Review Framework

---

## 1. Purpose and Scope

This document is the engineering layer beneath the PRDs. The PRDs specified what each platform does and what requirements it satisfies. This document specifies how the platforms are built: service decomposition, data models, APIs, event schemas, deployment topology, security boundaries, and cross-cutting infrastructure.

The document covers:

- **Cross-cutting infrastructure** — identity, event bus, observability, deployment, secrets management, the schema registry. These are shared across all three platforms.
- **Gaia architecture** — services, storage, APIs, and data flows for the epistemic platform.
- **A3 architecture** — services, storage, APIs, and event ledger for the governance platform.
- **OpenFactory architecture** — services, storage, APIs, and the bridge layer for manufacturing and fleet.
- **Integration patterns** — how the platforms talk to each other and to the federation.
- **Operational architecture** — multi-region deployment, disaster recovery, runbooks.

This is v0. Specific implementation details will evolve. The patterns and structure are intended to be stable for at least the first phase of the project; major architectural shifts go through governance per the Protocol Specifications §14.

---

## 2. Architectural Principles

These principles guide all architectural decisions and resolve disputes between alternative approaches.

### 2.1 Boring Technology Where Possible

**Choose well-understood, widely-deployed, openly-developed technologies over novel ones.** PostgreSQL over a new database. Kafka over a new event bus. Kubernetes over a new orchestrator. Multi-decade durability is incompatible with bleeding-edge tooling that may not exist in five years.

### 2.2 Open Source Default

**All chosen technologies are open-source where viable.** Proprietary technologies are used only when no open alternative meets requirements, with documented exit paths.

### 2.3 Stateless Services, Stateful Stores

**Services are stateless and replaceable. State lives in databases, object storage, and event logs.** This decouples deployment cadence from data lifecycle and supports the Data Lifecycle Plan's preservation discipline.

### 2.4 Event-Sourced Where History Matters

**Lease lifecycles, governance decisions, observations, and other historically-meaningful entities use event sourcing.** Current state is a projection of the event log; the log is the source of truth.

### 2.5 Schema First

**APIs and events are specified before code is written.** OpenAPI 3.1 for synchronous APIs; AsyncAPI 2.x for events; JSON Schema for data structures. Specifications are stored in a schema registry and versioned.

### 2.6 Multi-Region by Default

**Every platform supports multi-region deployment from day one.** Even if initial deployment is single-region, the architecture does not assume single-region operation.

### 2.7 Conformance Testable

**Every platform has a published conformance test suite.** Alternative implementations of any platform must pass conformance tests to participate in the federation per Protocol Specifications §13.

### 2.8 Edge-Tolerant

**Field operations operate during connectivity loss.** OpenFactory has explicit edge architecture; Gaia and A3 design for graceful degradation when regions partition.

### 2.9 Cryptographic Provenance

**Events of consequence are cryptographically signed.** Signatures are part of the data, verifiable independently of runtime per Protocol §3.1.

### 2.10 Operational Reversibility

**Deployments and migrations are reversible.** Every change supports rollback. Every migration includes a documented rollback procedure.

---

## 3. Cross-Cutting Infrastructure

These components are shared across all three platforms and federation members.

### 3.1 Identity

**Human identity:** OpenID Connect (OIDC) via a federation-managed identity provider. Initial implementation: Keycloak or Authentik (both open-source). Federation members may federate their own OIDC providers.

**Service identity:** SPIFFE / SPIRE. Services receive SPIFFE Verifiable Identity Documents (SVIDs) automatically through workload attestation. SVIDs are short-lived (1 hour default), automatically rotated.

**Party signing keys:** Ed25519 by default; algorithm-agile per Data Lifecycle §7.3. Keys stored in HashiCorp Vault or equivalent KMS. Hardware-backed keys for high-stakes signing (Federation governance, Council).

**URI resolution:** A federation-wide URI resolver service translates `gaia://`, `a3://`, `of://`, `robotanica://` URIs to current addresses. Indirect addressing supports infrastructure migration without breaking links.

### 3.2 Event Bus

**Kafka or Redpanda** as the event spine. Single logical bus with topic-level partitioning. Multi-region via MirrorMaker 2 or equivalent.

**Topic naming convention:** `<source-platform>.<entity-type>.<event-type>` (e.g., `gaia.observation.created`, `a3.lease.signed`, `of.cohort.transitioned`).

**Schema enforcement:** Every topic has registered AsyncAPI schemas in the schema registry. Producers write through a serialization layer that validates against current schema. Consumers declare schema compatibility on subscription.

**Retention:** Per topic, defined by data classification (Data Lifecycle §4). Class I events retained indefinitely; Class III events retained 25 years; Class IV events retained per operational need.

**Delivery semantics:** At-least-once delivery; consumers idempotent. Exactly-once is not pursued at the bus layer.

**Cross-region replication:** Events flow across regions with conflict-free merge. Sovereign-partition topics replicate only within sovereign boundaries.

### 3.3 Schema Registry

**Confluent Schema Registry or Apicurio** as the canonical registry for AsyncAPI, OpenAPI, and JSON Schema definitions. Every schema has a stable URI and a version. Schema evolution rules enforced automatically (forward and backward compatibility per change type).

**Schema repository:** Schemas are version-controlled in a Git repository alongside the registry. Pull requests for schema changes go through review.

### 3.4 Observability

**Tracing:** OpenTelemetry traces across all services. W3C Trace Context propagation. Trace storage in Tempo or Jaeger.

**Metrics:** Prometheus-format metrics. Storage in Prometheus, Mimir, or Cortex with long retention.

**Logs:** Structured JSON logs. Aggregation in Loki or equivalent. Personal data and sensitive-location data stripped at the source.

**Dashboards:** Grafana, with dashboards versioned in Git.

**Alerting:** Prometheus Alertmanager. Routing per service ownership. SLOs defined per service.

### 3.5 Secrets Management

**HashiCorp Vault** as secrets backend. Dynamic credentials for databases (Vault generates short-lived database users automatically). Static secrets only when dynamic is impossible.

**SPIFFE-based access:** Services authenticate to Vault via SPIFFE SVIDs.

**Audit:** All secret access logged. Audit logs preserved per Data Lifecycle Class II.

### 3.6 Deployment

**Kubernetes** as the orchestration layer. Multi-cluster across regions via Cluster API (CAPI) or vendor-specific equivalents.

**GitOps:** Argo CD or Flux for cluster state. All cluster state defined in Git; no manual `kubectl apply`. Pull requests for changes.

**Container registry:** Open-source registry (Harbor) per region with cross-region replication. Container images signed via Sigstore (cosign).

**Service mesh:** Istio or Linkerd. Mutual TLS between services via SPIFFE SVIDs. Traffic policies in Git.

**Networking:** Cilium for CNI. Network policies as code. Egress controls for compliance.

### 3.7 Data Storage

**Operational PostgreSQL:** Self-hosted (CloudNative-PG operator) per region. Logical replication for cross-region reads. Point-in-time recovery via WAL archival to object storage.

**TimescaleDB extension** for time-series.

**PostGIS extension** for spatial.

**pgvector extension** for embeddings.

**Object storage:** S3-compatible (Ceph, MinIO, or cloud-native S3). Lifecycle policies migrate cold data to cheaper tiers automatically.

**Knowledge graph:** Neo4j cluster (Community Edition initially; Enterprise with appropriate license if scale requires) or Apache Jena for RDF.

**Search:** OpenSearch cluster.

### 3.8 Workflows

**Temporal** as the durable workflow engine. Workflows are first-class code (Go or Python preferred for new workflows). Multi-region workflow clusters.

### 3.9 API Gateway

**Envoy** at the edge with Open Policy Agent (OPA) for authorization. Routing per OpenAPI spec.

**Rate limiting** at the gateway, configurable per consumer category.

### 3.10 Frontend

**Next.js** for web UIs (operator dashboards, public portal, admin consoles). Component library: Radix UI primitives + Tailwind CSS. Map components: MapLibre GL JS for Gaia spatial visualization.

**Mobile:** React Native for stewards' field tools. Offline-first design.

---

## 4. Gaia Architecture

Gaia is the epistemic platform: observations (the twin) and interpretations (the codex), tightly coupled through identity and feedback loops.

### 4.1 Service Decomposition

**Twin services:**

- **Parcel Service** — parcel CRUD, lifecycle state, ownership references to A3.
- **Cohort Service** — cohort lifecycle, plant-level records, lifecycle state aggregation.
- **Observation Service** — observation ingest, validation, signing, persistence.
- **Imagery Service** — STAC-based catalog, satellite imagery ingest, derived index computation.
- **Sensor Service** — environmental sensor data ingest, time-series storage.
- **Predictive Service** — site-suitability models, mortality risk, intervention timing.

**Codex services:**

- **Species Service** — species ontology, links to external authorities (GBIF, Catalogue of Life).
- **Ecosystem Service** — ecosystem types, structure, succession.
- **Recipe Service** — recipe entries, versioning, evidence linking.
- **Revision Service** — proposal-review-merge workflow for codex entries.
- **Evidence Service** — links between codex entries and twin observations.

**Bridge services:**

- **RecipeInstance Service** — the bridge entity connecting codex recipes to twin parcels and cohorts.
- **Outcome Service** — periodic outcome computation per RecipeInstance, aggregation across instances.

**Cross-cutting:**

- **URI Resolver** — translates Gaia URIs to current addresses, supports versioned references.
- **Provenance Service** — manages signing keys for Gaia services, signs events.
- **Federation Sync** — exposes federated query interface; coordinates with external scientific KGs.

### 4.2 Data Model (Concrete)

**Parcel** (PostGIS):

```
parcels (
    uri text primary key,           -- gaia://parcel/<region>/<id>
    geometry geography(MultiPolygon, 4326),
    region text not null,
    sovereignty_declaration_uri text,
    a3_lease_uri text,              -- references a3://lease/...
    lifecycle_state text not null,  -- enum: proposed, committed, active, ...
    created_at timestamptz,
    updated_at timestamptz,
    sovereign_partition text not null  -- partition key for sovereignty
)
```

**Cohort:**

```
cohorts (
    uri text primary key,            -- gaia://cohort/<region>/<id>
    parcel_uri text references parcels(uri),
    recipe_instance_uri text,
    species_mix jsonb,               -- {species_uri: proportion}
    establishment_date date,
    lifecycle_state text,            -- planned, planted, established, juvenile, mature, deceased
    parent_population_count integer,
    sovereign_partition text not null
)
```

**Observation** (TimescaleDB hypertable):

```
observations (
    uri text,
    occurred_at timestamptz not null,
    subject_uri text not null,       -- parcel, cohort, or plant URI
    type text not null,              -- enum: sensor_reading, satellite_index, field_inspection, ...
    method text,
    payload jsonb,
    confidence numeric,
    source_uri text,                 -- principal that recorded
    signature bytea,
    sovereign_partition text not null
)
-- partitioned by occurred_at
```

**Recipe** (PostgreSQL + content-addressable storage):

```
recipes (
    uri text not null,                -- gaia://recipe/<region>/<id>
    version text not null,            -- semver
    methodology text,                 -- miyawaki, savory, fmnr, ...
    bioregion text,
    target_ecosystem_uri text,
    species_mix jsonb,
    density_specification jsonb,
    succession_plan jsonb,
    monitoring_protocol_uri text,
    expected_outcomes jsonb,
    content_hash text,                -- hash of canonical serialization
    primary key (uri, version)
)
```

**Knowledge graph** (Neo4j or RDF triple store):

```
Recipe -[INHERITS_FROM]-> Methodology
Recipe -[TARGETS]-> Ecosystem
Recipe -[INCLUDES_SPECIES]-> Species
Recipe -[CITES]-> Evidence
Species -[PART_OF]-> Ecosystem
Species -[ASSOCIATES_WITH]-> Species  (mycorrhizal, pollinator, companion)
Evidence -[REFERENCES]-> Observation
Recipe -[REVISED_BY]-> Revision
Revision -[AUTHORED_BY]-> Party
```

### 4.3 API Surfaces

**Public REST APIs (selected):**

```
GET  /parcels/{uri}                    -- read parcel state
GET  /parcels/{uri}/observations       -- observations for parcel
POST /observations                      -- submit observation (auth required)
GET  /cohorts/{uri}                    -- read cohort
GET  /cohorts/{uri}/lifecycle          -- lifecycle history
GET  /recipes                          -- list recipes
GET  /recipes/{uri}@{version}          -- specific recipe version
POST /recipe-revisions                 -- propose revision
GET  /recipe-instances/{uri}/outcomes  -- outcomes for instance
```

**GraphQL:** Federated read across twin and codex. Single query can return a parcel, its bound recipes, evidence supporting the recipe, and outcome history.

**SPARQL endpoint:** For codex graph traversal where RDF is implemented.

**STAC API:** For imagery catalog access.

**Event topics published:**
- `gaia.parcel.lifecycle`
- `gaia.cohort.lifecycle`
- `gaia.observation.created`
- `gaia.recipe.revision`
- `gaia.outcome.computed`
- `gaia.anomaly.detected`

### 4.4 Storage Layout

| Storage | Purpose | Class |
|---|---|---|
| PostgreSQL (PostGIS, TimescaleDB) | Operational state, observations, time-series | Hot/Warm |
| Object storage (Parquet/COG) | Imagery, large derived datasets | Warm |
| Neo4j or RDF store | Codex knowledge graph | Hot |
| pgvector | Embeddings for semantic search | Hot |
| Object storage (signed event archives) | Event log archive | Cold |
| Glacial archival | Long-term Class I preservation | Glacial |

### 4.5 Data Flows

**Observation ingest:**

```
Source (sensor, robot, human) 
  → API gateway (auth, rate limit)
  → Observation Service (validate, sign, persist)
  → PostgreSQL/TimescaleDB
  → Event bus: gaia.observation.created
  → Outcome Service (consume), Anomaly Service (consume)
```

**Imagery ingest:**

```
Satellite provider (Sentinel, Landsat, Planet) 
  → Imagery Service (STAC catalog update)
  → Object storage (COG)
  → Derived Index Service (NDVI, biomass) 
  → PostgreSQL (per-parcel time series)
  → Event bus: gaia.imagery.indexed
```

**Recipe revision:**

```
Author (Scientific Contributor)
  → Revision Service (proposal)
  → Review queue (Council reviewers, peer reviewers)
  → Approval (signed)
  → Recipe Service (new version)
  → Event bus: gaia.recipe.revision
  → A3 (notify affected RecipeInstances)
```

### 4.6 Edge Cases

**Plant-level vs cohort-level granularity** (PRD §14 open question): Plant-level tracking is supported but optional per cohort. Where plant-level is impractical (large cohorts, dense plantings), cohort-level statistical sampling is used. The decision is a recipe parameter.

**Climate-shifted bioregions:** Each bioregion entity has a `climate_analog_bioregion` field referencing the bioregion whose current climate matches projected future climate. Climate-aware provenance decisions (Genetic Strategy §6) reference these.

---

## 5. A3 Architecture

A3 is the governance and coordination platform. Its discipline is the append-only signed event ledger; everything else flows from there.

### 5.1 Service Decomposition

**Lease services:**

- **Lease Service** — lease lifecycle, state machine, amendment workflow.
- **Consent Service** — FPIC and other consent records, signing workflow.
- **Lease Document Service** — document storage, signature verification, jurisdictional variants.

**Marketplace services:**

- **Service Catalog Service** — Operator service offerings.
- **Match Service** — service-request to operator matching.
- **ServiceContract Service** — contract lifecycle, dispatch, completion.

**Credit services:**

- **Credit Issuance Service** — verified-outcome-driven issuance.
- **Credit Registry Service** — credit lifecycle, transfer, retirement.
- **Reconciliation Service** — site-failure-driven credit voiding or making whole.
- **Reserve Service** — reconciliation reserve management.

**Governance services:**

- **GovernanceDecision Service** — recording and querying decisions.
- **Membership Service** — federation membership lifecycle.
- **Veto Service** — Council veto authority interface.

**Dispute services:**

- **DisputeCase Service** — dispute filing, routing, state.
- **Mediation Service** — mediation workflow integration.

**Cross-cutting:**

- **Event Ledger Service** — append-only signed event ledger; the source of truth.
- **Public Record Service** — exposes the public-record subset of the ledger.
- **URI Resolver** — A3-specific URI resolution.

### 5.2 The Event Ledger

The ledger is the architectural heart of A3. Every state change in A3 is an event in the ledger.

**Event format** (matches Protocol §5.1):

```json
{
  "id": "a3://event/<region>/<uuid>",
  "type": "a3.lease.signed",
  "occurred_at": "2026-04-15T14:32:00Z",
  "ingested_at": "2026-04-15T14:32:01Z",
  "principal": "robotanica://party/global/<id>",
  "subject": "a3://lease/<region>/<id>",
  "schema_version": "1.0",
  "payload": { ... type-specific ... },
  "signature": "<base64>",
  "prior_event_hash": "<sha256>",
  "sovereign_partition": "<jurisdiction>"
}
```

**Storage:**

```
events (
    id text primary key,
    event_type text not null,
    occurred_at timestamptz not null,
    ingested_at timestamptz not null,
    principal_uri text not null,
    subject_uri text not null,
    schema_version text not null,
    payload jsonb not null,
    signature bytea not null,
    prior_event_hash text,
    sovereign_partition text not null,
    -- indexed by (subject_uri, occurred_at) and (sovereign_partition, occurred_at)
)
-- partitioned by sovereign_partition + month
```

**Hashing chain:** Each event's content (canonical JSON serialization) is hashed (SHA-256). The next event affecting the same subject references the prior event's hash, creating a tamper-evident chain per subject.

**Verification:** A reader with the events, the signing public keys, and the canonicalization spec can verify integrity end-to-end without trusting A3's runtime.

**Materialized projections:** Current state of leases, credits, members is projected from the event log into operational tables. Projections are rebuildable from the log.

### 5.3 Data Model (Concrete)

**Lease** (projected from events):

```
leases (
    uri text primary key,
    parcel_uri text references gaia parcels,
    landowner_party_uri text not null,
    operator_party_uri text not null,
    federation_party_uri text not null,
    community_party_uri text,         -- nullable, indigenous/community party
    bound_recipe_uri text,
    bound_recipe_version text,
    jurisdictional_variant_uri text,
    term_start date,
    term_end date,
    state text not null,              -- state machine state
    sovereign_partition text not null,
    last_event_id text references events(id)
)
```

**Credit:**

```
credits (
    uri text primary key,
    type text not null,               -- carbon, biodiversity, ecosystem_service
    vintage_year integer,
    parcel_uri text,
    lease_uri text,
    recipe_instance_uri text,
    verification_report_uris text[],
    issuer_uri text,
    current_holder_uri text,
    state text,                       -- pending, issued, transferred, retired, reconciled
    issuance_event_id text,
    last_event_id text references events(id)
)
```

**Party:**

```
parties (
    uri text primary key,
    type text not null,               -- landowner, operator, community, funder, ...
    display_name text,
    signing_keys jsonb,               -- list of {key_id, algorithm, public_key, valid_from, valid_until}
    membership_status text,
    region text,
    contact jsonb,                    -- structured contact info, access-controlled
    sovereign_partition text
)
```

### 5.4 API Surfaces

```
GET  /leases/{uri}                    -- current state
GET  /leases/{uri}/events              -- event history
POST /leases/{uri}/amendments          -- propose amendment (signed)
POST /leases/{uri}/disputes            -- file dispute
GET  /credits/{uri}                    -- credit state
POST /credits/{uri}/transfer           -- transfer (signed by both parties)
POST /credits/{uri}/retire             -- retire credit
GET  /governance-decisions             -- search decisions
GET  /public-record                    -- public-record stream
GET  /federation/members               -- member directory
```

**Event topics:**
- `a3.lease.lifecycle`
- `a3.service-contract.lifecycle`
- `a3.credit.lifecycle`
- `a3.governance.decision`
- `a3.dispute.lifecycle`
- `a3.federation.membership`

### 5.5 The Lease State Machine

States: `proposed, consent-pending, signed, active, under-amendment, breach-notice, cure-period, under-mediation, under-arbitration, succession-pending, terminated, closed-out`.

Transitions are events. Each event records: the actor, the cause, the new state, and the prior event hash. State machines are enforced at the service layer; transitions outside the defined paths are rejected.

### 5.6 Sovereign Partitions

Every entity in A3 is associated with a `sovereign_partition`: the jurisdiction or community whose sovereignty governs the data. Storage, replication, and access are scoped by partition.

**Partitioning implementation:**

- Database partitioning by `sovereign_partition` field.
- Object storage path prefixed by partition.
- Event topics either partition-scoped or globally replicated based on policy.
- API queries enforce partition scope via the policy engine.

**Cross-partition coordination:** Federation-wide governance events span partitions. They are stored in a federation-global partition; access controls enforce the appropriate read scope.

### 5.7 Cryptographic Discipline

**Per-party signing keys:** Stored in Vault per party. Hardware-backed keys for governance bodies (Council, Stewardship Office, Federation governance).

**Event signing:** Every event is signed by its principal (the party authoring it) at write time. Service-authored events are signed by service identity (SPIFFE).

**Manifest signing:** Periodic manifests (daily, weekly, monthly snapshots of the ledger) are signed by Federation governance keys, providing a cumulative attestation.

**Key rotation:** Documented per Protocol Specifications §4.4.

---

## 6. OpenFactory Architecture

OpenFactory bridges three production layers: ERPNext + Frappe MES app for system of record, UMH for shop-floor reality, and Open-RMF + ROS 2 for fleet coordination.

### 6.1 Service Decomposition

**Production layer (Frappe-based):**

- ERPNext stock — work orders, BOMs, items, costing.
- **Robotanica MES app** — custom doctypes:
  - `ProductionRun`
  - `BiologicalBatch`
  - `EnvironmentEpisode`
  - `RobotAssemblyRecord`
  - `Component`
  - `GeneticLineage`
  - `QualityCheck`

**Fleet layer:**

- **Fleet Manager** — robot registry, capability profiles, current state.
- **Open-RMF integration** — multi-vendor fleet coordination.
- **Mission Planner** — A3 service contracts → Mission decomposition.
- **Dispatch Service** — Mission → Operation routing to robots/humans.
- **Edge Coordination Service** — local-cluster coordination during connectivity loss.

**Telemetry layer:**

- **UMH stack** — managed externally (UMH is a project of its own); integrated via UNS.
- **Bridge Service** — UMH UNS ↔ Frappe MES translation (per OpenFactory PRD §6.10).
- **TimescaleDB** — operational telemetry storage.

**Edge layer:**

- **ROS 2 nodes** on robots — control, perception.
- **ONNX Runtime** at the edge — perception inference.
- **Local UMH agent** — buffers events offline.
- **Edge integrity service** — verifies firmware, signs events.

**Cross-cutting:**

- **Provenance Service** — signing of operation events, batch records.
- **Event publication** — to federation event bus.

### 6.2 The Bridge Service

The bridge between UMH UNS and ERPNext/Frappe is small but central.

**Functionality:**

- Subscribes to UMH UNS topics (`umh.v1.<site>.<area>.<line>.<machine>...`).
- Translates relevant events to Frappe doctype updates via Frappe REST API.
- Aggregates high-frequency events (debouncing, batching) before writing to Frappe.
- Publishes ERPNext state changes back to UNS as events.
- Propagates correlation IDs (work_order_id, batch_id) through MQTT topic hierarchy.

**Implementation:** Python service. Subscribes via paho-mqtt or kafka client (depending on UMH topology). Writes to Frappe via the standard `/api/method/frappe.client.set_value` and similar endpoints. Stateless — restarts replay from UMH retention.

**Throughput design:** Aggregates, doesn't pass through. UMH retains the firehose; Frappe sees state-relevant events at sustainable cadence.

### 6.3 Fleet Architecture

**Open-RMF** as the heterogeneous fleet coordinator. RMF traffic schedules across vendors. Vendor-specific adapters bridge robots without native ROS 2 to RMF.

**Mission decomposition:**

```
A3 Service Contract
  → Mission (e.g., "plant cohort X on parcel Y")
  → Operations (e.g., "place tree at GPS coord A; install inoculant at B; ...")
  → Dispatch to capable robots (RMF assigns)
  → Robot executes
  → OperationEvent published
  → Gaia receives observation; ERPNext receives genealogy update
```

**Edge coordination:** When wide-area connectivity is lost, robots in a local cluster coordinate via local-network ROS 2 or a lightweight edge-coordination service. Bounded autonomy — no novel decisions outside dispatched mission scope.

### 6.4 Data Model (Concrete)

Frappe doctypes (selected):

**ProductionRun:**

```
ProductionRun
  - work_order: link to ERPNext Work Order
  - facility: link to Facility doctype
  - production_line: link to ProductionLine
  - start_datetime, end_datetime
  - operators: list of users
  - environment_episode: link to EnvironmentEpisode
  - quality_outcomes: list of QualityCheck
  - genealogy: child table linking to consumed Items and produced Items
```

**BiologicalBatch:**

```
BiologicalBatch
  - batch_id: stable URI (of://biological-batch/...)
  - species_uri: link to Gaia species
  - parent_batch_uri: nullable, parent BiologicalBatch
  - genetic_lineage: link to GeneticLineage
  - production_run: link to ProductionRun
  - environment_history: list of EnvironmentEpisode
  - quality_state: enum
  - cohort_uri: nullable, link to Gaia cohort once deployed
```

**Robot:**

```
Robot
  - uri: stable
  - assembly_record: link to RobotAssemblyRecord
  - current_firmware_version
  - current_software_version
  - capabilities: list (planting, monitoring, transport, ...)
  - current_state: enum (commissioned, deployed, in_operation, in_maintenance, retired)
  - current_location
  - operator_party: link to Operator
  - fleet: link to Fleet
```

### 6.5 API Surfaces

OpenFactory exposes:

- **Frappe REST API** — for ERPNext + MES doctype access.
- **Custom REST endpoints** — for fleet operations, mission management.
- **ROS 2 interfaces** — for robot integration.
- **UMH UNS** — for telemetry and shop-floor reality.
- **Open-RMF interfaces** — for multi-vendor fleet integration.

**Event topics:**

- `of.production-run.lifecycle`
- `of.biological-batch.lifecycle`
- `of.robot.lifecycle`
- `of.mission.lifecycle`
- `of.operation.event`
- `of.maintenance.event`

### 6.6 Cohort Transition

When a BiologicalBatch leaves OpenFactory and is deployed to the field as plants, it becomes a Cohort in Gaia. The transition:

```
1. OpenFactory Mission dispatches deployment Operation.
2. Operation events emitted as plants are placed (one per plant or per group).
3. BiologicalBatch transitions to "deployed" state.
4. Cohort is created in Gaia with reference to BiologicalBatch.
5. Genealogy preserved: Cohort → BiologicalBatch → parent batches → seed source.
6. Future observations on the Cohort link back to the original genetic lineage.
```

This is the structural answer to the genealogy problem: full traceability across two platforms via cross-system event chaining and shared URI references.

---

## 7. Integration Patterns

### 7.1 Cross-Platform Events

Platforms communicate primarily via the event bus. Synchronous APIs are used for immediate-need queries; events are used for state propagation.

**Standard pattern:**

```
Platform A makes a state change.
  → Platform A persists state, signs event, publishes to its topic.
  → Platform B subscribes to the topic.
  → Platform B updates its derived state and continues.
```

**Examples:**

- A3 issues a credit → A3 publishes `a3.credit.lifecycle` → Gaia updates parcel-credit linkage; reporting subscribers update dashboards.
- Gaia computes an outcome → Gaia publishes `gaia.outcome.computed` → A3 updates RecipeInstance outcome state; potentially triggers credit milestone.
- OpenFactory completes a Mission → OpenFactory publishes `of.mission.lifecycle` → A3 updates ServiceContract; Gaia receives operation observations.

### 7.2 Synchronous Cross-Platform Queries

Where immediate consistency is required, services call each other directly via authenticated REST.

**Examples:**

- A3 lease formation needs current parcel state → A3 calls Gaia parcel API.
- OpenFactory mission dispatch needs current recipe → OpenFactory calls Gaia recipe API.
- Gaia recipe revision needs to notify affected leases → Gaia queries A3 for lease-recipe bindings.

**Caching:** Cross-platform queries cache aggressively (recipe content, parcel boundaries) with cache invalidation via events.

### 7.3 Federation Member Integration

Federation members operate their own platform instances or interact with Robotanica's instances per Protocol Specifications §13 conformance levels.

**Read-conformant members:**
- Authenticate via federation OIDC.
- Read public APIs.
- Subscribe to event topics within their scope.

**Write-conformant members:**
- Above, plus authenticated write to scoped APIs.
- Event publication with their party signing keys.

**Platform-conformant members:**
- Operate their own platform instance.
- Federate via API gateway and event-bus replication.
- Pass conformance test suite.

### 7.4 External System Integration

**Government registries:** Per-jurisdiction adapters; not in the core platform. Built as separate integration services.

**Payment rails:** External payment providers integrated via wrapper services. A3 records obligations and confirmations; funds flow externally.

**External credit registries (Verra, Gold Standard, Plan Vivo):** Bidirectional sync via per-registry adapters. A3 remains source of truth.

**Scientific databases (GBIF, iNaturalist):** Periodic sync into Gaia codex. Federated query for live cross-references.

---

## 8. Operational Architecture

### 8.1 Multi-Region Deployment

**Regions** correspond to sovereign partitions. Each region runs:

- Kubernetes cluster (or fleet of clusters)
- PostgreSQL primary + replicas
- Object storage (regional)
- Event bus (regional + cross-region replication)
- Kafka MirrorMaker for federation-global topics

**Cross-region traffic** flows through the federation backbone (private VPN or cloud interconnect). Traffic is encrypted (mTLS at minimum); sensitive data flows are additionally encrypted at the application layer.

### 8.2 Disaster Recovery

**Recovery Point Objective (RPO):** < 5 minutes for committed transactional data.

**Recovery Time Objective (RTO):** < 1 hour for primary operational services; < 4 hours for full restoration.

**Backup strategy:**

- WAL archival to object storage (PostgreSQL).
- Daily snapshots of PostgreSQL, retained per Data Lifecycle Plan classes.
- Cross-region object storage replication.
- Quarterly DR drills exercising full restoration.

### 8.3 Capacity Planning

**Growth assumptions** (rough order):

| Year | Parcels | Cohorts | Observations/year | Federation members |
|---|---|---|---|---|
| 1 | 10² | 10³ | 10⁵ | 10² |
| 3 | 10⁴ | 10⁵ | 10⁷ | 10³ |
| 5 | 10⁵ | 10⁶ | 10⁹ | 10⁴ |
| 10 | 10⁶ | 10⁸ | 10¹¹ | 10⁵ |

Architecture must accommodate Year 10 numbers without re-architecting; specific implementations may need optimization at intermediate scales.

### 8.4 SRE Discipline

**Service ownership:** Every service has a named owner (team or individual). Ownership responsibilities documented.

**SLO definitions:** Per service, in machine-readable format (Sloth or equivalent).

**Runbooks:** In Git, alongside service code. Auto-linked from alerts.

**On-call rotation:** Federation-wide SRE function for cross-cutting infrastructure; per-platform SRE for platform-specific services.

**Incident response:** Documented severity levels, escalation paths, and post-incident review process.

---

## 9. Security Architecture

### 9.1 Defense in Depth

Multiple layers protect against compromise:

1. **Network:** Private networking, network policies, egress controls.
2. **Identity:** OIDC and SPIFFE; no shared credentials.
3. **Authorization:** OPA policies at API gateway and service mesh.
4. **Data:** Encryption at rest (KMS-backed); encryption in transit (TLS).
5. **Audit:** Append-only logs of all sensitive actions.
6. **Cryptographic provenance:** Signed events; verifiable independently.

### 9.2 Threat-Specific Defenses

Mapped to Threat Model categories (Threat Model §5):

- **Insider tampering** — append-only event log; key separation; service mesh isolation.
- **Credential compromise** — short-lived credentials (SPIFFE 1-hour SVIDs); MFA for human access; HSM-backed signing keys for high-stakes parties.
- **Supply chain compromise** — signed container images; SBOMs maintained; reproducible builds where possible.
- **Cryptographic decay** — algorithm-agile signing; periodic re-signing; planned post-quantum migration.

### 9.3 Sensitive Data Handling

- **PII:** Stored only where necessary; encrypted at rest with separate keys; access logged.
- **Sensitive locations:** Coarsened in public APIs; access controls enforce sovereign-partition rules.
- **Indigenous data sovereignty:** Sovereign-partition model enforces at storage and API layers; not policy overlay.

### 9.4 Compromise Response

If compromise is detected:

1. Affected services isolated (service mesh policy).
2. Compromised credentials revoked.
3. Event log review for tampering (signature verification across the chain).
4. External audit if substantial.
5. Disclosure per Public Communication Doctrine §8.

---

## 10. Phasing and Dependencies

### 10.1 Architecture Phasing

**Phase 0 — Foundations**

- Identity infrastructure (OIDC, SPIFFE, Vault).
- Single-region Kubernetes cluster.
- Event bus (single-region).
- Schema registry.
- Observability stack.
- PostgreSQL with PostGIS, TimescaleDB, pgvector.

**Phase 1 — Pilot platforms**

- Gaia: Parcel, Cohort, Observation, Recipe services. STAC catalog. Initial codex.
- A3: Lease Service, Event Ledger, Public Record. Initial Lease state machine.
- OpenFactory: ERPNext + first Frappe MES doctypes. UMH integrated. Bridge service v1.

**Phase 2 — Federation**

- Multi-region deployment.
- Federation OIDC.
- Conformance test suite.
- External KG integration (GBIF).
- External credit registry adapter (one to start).

**Phase 3 — Scale**

- Open-RMF multi-vendor fleet support.
- Tier 2 agents in production.
- Sophisticated marketplace logic.
- Sovereign-partition full enforcement.

**Phase 4 — Maturity**

- Tier 3 agents at scale.
- Decadal review tooling.
- Long-term archival migration tested at production scale.

### 10.2 Critical Path

Earliest blockers:

1. Identity infrastructure (everything depends on it).
2. Event bus and schema registry (cross-cutting).
3. PostgreSQL with extensions (data foundation).
4. Gaia observation ingest (everything else needs observations).
5. A3 event ledger (everything else needs immutable record).
6. First Lease formation end-to-end (the actual product).

Without the first Lease formation working end-to-end across Gaia and A3, no other architecture work has demonstrated value.

---

## 11. Open Questions

These are unresolved technical questions:

- **Knowledge graph backend.** Neo4j vs RDF triple store choice still pending. Decision criteria: federation requirements with external scientific KGs, query patterns, operational maturity. May vary by deployment.
- **Schema evolution at planetary scale.** Schema migration across 10⁹ entities is operationally non-trivial. Specific tooling and migration patterns need development.
- **Multi-region event ordering.** Cross-region event ordering with sovereignty constraints requires careful design. Single global ordering is impractical; per-partition ordering plus carefully-designed merge semantics needed.
- **Cost optimization at scale.** Object storage costs at 10¹¹ events become material. Tiering and compression strategy needs explicit work.
- **Robot capability evolution.** Open-RMF supports vendor heterogeneity; capability evolution within vendor is more complex. Versioning and compatibility approach needs design.
- **Reservoir for federation OIDC.** Federating dozens then hundreds of identity providers across federation members is operationally complex. Identity broker design needs work.
- **PostGIS scaling.** PostGIS is excellent at moderate scale; planetary-scale spatial queries may need specialized extensions or offload to GeoParquet/DuckDB analytics path. Threshold and migration path needed.
- **Edge runtime variance.** ROS 2 versions, ONNX runtime versions, hardware variance across robot fleet. Compatibility and update strategy needs explicit design.

---

## Appendix A — Technology Stack Summary

| Layer | Technology | Notes |
|---|---|---|
| Container orchestration | Kubernetes | Multi-cluster via CAPI |
| GitOps | Argo CD | Declarative cluster state |
| Service mesh | Istio or Linkerd | mTLS via SPIFFE |
| API gateway | Envoy + OPA | Policy-based authorization |
| Identity (human) | OIDC (Keycloak/Authentik) | Federation members may federate own |
| Identity (service) | SPIFFE / SPIRE | Short-lived SVIDs |
| Secrets | HashiCorp Vault | Dynamic credentials |
| Operational DB | PostgreSQL + extensions | PostGIS, TimescaleDB, pgvector |
| Knowledge graph | Neo4j or RDF triple store | Decision pending |
| Object storage | S3-compatible (Ceph/MinIO/cloud) | Tiered lifecycle |
| Event bus | Kafka / Redpanda | Multi-region replication |
| Schema registry | Confluent or Apicurio | Versioned schemas |
| Workflow | Temporal | Durable workflows |
| Observability | OpenTelemetry, Prometheus, Grafana, Loki | Full stack |
| Container registry | Harbor + Sigstore | Signed images |
| Frontend (web) | Next.js + Radix + Tailwind | Component library |
| Frontend (mobile) | React Native | Offline-first |
| Robot middleware | ROS 2 | Industry standard |
| Fleet coordination | Open-RMF | Multi-vendor |
| Edge inference | ONNX Runtime | Hardware-portable |
| ERP | ERPNext + Frappe | Self-hosted |
| Shop-floor / UNS | United Manufacturing Hub | External project, integrated |
| Spatial analytics | DuckDB + GeoParquet | Planetary-scale queries |

---

## Appendix B — Cross-References

- Charter (entire corpus depends on it)
- Gaia PRD (functional requirements implemented here)
- A3 PRD (functional requirements implemented here)
- OpenFactory PRD (functional requirements implemented here)
- Protocol Specifications (cross-platform contract)
- Data Lifecycle and Preservation Plan (operational architecture connects here)
- AI Ethical Review Framework (agent governance interfaces with services)
- Threat Model (security architecture defends against named threats)

---

*This document is the engineering layer beneath the PRDs. It is opinionated about technology choices because choices must be made; it is opinionated about patterns because patterns govern long-term maintainability. It will be revised. Specific technologies will be replaced as the ecosystem evolves. The patterns — boring technology, open source, schema first, signed events, multi-region, edge-tolerant — are the durable substance.*
