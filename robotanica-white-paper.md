# Robotanica

## A Platform for Planetary Biosphere Restoration

**White Paper · v0.2**

---

## Executive Summary

Robotanica's mission is to restore the biosphere. Its primary OKR is adding one trillion adult trees to Earth, measured at survival to maturity on a horizon of decades. Earth currently hosts roughly three trillion trees; the goal proposes a 33% increase in standing biomass at maturity, in a context where most planted trees die before adulthood. Robotanica is therefore a steward of self-perpetuating ecosystems, and planting is one early step in a long lifecycle.

To accomplish this, Robotanica operates three platforms, built on open-source foundations and connected by a unified namespace and event bus:

- **Gaia** — planetary state, observation, and ecological knowledge
- **A3 Agro As API** — land governance and rights coordination
- **OpenFactory** — manufacturing and fleet operations

The organization is small at the core (an estimated 30–80 people), with a protocol-led federation extending to thousands of operators, landowners, scientists, and partner labs. The technical strategy is biased toward open-source components and toward minimizing platform count; where adequate open-source tooling does not exist, Robotanica designs and contributes new components rather than buying proprietary alternatives.

This paper specifies the foundational mental models, organizational design, platform architecture, technology stack, agent architecture, and governance layer required to operate Robotanica.

---

## 1. Mission and the Honest Metric

The headline OKR is one trillion adult trees. The operational metric is:

> **Survival-to-maturity rate × planting throughput × area available**

Of these three terms, survival-to-maturity dominates because it operates on the slowest timescale (decades) and is the most variable (typical reforestation projects report mortality between 30% and 90%). Throughput and area are the terms most amenable to robotic and platform-led acceleration, but only after the survival problem is solved by ecological design.

This implies a cascade of derived metrics tracked at the platform layer:

| Layer | Time horizon | Primary metric |
|---|---|---|
| Operations | Days–months | Seedlings established, fleet utilization, factory yield |
| Site | 1–10 years | Survival rate by cohort, biodiversity index, soil health |
| Ecosystem | 10–50 years | Canopy closure, holobiont integrity, trophic recovery |
| Planetary | 50+ years | Net standing biomass, carbon stock, ecosystem service value |

Survival data from year 5 onward is the most important feedback signal for every other system. It trains the agents, validates the recipes in Gaia, and determines whether contracts on A3 are honored.

---

## 2. Foundational Mental Models

### 2.1 Pace Layers (Stewart Brand)

Robotics iterates monthly. Soil microbiomes shift over years. Canopy succession over decades. Climate over centuries. The organization is designed so that fast layers serve slow layers, never the reverse. Most prior tech-for-trees projects fail because they optimize the layer they can measure this quarter.

### 2.2 Commons Governance (Elinor Ostrom)

Land and biosphere are commons. A3 will succeed or fail according to whether it embodies Ostrom's eight design principles for long-enduring common-pool resource institutions: clear boundaries, congruence with local conditions, collective-choice arrangements, monitoring, graduated sanctions, conflict-resolution mechanisms, recognition of self-governance, and nested enterprises. These principles are encoded as constraints in the A3 protocol itself.

### 2.3 Holobiont Thinking

A tree without its mycorrhizae, pollinators, soil biota, and successional companions is a stick. Gaia models the holobiont, not just the stems. OpenFactory produces inoculants and companion species, not just seedlings. Recipe primitives are ecosystem assemblages, not single species.

### 2.4 Leverage Points (Donella Meadows)

The highest-leverage interventions are rarely "more robots." They are, in Meadows' ascending order: paradigms, goals, self-organization rules, information flows, and feedback loops. The platform architecture privileges these high-leverage points: the protocol (rules), the codex (information), the survival metrics (feedback).

### 2.5 Viable System Model (Stafford Beer)

Local operations are autonomous within constraints set by regional, set by global. Decisions that should be made on the ground are pushed to the ground. The platforms enforce constraints, not procedures.

### 2.6 Operating Methodologies

Three traditions of practice underpin Robotanica's biological work:

- **Miyawaki method** — dense, native, multi-species pocket forests with accelerated succession
- **Holistic Management (Savory)** — restoration of brittle grasslands through managed herd impact, recognizing that grassland and forest restoration are coupled. Savory's carbon-sequestration claims are contested in the rangeland-science literature; the operational planning framework is more robust than the climate claims, and Robotanica adopts it on that basis
- **Ecosystem Restoration (Liu / FMNR)** — landscape-scale restoration through human stewardship, exemplified by the Loess Plateau project and Farmer Managed Natural Regeneration in the Sahel

These methodologies are encoded as templates in Gaia's interpretation layer and instantiated as recipes in A3.

---

## 3. Organizational Design

Robotanica is structured as a small permanent core plus an open protocol that admits a federation of operators, landowners, laboratories, and partner organizations.

### 3.1 Permanent Core

Three product organizations, one per platform (Gaia, A3, OpenFactory), with shared infrastructure. The Gaia organization includes both platform engineering and the science and curation function that maintains the interpretation layer.

### 3.2 Cross-Cutting Bodies

- **Science Council** — ecologists, soil scientists, indigenous land stewards, restoration practitioners. Holds veto authority over species choices, site recipes, and intervention protocols. The Council exists because robotics-led teams will reliably propose monocultures of fast-growing exotics if no one is empowered to say no.

- **Stewardship Office** — owns the multi-decade contracts with landowners. Operates on a longer planning horizon than the product organizations and is insulated from quarterly performance pressure.

### 3.3 Federation

The protocol admits external operators (planting and tending services), landowners (committing land to A3), scientists (contributing recipes to Gaia), fabricators (producing components for OpenFactory), and partner organizations (ecosystem restoration camps, regenerative agriculture cooperatives, indigenous land councils).

Robotanica's moat is the protocol, not the org chart.

---

## 4. Platform Architecture

Three platforms, organized around the classical state, coordination, and action decomposition: Gaia is what is and what is known; A3 is what is agreed; OpenFactory is what is done.

### 4.1 Gaia — State and Knowledge

Gaia is Robotanica's epistemic platform: the integrated record of the biosphere as Robotanica observes it and understands it. It comprises two tightly-coupled layers:

**Observation layer (the twin)** — a planetary-scale spatial database of all land under Robotanica stewardship, every tree and cohort, environmental sensor data, satellite imagery time-series, and derived ecological indicators. Canonical for *what is true on the ground*.

**Interpretation layer (the codex)** — a versioned, citable, contestable knowledge graph of species, ecosystems, intervention recipes, and outcomes. Canonical for *what is known about how the biosphere works*.

The two layers are one platform because the feedback loop between them is the highest-leverage loop in the company: an observation in the twin is evidence that may update the codex; a recipe in the codex is a hypothesis that the twin tests on the ground. Separating them administratively or technically creates friction at exactly the data flow that should have none.

**Responsibilities**

- Land parcels, ownership, and rights (sourced from A3)
- Tree and cohort lifecycle records
- Environmental time-series (soil moisture, temperature, humidity, growth)
- Remote-sensing imagery and derived indices (NDVI, canopy cover, biomass)
- Predictive models for site suitability, mortality risk, and intervention timing
- Species and ecosystem ontology
- Site-recipe templates (Miyawaki, Savory, Liu, regional variants)
- Empirical outcome records linked back to observations
- Recipe contestation and revision protocol
- Provenance and citation graph

Without Gaia's integrated structure, A3 would broker contracts that OpenFactory would fulfill that the twin would measure, with no system knowing whether the recipe was ecologically sound. Gaia closes this loop by construction.

### 4.2 A3 Agro As API — Coordination and Governance

The land-rights and service-coordination platform. Landowners commit land; operators commit services; the platform brokers planting, tending, and monitoring contracts.

**Responsibilities**

- Land submission, verification, and lifecycle
- Rights registry (planting, harvesting, monitoring, succession)
- Recipe selection (drawn from Gaia)
- Operator marketplace and dispatch
- Multi-decade contract instruments (see §8)
- Audit trail and provenance

A3's protocol embeds Ostrom's eight principles as enforced constraints, not aspirational principles.

### 4.3 OpenFactory — Action and Manufacturing

The platform for managing factories and fleets of robots. Used for:

- Greenhouses (seedling and biological-input production)
- Robot fabrication (and components and consumables)
- Field operations (planting, tending, monitoring fleets)

OpenFactory bridges classical discrete manufacturing (robots, components) and biological production (seedlings, inoculants, biochar). These two domains share a framework but require different data models — see §6 for the manufacturing-stack decision.

---

## 5. Technology Stack

### 5.1 Gaia

**Observation layer**

- **PostGIS** for spatial data
- **TimescaleDB** for sensor and growth time-series
- **pgvector** for embeddings of satellite tiles and species descriptions
- **STAC** for the imagery catalog
- **GeoParquet + DuckDB** for analytical queries at planetary scale (PostGIS struggles beyond a certain size)
- **Sentinel-2, Landsat, Planet, Maxar** ingested on a regular cadence
- **Temporal** (or Restate) for durable execution of multi-decade tree lifecycles — cron jobs do not survive the timescales involved

**Interpretation layer**

- **Neo4j** (or an RDF-based store, if interop with broader scientific knowledge graphs is prioritized) for the knowledge graph
- Versioned content store with citation graph
- Federated authoring with proposal-and-review protocol

The two layers share an identity model (every parcel, species, and recipe has a stable URI), share access controls, and expose a unified query surface to consumers. Storage backends differ; the consumer-facing model is one.

### 5.2 A3 Agro As API

- **PostgreSQL** with event sourcing for land-rights provenance (immutable history, audit-ready)
- **OpenAPI + AsyncAPI** specifications — the public API is the product
- Signed attestations and append-only ledgers for cryptographic integrity, in lieu of blockchain (which adds operational overhead without proportionate benefit at this stage)

### 5.3 OpenFactory

- **ROS 2** for robot control
- **Open-RMF** for fleet coordination across heterogeneous robots
- **MQTT / Sparkplug-B** for telemetry (via United Manufacturing Hub — see §6)
- **ONNX Runtime** at the edge for perception without network dependency
- **ERPNext** as the ERP system of record
- **Custom Frappe MES app** for work-order, BOM, and biological-batch modeling
- **United Manufacturing Hub (UMH)** for shop-floor reality and unified namespace

### 5.4 Cross-Cutting

- **Kafka or Redpanda** as the event spine between platforms
- **Kubernetes** with **GitOps** for multi-region deployment
- **OIDC / SPIFFE** for identity across services and federation members
- **OpenTelemetry** for observability

---

## 6. Manufacturing Stack Decision

### 6.1 Context

Robotanica needs MES-class functionality for two distinct manufacturing domains:

1. **Mechanical** — robot fabrication and component production. Classical discrete manufacturing.
2. **Biological** — seedlings, mycorrhizal inoculant, biochar, companion species. Closer in shape to pharma batch production or agtech than to discrete manufacturing.

The ERP layer is **ERPNext**. The shop-floor and telemetry layer is **United Manufacturing Hub**. The decision concerns what sits between them.

### 6.2 Decision

**ERPNext + a custom Robotanica MES app on the Frappe framework + UMH for telemetry.**

Qcadoo MES, while a mature open-source MES, was evaluated and rejected for this architecture. Qcadoo was designed for a pre-Unified-Namespace world in which the MES is the source of truth for shop-floor state. UMH already occupies that layer, leading to architectural collision: qcadoo's data model and operator screens overlap with UMH's responsibilities, while requiring three pairwise integrations (ERPNext ↔ qcadoo, qcadoo ↔ UMH, UMH ↔ ERPNext) and introducing a third runtime (Java/Spring) alongside Python (ERPNext) and the UMH toolchain. AGPL licensing further complicates federated deployment under A3.

### 6.3 Architecture

**UMH** owns:
- Machine connectivity (OPC-UA, MQTT, Sparkplug-B)
- The Unified Namespace as canonical event spine
- Time-series storage (TimescaleDB) and dashboards (Grafana)
- Greenhouse environmental telemetry (a happy reuse of the same stack)

**ERPNext + Frappe MES app** owns:
- Work orders, BOMs, job cards, workstations, quality control
- Custom doctypes for Robotanica-specific concepts: `ProductionRun`, `BiologicalBatch`, `Cohort`, `GeneticLineage`, `EnvironmentEpisode`, `RobotAssemblyRecord`
- Genealogy and traceability across both mechanical and biological domains
- Costing, accounting, supplier and customer integration

**Bridge service** (Python, ~one engineer-month for v1):
- Subscribes to UNS topics, translates events into Frappe doctype updates via REST
- Publishes ERPNext state changes (work order release, BOM revision, quality hold) back to UNS
- Propagates batch and work-order IDs through the MQTT topic hierarchy as correlation keys

### 6.4 Reference Material

The qcadoo source code remains valuable as reading material — its data model encodes 15+ years of MES domain knowledge, particularly around production routings ("technologies") and material genealogy. Robotanica's Frappe MES app draws on these patterns without adopting the runtime.

---

## 7. Agent Architecture

Agents are organized in three tiers by stakes and reversibility. There is no monolithic agent; there are many narrow agents with explicit handoffs, and every agent action is logged to Gaia so that today's agents create the dataset that improves their successors.

### 7.1 Tier 1 — Advisory

*Low stakes; human reviews every output.*

- Site-selection drafts
- Species and recipe recommendations (grounded in Gaia)
- Anomaly summaries from satellite imagery
- Contract drafting on A3
- Scientific literature synthesis

LLMs with retrieval-augmented generation against Gaia.

### 7.2 Tier 2 — Supervised Actuation

*Medium stakes; human approves before action.*

- Robot fleet scheduling
- Supply ordering
- Maintenance dispatch
- Multi-site coordination

Constrained to tool use; no freeform reasoning in the action path.

### 7.3 Tier 3 — Autonomous Operations

*Low stakes per action, high frequency.*

- Per-plant watering decisions
- Weed identification and removal
- Continuous monitoring loops
- Edge perception on field robots

Small specialized models (vision, classification), not LLMs. Run at the edge where possible.

### 7.4 Evaluation

Agent evaluations are tied to ecological outcomes (survival rate, biodiversity index, soil carbon trajectory), not to agent-internal metrics like "task completed." Evaluation cycles run against historical Gaia data with known outcomes — the question is whether the agent would have made the right call in a past situation whose result is now known.

### 7.5 Prompt and Recipe Discipline

Agent prompts encode the long-horizon mindset directly: *optimize for survival to year 30, not seedlings planted this quarter*. Recommendations require grounding in Gaia queries before generation; ungrounded outputs are rejected at the orchestration layer.

---

## 8. Governance Layer

Robotanica's hardest problem is not technical. The project proposes to operate land it does not own, on timescales that exceed any government's planning horizon, with returns accruing to people not yet born. The governance layer must therefore be designed with at least the rigor of the technical layer.

### 8.1 The Multi-Decade Biosphere Lease

A novel legal-financial instrument is required: a long-duration agreement under which a landowner commits land to ecological restoration, with transparent accounting of ecological state via Gaia, graduated obligations enforceable in local jurisdictions, and mechanisms for inheritance, transfer, and dissolution.

This instrument is the actual product of A3. The robots and platforms are downstream of getting it right.

### 8.2 Nested Governance

Following Ostrom's eighth principle, governance is nested:

- **Local** — site stewards make day-to-day decisions within site recipes
- **Regional** — coordinates across sites within a bioregion, adapts recipes to local conditions
- **Global** — sets protocol, approves new recipe templates, manages cross-bioregion learning

The Science Council and Stewardship Office sit at the global layer with explicit veto authority.

### 8.3 Indigenous and Local Recognition

Many of the highest-leverage restoration sites are subject to indigenous land rights and traditional ecological knowledge. The protocol recognizes these as first-class — not as a compliance overlay but as a structural commitment. Recipes co-developed with traditional stewards are first-class entries in Gaia's interpretation layer.

---

## 9. Roadmap (Indicative)

| Phase | Focus | Exit criteria |
|---|---|---|
| 0 | Founding instruments | Multi-decade lease drafted; Science Council seated; Gaia interpretation layer v0 |
| 1 | Platform v1 | Gaia observation layer ingesting satellite + sensor data for pilot sites; A3 protocol v1; OpenFactory operating one greenhouse |
| 2 | Federation | First external operators on A3; first external recipe contributors to Gaia; agent Tier 1 in production |
| 3 | Scaling | Multi-region deployment; agent Tier 2 with supervised actuation; biological MES fully integrated |
| 4 | Autonomy | Tier 3 agents operating at scale; survival data from earliest cohorts feeding back into recipe revisions |

The OKR's true horizon is measured in decades. Phase numbering should not be confused with quarters.

---

## 10. Open Questions

These are known unresolved questions where decisions will have outsized downstream impact:

- **Lease enforceability.** The multi-decade lease has no settled legal precedent at scale. A jurisdiction-by-jurisdiction strategy is required, and the protocol must accommodate variation.
- **Genetic strategy.** Native provenance versus assisted migration in the face of climate change is contested ecology. Gaia must support both positions and track outcomes by strategy.
- **Funding model.** Carbon markets are insufficient and partly compromised. Ecosystem service payments, biodiversity credits, sovereign biosphere bonds, and patient capital all play roles. The mix is unsettled.
- **Robot autonomy in protected areas.** Many target sites are or border protected ecosystems with restrictions on machinery. The fleet design must accommodate low-impact, animal-mimicking, or seasonal operations.
- **Failure protocol.** When a site fails (mortality > threshold, contamination event, regulatory change), what happens to the lease, the operator, the carbon claim, and the recipe entry in Gaia? The protocol must specify this from day one.

---

## Appendix A — Reading List

**Governance and commons**
- Elinor Ostrom, *Governing the Commons: The Evolution of Institutions for Collective Action* (1990)
- Ostrom, "Beyond Markets and States" (2009 Nobel lecture)

**Restoration ecology and practice**
- Akira Miyawaki and Elgene O. Box, *The Healing Power of Forests* (2007)
- Allan Savory and Jody Butterfield, *Holistic Management: A Commonsense Revolution to Restore Our Environment* (3rd ed., 2016)
- Tony Rinaudo, *The Forest Underground* (on Farmer Managed Natural Regeneration in the Sahel)
- Judith D. Schwartz, *Cows Save the Planet* and *Water in Plain Sight*
- John D. Liu, *Green Gold* and *Hope in a Changing Climate* (documentaries)

**Systems thinking**
- Donella Meadows, *Thinking in Systems*
- Stewart Brand, *The Clock of the Long Now*
- Stafford Beer, *Brain of the Firm* (Viable System Model)

**Architecture and engineering**
- Martin Kleppmann, *Designing Data-Intensive Applications*
- ISA-95 standard (manufacturing systems hierarchy)
- Unified Namespace pattern (UMH documentation)

---

## Appendix B — Glossary

- **A3** — Agro As API. The land-rights and service-coordination platform.
- **AGPL** — Affero General Public License. A copyleft license with a network-use clause.
- **BOM** — Bill of Materials.
- **Codex** — The interpretation layer of Gaia: the knowledge graph of species, ecosystems, recipes, and outcomes.
- **FMNR** — Farmer Managed Natural Regeneration. A low-tech restoration technique pioneered by Tony Rinaudo.
- **Gaia** — Robotanica's epistemic platform, comprising the observation layer (the twin) and the interpretation layer (the codex).
- **Holobiont** — A host organism considered together with its microbiota and symbionts as a unit of biological organization.
- **MES** — Manufacturing Execution System. The software layer between ERP and shop floor.
- **Miyawaki method** — A dense, native, multi-species reforestation technique developed by Akira Miyawaki.
- **OpenFactory** — Robotanica's manufacturing and fleet platform.
- **STAC** — SpatioTemporal Asset Catalog.
- **Twin** — The observation layer of Gaia: the spatial, temporal, and remote-sensing record of the biosphere under stewardship.
- **UMH** — United Manufacturing Hub. An open-source stack for shop-floor data and unified namespace.
- **UNS** — Unified Namespace. An architectural pattern in which a single canonical event/state model is published to all subscribers.
- **VSM** — Viable System Model. Stafford Beer's framework for organizational cybernetics.

---

*Robotanica is a long-horizon project. This document is a snapshot of v0.2 thinking and is expected to evolve substantially as platforms and partnerships mature.*
