# OpenFactory

## Product Requirements Document

**System:** OpenFactory, the manufacturing and fleet platform of Robotanica
**Version:** 0.1
**Status:** Draft for review
**Companion documents:** Robotanica Charter, Gaia PRD, A3 PRD, MRV Specification

---

## 1. Overview

OpenFactory is Robotanica's platform of action: the system through which physical operations happen. It manages factories and fleets of robots across two genuinely different production domains:

- **Mechanical production** — robots, components, sensors, and consumables. Classical discrete manufacturing.
- **Biological production** — seedlings, mycorrhizal inoculants, biochar, companion species, and other living or biologically-derived inputs. Closer in shape to pharma batch production or agtech than to discrete manufacturing.

OpenFactory also coordinates **field operations**: planting, tending, monitoring, and harvest by fleets of robots and human operators on the parcels under stewardship.

OpenFactory is bound by recipes from Gaia, dispatched by service contracts from A3, and reports operations and outcomes back to both. It is the layer where intentions become events on the ground.

The platform is built on open-source components: ROS 2 for robot control, Open-RMF for heterogeneous fleet coordination, ERPNext as ERP system of record, a custom Frappe MES app for production modeling, and United Manufacturing Hub (UMH) for shop-floor reality and unified namespace. Where adequate open-source tooling does not exist — particularly for biological production — Robotanica designs and contributes new components.

---

## 2. Problem Statement

Operating restoration at planetary scale requires:

- **Producing biological inputs at scale** — billions of seedlings, large volumes of inoculants and amendments, in quality consistent with Gaia's recipes.
- **Producing the robots and tools** that perform the work — fabrication, assembly, maintenance, retirement.
- **Coordinating heterogeneous fleets** — robots from many vendors and many generations, deployed across many regions, performing many task types.
- **Operating at the edge** — field operations occur in places with intermittent connectivity, harsh conditions, and ecological constraints.
- **Bridging mechanical and biological domains** under one platform so that the genealogy from seed to seedling to mature tree, and from raw component to robot to retired machine, is queryable and complete.
- **Respecting the recipes** from Gaia and the contracts from A3 as authoritative — OpenFactory executes; it does not override.

No existing platform does this combination. MES platforms handle discrete manufacturing but not biological production. Greenhouse management systems handle nursery operations but not robot fleets. Fleet management platforms handle robots but not the production of robots. Agricultural ERP handles farm operations but not at this scale or with this rigor.

OpenFactory is built to integrate these capabilities under the discipline of the Charter, the Gaia and A3 platforms, and the MRV Specification.

---

## 3. Goals and Non-Goals

### 3.1 Goals

- Produce biological inputs at scale: seedlings, inoculants, biochar, companion species, and other recipe-required materials.
- Produce mechanical inputs at scale: robots, components, sensors, consumables.
- Coordinate heterogeneous fleets of robots and human operators across the parcels under stewardship.
- Maintain end-to-end genealogy: from seed source to planted tree, from raw material to deployed robot.
- Execute recipes from Gaia faithfully, with deviations reported and logged.
- Fulfill service contracts from A3 with reliable dispatch, execution, and reporting.
- Operate at the edge: field robots and remote facilities continue to function during connectivity loss.
- Be open-source and built on open-source components.
- Support federation operation: external Operators run their own OpenFactory instances within the Federation's protocol.

### 3.2 Non-Goals

- OpenFactory is not the source of ecological state — that is Gaia.
- OpenFactory is not the contract or governance platform — that is A3.
- OpenFactory is not the planetary observation system — Gaia handles satellite imagery and large-scale observation; OpenFactory provides operational telemetry that feeds Gaia.
- OpenFactory is not a full-stack robotics company — it integrates ROS 2, Open-RMF, and other open robotics infrastructure rather than reinventing them.
- OpenFactory does not perform MRV verification — that is independent (MRV §7); OpenFactory produces the operational evidence MRV draws on.
- OpenFactory does not draft recipes — that is Gaia's interpretation layer.

---

## 4. Users and Personas

| Persona | Primary interaction | Concerns |
|---|---|---|
| Production manager (greenhouse/factory) | Plans production runs; assigns work; reviews quality | Throughput, quality, visibility |
| Fleet operator | Dispatches robots; monitors fleet state; handles exceptions | Real-time visibility, safe operation, exception handling |
| Field technician | Maintains robots; performs hands-on operations; coordinates with fleet | Practical UX, reliability, safety |
| Site steward | Receives operational dispatch; coordinates with fleet on parcel | Local control, safety, ecosystem-aware operation |
| Quality assurance | Audits production runs; investigates deviations | Traceability, evidence chains |
| Robot engineer | Develops, tests, retires robot generations | Open APIs, testbed access, telemetry |
| Biologist (production side) | Manages biological batches; oversees nursery operations | Batch genealogy, environmental control, biological QA |
| Federation Operator | Runs an OpenFactory instance for their own operations | Conformance, federation protocol, sovereignty |
| **System actors** | | |
| Gaia | Source of recipes; receives operational events and observations | Stable contract, reliable feedback |
| A3 | Source of service contract dispatch; receives operation events | Predictable execution, accurate reporting |
| ERPNext | ERP system of record | Integrity of work orders, BOMs, costing |
| UMH | Shop-floor and telemetry layer | Reliable event flow, schema stability |
| Bridge service | Translator between UMH UNS and Frappe MES | Throughput, fidelity, ID propagation |
| Agents (Tier 2/3) | Schedule fleets; perform per-plant decisions; flag anomalies | Bounded action space, human supervision, audit |

---

## 5. Core Concepts and Domain Model

### 5.1 Production Domain Entities

- **Facility** — A physical or logical production location: a greenhouse, a robot fabrication line, a biochar kiln, a mycorrhizal lab, a field-operation depot. Each Facility has a location (geographic and logical), a capability set, and a capacity.
- **WorkOrder** — From ERPNext. The authoritative production order, generated from BOMs and demand.
- **ProductionRun** — A specific instance of executing a WorkOrder: which line, which operators, which materials, which time window.
- **BOM** — From ERPNext. Bill of materials for a produced item, including biological items (seedlings have BOMs too: substrate, inoculant, water, energy).
- **Item** — From ERPNext. A produced or consumed item, mechanical or biological.
- **Genealogy** — The chain of provenance for an Item: source materials, processing operations, operators, conditions, batch links.

### 5.2 Biological Production Entities

- **BiologicalBatch** — A cohort of biological items produced together: a tray of seedlings, a batch of mycorrhizal inoculant, a kiln run of biochar. Has genealogy (parent batches, source materials), environmental history, and quality state.
- **Cohort** (shared with Gaia) — When a BiologicalBatch leaves OpenFactory and enters the field as plants, it becomes a Cohort in Gaia. The transition is recorded with full genealogy.
- **GeneticLineage** — The traceable lineage of biological material: seed source, parent genetics, selection history. Subject to Charter §5.3 (no patenting).
- **EnvironmentEpisode** — A bounded period of recorded environmental conditions (temperature, humidity, light, water, nutrients) under which a BiologicalBatch was produced. Drawn from UMH telemetry, summarized into bounded episodes.

### 5.3 Mechanical Production Entities

- **RobotAssemblyRecord** — The full assembly record of a specific robot: components used, assembly operators, tests performed, calibrations applied, firmware versions, software versions.
- **Component** — A discrete part used in a robot or other manufactured good, with its own genealogy.
- **Robot** — An individual deployed robotic unit, with stable identity, capability profile, current state, location, maintenance history, and assembly record.

### 5.4 Fleet and Operation Entities

- **Fleet** — A group of Robots managed together for dispatch purposes. Fleets are organized by region, capability, and Operator (Robotanica or federation member).
- **Mission** — A higher-level tasked outcome: "plant cohort X on parcel Y to recipe Z." A Mission decomposes into Operations.
- **Operation** — A unit of work performed by a Robot or human operator: planting an individual tree, taking a measurement, applying an inoculant, removing a weed, performing a maintenance check.
- **OperationEvent** — An immutable record of an Operation occurring (or attempted, or failed), with full provenance: who/what performed it, when, where, with what input, with what result.
- **MaintenanceEvent** — An immutable record of robot maintenance: routine, repair, calibration, retirement.

### 5.5 Identity Model

Every entity has a stable URI:

```
of://<type>/<region>/<id>[@<version>]
```

Robots have stable identifiers across their lifetime. BiologicalBatches retain their identifiers when transitioning to Gaia Cohorts, with the transition recorded as a cross-system event.

### 5.6 Recipe Binding

ProductionRuns and Missions are bound to recipes from Gaia at specific versions. The binding is recorded; recipe deviation is reported as an operational event and may trigger Gaia's recipe revision protocol.

---

## 6. Functional Requirements

Each requirement has an ID. Priority levels: **MUST**, **SHOULD**, **MAY**.

### 6.1 Facility and Production Management

- **OF-P-001 (MUST)** Maintain a registry of Facilities with location, capability, capacity, and current state.
- **OF-P-002 (MUST)** Receive WorkOrders from ERPNext and execute them as ProductionRuns.
- **OF-P-003 (MUST)** Schedule ProductionRuns against Facility capacity, considering current load, maintenance, and dependencies.
- **OF-P-004 (MUST)** Record ProductionRun execution: start, materials consumed, operators involved, environmental conditions, quality outcomes, completion.
- **OF-P-005 (MUST)** Maintain end-to-end genealogy from input materials to output Items.
- **OF-P-006 (SHOULD)** Surface ProductionRuns at risk of missing target throughput or quality before completion, for operator intervention.

### 6.2 Biological Production

- **OF-B-001 (MUST)** Manage BiologicalBatches with full genealogy: parent batches, source materials, environmental history.
- **OF-B-002 (MUST)** Bind BiologicalBatches to Gaia recipes; deviations from recipe (substrate substitution, inoculant variation, environmental departure) are recorded as operational events.
- **OF-B-003 (MUST)** Receive environmental telemetry from UMH and summarize it into EnvironmentEpisodes attached to BiologicalBatches.
- **OF-B-004 (MUST)** Record Quality Checks per BiologicalBatch: germination rates, contamination tests, growth metrics, viability assays.
- **OF-B-005 (MUST)** Manage GeneticLineage with full traceability to seed source, with refusal to issue Items lacking genealogy.
- **OF-B-006 (MUST)** Coordinate the transition from BiologicalBatch (OpenFactory) to Cohort (Gaia) when biological material is deployed to a parcel: identifiers preserved, genealogy carried forward.
- **OF-B-007 (SHOULD)** Apply biosecurity protocols: quarantine, contamination testing, inter-facility transfer controls.
- **OF-B-008 (MUST)** Refuse to ship BiologicalBatches that fail Quality Check thresholds for their recipe.

### 6.3 Mechanical Production

- **OF-M-001 (MUST)** Manage RobotAssemblyRecords with full component genealogy, operator records, and test histories.
- **OF-M-002 (MUST)** Maintain firmware and software version records per Robot, with update history.
- **OF-M-003 (MUST)** Implement supply chain attestation: components from verified sources, with tamper-evident records (per Threat Model §5.3).
- **OF-M-004 (MUST)** Refuse to deploy Robots failing assembly or commissioning quality checks.
- **OF-M-005 (SHOULD)** Support federation Operators producing their own robot designs while sharing platform infrastructure for management.

### 6.4 Fleet Management

- **OF-F-001 (MUST)** Maintain a registry of Robots with capability profile, current state, location, fleet membership, and Operator.
- **OF-F-002 (MUST)** Use Open-RMF (Open Robotics Middleware Framework) for heterogeneous multi-vendor fleet coordination where applicable.
- **OF-F-003 (MUST)** Use ROS 2 for robot control interfaces; robots without ROS 2 are integrated through adapters.
- **OF-F-004 (MUST)** Track Robot lifecycle: commissioned, deployed, in-operation, in-maintenance, retired.
- **OF-F-005 (MUST)** Schedule and dispatch Robots to Missions based on capability match, location, current load, and Mission priority.
- **OF-F-006 (MUST)** Support real-time fleet visibility: location, state, current Operation, alerts.
- **OF-F-007 (MUST)** Handle fleet exceptions: stuck robots, depleted resources, sensor failures, communication loss; route to maintenance as needed.
- **OF-F-008 (SHOULD)** Optimize fleet assignments for throughput, energy efficiency, and ecosystem-aware operation (avoiding sensitive areas, respecting wildlife windows).

### 6.5 Mission and Operation Lifecycle

- **OF-O-001 (MUST)** Receive Mission requests from A3 (via ServiceContract dispatch) and from Robotanica's internal operations.
- **OF-O-002 (MUST)** Decompose Missions into Operations bound to recipe-specified procedures.
- **OF-O-003 (MUST)** Dispatch Operations to Robots or human operators per fleet management.
- **OF-O-004 (MUST)** Record each OperationEvent immutably with full provenance.
- **OF-O-005 (MUST)** Report Mission completion or failure to A3 with full operational record.
- **OF-O-006 (MUST)** Synchronize OperationEvents with Gaia: every plant placed, every measurement taken, every intervention applied is recorded as an Observation in Gaia (per Gaia §6.2).
- **OF-O-007 (MUST)** Support Mission abort and rollback when conditions require: weather emergency, ecological discovery (rare species, archaeological find), safety concern, Landowner request.

### 6.6 Edge Operation

- **OF-E-001 (MUST)** Field robots operate without continuous network connectivity; basic perception, navigation, and operation execute at the edge using ONNX Runtime or equivalent.
- **OF-E-002 (MUST)** Field robots queue OperationEvents locally when offline; sync to UMH when connectivity returns.
- **OF-E-003 (MUST)** Field robot behavior in offline mode is bounded by safe defaults: no novel terrain exploration, no operations outside dispatched mission scope.
- **OF-E-004 (SHOULD)** Multi-robot coordination at the edge through local-network protocols when wide-area connectivity is unavailable.

### 6.7 Quality and Safety

- **OF-Q-001 (MUST)** Record Quality Checks for both biological and mechanical Items with structured results, signed by the inspector or system performing the check.
- **OF-Q-002 (MUST)** Refuse to ship Items failing Quality Checks; quality holds propagate to ERPNext and to dependent Missions.
- **OF-Q-003 (MUST)** Implement safety controls for robot operations: geofencing, human-proximity awareness, ecosystem-sensitive zones, weather and condition limits.
- **OF-Q-004 (MUST)** Support safety overrides by site stewards, field technicians, and Landowners: any local human authority can halt local operations.
- **OF-Q-005 (MUST)** Record all safety events (overrides, near-misses, incidents) immutably, with review and remediation tracking.
- **OF-Q-006 (MUST)** Robot perception cross-verification: high-stakes decisions (large-tree felling, area-effect application) require multi-modal confirmation or human authorization.

### 6.8 Maintenance

- **OF-MN-001 (MUST)** Schedule routine Robot maintenance based on usage, condition, and manufacturer recommendation.
- **OF-MN-002 (MUST)** Record MaintenanceEvents with full detail: actions performed, parts replaced, tests after, operator.
- **OF-MN-003 (MUST)** Manage Robot retirement: parts recovery, decommissioning records, environmental disposal.
- **OF-MN-004 (SHOULD)** Use telemetry and predictive analytics to forecast maintenance needs before failure.

### 6.9 Federation Operation

- **OF-X-001 (MUST)** Support federation Operators running their own OpenFactory instances within the Federation protocol.
- **OF-X-002 (MUST)** Enforce conformance: federation OpenFactory instances must satisfy the platform's published contracts for events, telemetry, genealogy, and reporting.
- **OF-X-003 (MUST)** Support sovereignty: federation Operators maintain their own data within their jurisdiction; cross-Operator data flows are policy-controlled.
- **OF-X-004 (SHOULD)** Allow forking per Charter §5.4: a region or community may take OpenFactory's reference implementation and operate independently.

### 6.10 Bridge Service (UMH ↔ ERPNext + Frappe MES)

- **OF-BR-001 (MUST)** Subscribe to UMH UNS topics; translate events into Frappe doctype updates via REST.
- **OF-BR-002 (MUST)** Publish ERPNext state changes (work order release, BOM revision, quality hold) back to UMH UNS.
- **OF-BR-003 (MUST)** Propagate batch and work-order IDs through the MQTT topic hierarchy as correlation keys.
- **OF-BR-004 (MUST)** Aggregate or debounce high-frequency UMH events that should not be written one-for-one to Frappe; persist raw events in UMH for audit.
- **OF-BR-005 (SHOULD)** Support replay: the bridge can re-process UNS topics for a time range to reconstruct ERPNext state if needed.

---

## 7. Non-Functional Requirements

### 7.1 Scale

- **OF-N-001** Support 10⁹ biological items per year at full deployment (seedlings dominant).
- **OF-N-002** Support 10⁶ active Robots across the federation.
- **OF-N-003** Support 10¹¹ OperationEvents per year at peak (high-frequency per-plant operations dominant).
- **OF-N-004** Support 10² Facilities at full Robotanica scale; many more under federation Operators.

### 7.2 Performance

- **OF-N-010** P95 latency for fleet state query: < 500 ms.
- **OF-N-011** Real-time fleet telemetry latency (robot to dashboard): < 5 s when connected.
- **OF-N-012** Mission dispatch latency from A3 service contract acceptance: < 5 minutes for non-emergency dispatch.
- **OF-N-013** OperationEvent ingest from UMH to Frappe MES (via bridge): < 30 s P95 for state-relevant events.

### 7.3 Edge Resilience

- **OF-N-020** Field robots operate offline for at least 72 hours without losing operational capability or queued events.
- **OF-N-021** Edge perception latency (robot decision loop): < 100 ms for routine operations.
- **OF-N-022** Local fleet coordination at the edge supports up to 50 robots in a coordinated cluster without wide-area connectivity.

### 7.4 Durability

- **OF-N-030** All ProductionRun, BiologicalBatch, RobotAssemblyRecord, OperationEvent, and MaintenanceEvent records are immutable and replicated across at least three regions.
- **OF-N-031** ERPNext data has standard backup and disaster recovery; recovery point objective < 1 hour, recovery time objective < 4 hours.
- **OF-N-032** UMH telemetry retention: hot for 90 days, warm for 2 years, cold archival for the lifetime of the Robot or BiologicalBatch's downstream Cohort plus 50 years.

### 7.5 Multi-Decade Operability

- **OF-N-040** Robot genealogies remain queryable for the lifetime of any downstream restoration claim (50+ years).
- **OF-N-041** BiologicalBatch genealogies remain queryable for the lifetime of the resulting Cohort plus 50 years.
- **OF-N-042** Component, BOM, and recipe versions are preserved with their original semantics; reproducibility of past operations is maintained.

### 7.6 Heterogeneity

- **OF-N-050** Multi-vendor Robot support via Open-RMF and ROS 2 adapters.
- **OF-N-051** Multi-generation Robot support: older Robots remain operable while newer Robots are introduced; retirement is graduated, not abrupt.
- **OF-N-052** Multi-modality biological production: open-air greenhouses, controlled environments, in-situ propagation, and biomass-based production share platform infrastructure where appropriate.

### 7.7 Security

- **OF-N-060** API access authenticated (OIDC), authorized (attribute-based, with facility and Robot scope).
- **OF-N-061** Robot-to-platform identity is SPIFFE-based; Robots cannot impersonate other Robots.
- **OF-N-062** Firmware and software signed; Robots verify signatures before executing.
- **OF-N-063** Edge-stored data encrypted at rest; secrets rotated.
- **OF-N-064** Supply chain attestation for components per Threat Model §5.3.

### 7.8 Safety

- **OF-N-070** All field operations conform to applicable jurisdictional safety regulations.
- **OF-N-071** Geofencing and human-proximity awareness operate at the edge; do not require network for safety enforcement.
- **OF-N-072** Emergency stop is universally available; any Robot can be remotely or locally halted.
- **OF-N-073** Ecosystem-sensitive zones (vulnerable species, archaeological sites, sacred sites) are honored by Robot navigation absent override.

### 7.9 Observability

- **OF-N-080** OpenTelemetry traces, metrics, and logs across all services.
- **OF-N-081** Fleet, facility, and production dashboards available to operators.
- **OF-N-082** Every agent action logged for evaluation per Gaia §7.4.

---

## 8. Architecture

### 8.1 Component Overview

```
                ┌──────────────────────────────────────────────────┐
                │                  OpenFactory                     │
                │                  API Surface                     │
                │  REST · GraphQL · Events · Telemetry Bridge      │
                └──────────────────────────────────────────────────┘
                           ▲              ▲              ▲
                           │              │              │
       ┌───────────────────┴──┐  ┌────────┴────────┐  ┌──┴────────────────┐
       │  Production Layer    │  │  Fleet Layer    │  │  Mission Layer    │
       │  (Frappe MES app on  │  │  (Open-RMF +    │  │  (Mission planner,│
       │   ERPNext, biologic  │  │   ROS 2 fleet   │  │   dispatch, edge  │
       │   + mechanical)      │  │   adapters)     │  │   coordination)   │
       └──────────────────────┘  └─────────────────┘  └───────────────────┘
                  ▲                       ▲                      ▲
                  │                       │                      │
       ┌──────────┴───────┐   ┌───────────┴────────┐   ┌─────────┴─────────┐
       │   ERPNext        │   │  UMH               │   │  Edge Runtimes    │
       │   (ERP system    │   │  (telemetry, UNS,  │   │  (ROS 2 nodes,    │
       │   of record)     │   │   TimescaleDB)     │   │   ONNX inference) │
       └──────────────────┘   └────────────────────┘   └───────────────────┘
                  ▲                       ▲
                  │                       │
                  └────────┬──────────────┘
                           ▼
                ┌─────────────────────────┐
                │    Bridge Service       │
                │    (UMH ↔ Frappe MES)   │
                └─────────────────────────┘
                           │
                           ▼
                ┌─────────────────────────┐
                │   Identity & Access     │
                │   OIDC · SPIFFE         │
                │   Sovereignty policy    │
                └─────────────────────────┘
                           │
                           ▼
                ┌─────────────────────────┐
                │   Durable Workflows     │
                │   (Temporal): Missions, │
                │   long-running ops      │
                └─────────────────────────┘
```

### 8.2 The Three Layers

**Production layer.** ERPNext provides ERP services (work orders, BOMs, items, costing). The custom Frappe MES app extends ERPNext with Robotanica-specific doctypes: `ProductionRun`, `BiologicalBatch`, `Cohort` (transitioning), `GeneticLineage`, `EnvironmentEpisode`, `RobotAssemblyRecord`, `Component`. The MES app provides the operator-facing UI for production work. UMH provides the telemetry and shop-floor reality layer beneath.

**Fleet layer.** Open-RMF coordinates heterogeneous Robots from multiple vendors and generations. ROS 2 is the control interface; Robots without native ROS 2 support are bridged through adapters. Fleet state is published to UMH UNS; fleet dispatch is computed against current state and Mission backlog.

**Mission layer.** Mission planning translates A3 service contracts and Gaia recipes into concrete sequences of Operations. Dispatch routes Operations to Robots or human operators. Edge coordination handles local-cluster operation when wide-area connectivity is degraded.

### 8.3 The Bridge Service

The bridge service is small (~one engineer-month for v1, per the white paper) but central. It:

- Subscribes to UMH UNS topics.
- Translates events into Frappe doctype updates via REST.
- Aggregates high-frequency events to avoid overwhelming Frappe.
- Publishes ERPNext state changes back to UNS.
- Propagates batch and work-order IDs through MQTT topic hierarchy.

It is replaceable: the contract is the UNS topic schema and the Frappe doctype schema; an alternative bridge implementation that conforms is acceptable.

### 8.4 Edge Runtimes

Field Robots run ROS 2 nodes for control, ONNX Runtime for perception inference, and a local UMH agent that buffers events. Edge runtimes are designed for:

- **Offline tolerance** — the Robot continues to perform safe operations during connectivity loss.
- **Eventual consistency** — events sync to UMH when connectivity returns; the bridge service then propagates them to Frappe MES.
- **Bounded autonomy** — the Robot does not make decisions outside its dispatched Mission scope; novel decisions require connectivity and human authorization.

### 8.5 Storage Layout

- **ERPNext (MariaDB or PostgreSQL)** — work orders, BOMs, items, financial records, custom Frappe doctypes for Robotanica entities.
- **UMH (TimescaleDB + object storage)** — time-series telemetry, raw event archival.
- **Object storage** — long-term archival of operational records, RobotAssemblyRecords, and BiologicalBatch genealogy in open formats.
- **Edge storage on Robots** — local buffers for offline operation; cleared after sync.

### 8.6 Cryptographic Provenance

OperationEvents are signed by the executing principal (Robot identity, human operator, or service identity). Signatures are part of the event payload and are verifiable independently of OpenFactory's runtime. The signed event log is the primary record of what happened in the field.

### 8.7 Durable Workflows

Temporal hosts long-running workflows: Mission lifecycles spanning days to weeks, BiologicalBatch lifecycles spanning weeks to months, Robot maintenance schedules spanning years.

### 8.8 Event Bus

Kafka or Redpanda carries OpenFactory events to Gaia, A3, and other consumers. Topics include: `of.production-run.lifecycle`, `of.biological-batch.lifecycle`, `of.robot.lifecycle`, `of.mission.lifecycle`, `of.operation.event`, `of.maintenance.event`.

---

## 9. APIs

### 9.1 External API Surface

- **REST** for CRUD-style access to Facilities, Robots, Fleets, Missions, Operations, ProductionRuns, BiologicalBatches, MaintenanceEvents.
- **GraphQL** for federated reads composing across entities.
- **Event subscriptions** on Kafka topics (per §8.8).
- **ROS 2 interfaces** for Robot integration; Open-RMF interfaces for fleet coordination.
- **UMH UNS** for telemetry and shop-floor reality.

### 9.2 Specifications

- All synchronous APIs in **OpenAPI 3.1**.
- All event APIs in **AsyncAPI 2.x**.
- All entity schemas in **JSON Schema** with stable `$id` URIs.
- ROS 2 interfaces specified through standard ROS 2 messaging.

### 9.3 SDKs

Python and TypeScript SDKs for platform APIs. ROS 2 client libraries for Robot integration. SDKs are generated from specifications where possible.

---

## 10. Integrations

| System | Direction | Interface | Data flowing |
|---|---|---|---|
| Gaia | Bidirectional | REST + Events | Recipes (in), parcel state (in), OperationEvents and Cohort transitions (out) |
| A3 | Bidirectional | REST + Events | Service contract dispatch (in), Mission completion (out), batch genealogy (out) |
| ERPNext | Embedded | Frappe REST + DocTypes | Work orders, BOMs, items, custom production data |
| UMH | Embedded | MQTT/Sparkplug-B + UNS | Telemetry, machine connectivity, time-series storage |
| External robot vendors | Inbound | ROS 2 + Open-RMF + adapters | Robot capabilities, telemetry, control |
| External seed banks and genetic suppliers | Inbound | Per-supplier APIs | Genetic provenance, seed lots, certifications |
| External component suppliers | Inbound | Per-supplier APIs | Component genealogy, supply chain attestation |
| Federation Operator instances | Bidirectional | OpenFactory protocol | Conforming events, telemetry, genealogy |
| Agents (Tier 2/3) | Bidirectional | REST + edge runtime | Reads for context; writes for proposals (Tier 2) and high-frequency observations (Tier 3) |

---

## 11. Success Metrics

### 11.1 System Health

- Platform availability (P95 over rolling 30 days): > 99.9%.
- ERPNext availability: standard ERP SLA per ERPNext deployment.
- UMH telemetry ingest success: > 99.9%.
- Bridge service event throughput SLO met (per topic, per region).

### 11.2 Production Health

- ProductionRun completion rate (on-time, on-spec): > 95%.
- BiologicalBatch quality pass rate: tracked per recipe; recipe-specific thresholds.
- Robot first-pass commissioning rate: > 95%.
- Genealogy completeness: 100% (every Item has full genealogy or is rejected).

### 11.3 Fleet Health

- Robot operational uptime (excluding scheduled maintenance): > 90%.
- Mission completion rate (on-time, on-spec): > 95%.
- Edge offline tolerance demonstrated: Robots complete dispatched Missions during simulated 72-hour offline.
- Safety incidents per million Robot-hours: tracked; trend monitored.

### 11.4 Recipe and Outcome Alignment

- Recipe deviations reported per ProductionRun and Mission: tracked, not bounded; deviations are signal, not failure.
- OperationEvents synchronized to Gaia: 100% within currency window.
- Cohort transition completeness (BiologicalBatch → Gaia Cohort): 100% with full genealogy.

### 11.5 Mission Alignment

- Total seedlings produced.
- Total seedlings deployed.
- Total Operations executed.
- Total Robot-hours in field operations.

These are reported by OpenFactory but are OKRs of Robotanica, not OpenFactory in isolation.

---

## 12. Phasing

| Phase | Scope | Exit criteria |
|---|---|---|
| 0 — Foundations | ERPNext + Frappe MES app v0; UMH integrated; first Facility operational | First WorkOrder executed end-to-end with full genealogy |
| 1 — Pilot | First greenhouse at scale; first robot prototypes; first field Mission | First Cohort transitions from BiologicalBatch to Gaia with full genealogy; first robot Mission completed |
| 2 — Fleet | Multi-Robot fleets; Open-RMF integration; multi-vendor support | Multi-vendor fleet executing coordinated Mission |
| 3 — Federation | Federation Operators running OpenFactory instances; protocol conformance | First Federation Operator executes Mission via own OpenFactory instance |
| 4 — Scale | Multi-region production; planetary fleet operations; agent integration at Tier 2/3 | NFRs at §7.1 sustained for 90 days; Tier 3 agents operating with measured outcome alignment |

Phase boundaries are exit criteria, not dates.

---

## 13. Risks and Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Biological production failure (contamination, pest, disease) | Loss of cohorts; mission delay | Biosecurity protocols; multi-source production for critical inputs; quality holds; quarantine procedures |
| Robot supply chain compromise | Compromised robots in the field; falsified telemetry | Verified component sourcing; supply chain attestation; firmware signing; runtime integrity checks; periodic audit (Threat Model §5.3) |
| Edge connectivity failure beyond planning bounds | Operations stalled; safety risk | Robust offline mode; safe-default behavior; local coordination protocols; manual operator override |
| Multi-vendor robot coordination failure | Fleet operates inefficiently or unsafely | Open-RMF as standard; vendor adapter discipline; conformance testing for new vendors |
| Recipe execution drift | Operations diverge from recipe; outcomes degrade | Recipe binding at dispatch; deviation events; Gaia recipe revision triggered by drift |
| Worker safety incidents | Harm to humans | Safety-first protocols; refusal authority for field workers; jurisdiction compliance; insurance and support |
| Genetic drift in biological lines | Loss of recipe integrity over generations | Genetic verification at intervals; outsourcing of foundational genetic stock to specialists; codex-bound species references |
| Frappe MES performance limits | Unable to scale to required throughput | Bridge aggregation; UMH absorbs high-frequency state; Frappe handles state transitions only |
| ERPNext deployment fragility at scale | Production halt on ERPNext failure | Robust ERPNext deployment; hot standby; regular DR exercises |
| Federation conformance erosion | Operator instances diverge from protocol | Conformance test suite mandatory for federation members; periodic recertification; suspension procedures |
| AI agent-driven operational drift | Operational decisions biased by agent suggestions | Tier 3 agents constrained to bounded actions; Tier 2 actions human-reviewed; agent provenance distinct; outcome-driven evaluation |

---

## 14. Open Questions

- **Scaling Frappe.** ERPNext + Frappe is excellent for the medium-scale operations of early phases. At full deployment with billions of biological items, the scaling envelope of Frappe needs validation. Alternatives may be needed for specific high-volume entities (e.g., individual seedling records).
- **ROS 2 longevity.** ROS 2 is the right choice today; the open-source robotics standard 30 years from now is unknown. Migration paths must be considered.
- **Robot retirement and recycling.** Where do retired Robots go? What is reused, recycled, salvaged for parts? This is an ecological question as much as an operational one.
- **Federated genealogy across Operators.** When BiologicalBatches or Robots transit between Federation Operators, how is genealogy preserved across data-sovereignty boundaries?
- **Edge AI capability evolution.** As edge AI improves, more decisions can move to Robots in the field. The framework for moving the autonomy line needs structure (Charter §2.8 reversibility principle applies).
- **Biosecurity at planetary scale.** Pathogen and pest movement through OpenFactory's logistics network is a real risk. Dedicated biosecurity protocols beyond the routine quality controls may be needed.
- **Heterogeneous fleet failure modes.** When old and new Robots, multiple vendors, and edge cases interact, failure modes can be subtle. The fleet management discipline needs to be hardened over time.
- **Safety regulatory evolution.** Field robots in agricultural and ecological settings are subject to evolving regulation. Multi-jurisdictional compliance is non-trivial.

---

## Appendix A — Glossary (OpenFactory-Specific)

- **BiologicalBatch** — A cohort of biological items produced together with full genealogy.
- **BOM** — Bill of Materials. From ERPNext.
- **Bridge Service** — The translator between UMH UNS and ERPNext + Frappe MES.
- **Component** — A discrete part used in a Robot or other manufactured good.
- **Cohort** — A group of plants of common provenance (shared with Gaia); transitions from BiologicalBatch when deployed.
- **EnvironmentEpisode** — A bounded period of recorded environmental conditions attached to a BiologicalBatch.
- **Facility** — A physical or logical production location.
- **Fleet** — A group of Robots managed together for dispatch.
- **GeneticLineage** — Traceable biological lineage; subject to no-patenting per Charter §5.3.
- **Item** — A produced or consumed item; from ERPNext.
- **MaintenanceEvent** — An immutable record of Robot maintenance.
- **MES** — Manufacturing Execution System.
- **Mission** — A higher-level tasked outcome.
- **Open-RMF** — Open Robotics Middleware Framework. Heterogeneous fleet coordination.
- **Operation** — A unit of work performed.
- **OperationEvent** — An immutable record of an Operation.
- **ProductionRun** — A specific instance of executing a WorkOrder.
- **Robot** — An individual deployed robotic unit.
- **RobotAssemblyRecord** — Full assembly record of a specific Robot.
- **ROS 2** — Robot Operating System 2. The standard robotics middleware.
- **UMH** — United Manufacturing Hub.
- **UNS** — Unified Namespace.
- **WorkOrder** — From ERPNext; the authoritative production order.

---

## Appendix B — Standards and References

- **ROS 2** (Robot Operating System 2).
- **Open-RMF** (Open Robotics Middleware Framework).
- **MQTT** and **Sparkplug-B** for telemetry.
- **OPC-UA** for industrial machine connectivity.
- **ISA-95** for the manufacturing systems hierarchy.
- **OpenAPI** 3.1, **AsyncAPI** 2.x, **JSON Schema**.
- **OIDC**, **SPIFFE**.
- **ERPNext** and **Frappe Framework**.
- **United Manufacturing Hub (UMH)**.
- **ONNX Runtime** for edge inference.
- **OpenTelemetry** for observability.

---

*This is v0.1 of the OpenFactory PRD. It will evolve substantially as biological production scales beyond pilot, as multi-vendor fleets are integrated, and as the Federation expands beyond Robotanica's own operations.*
