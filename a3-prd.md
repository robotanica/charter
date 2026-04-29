# A3 — Agro As API

## Product Requirements Document

**System:** A3, the governance and coordination platform of Robotanica
**Version:** 0.1
**Status:** Draft for review
**Companion documents:** Robotanica Charter, Stewardship Lease Requirements Specification, Gaia PRD

---

## 1. Overview

A3 is Robotanica's platform of land governance and service coordination. It is the system in which:

- Landowners commit land under stewardship leases.
- Operators (federation members) offer planting, tending, and monitoring services.
- Recipes from Gaia are selected, bound to parcels, and executed under contract.
- Compensation flows between Landowners, Operators, communities, and the Federation.
- Credits (carbon, biodiversity, ecosystem service) are issued, held, transferred, and reconciled.
- Disputes are surfaced, mediated, and resolved.
- Governance decisions are recorded, including those of the Science Council and the Stewardship Office.

A3 is "Agro As API" because it exposes land rights, services, and governance as programmable interfaces. The Federation is the consumer; the Landowner is the beneficiary; the Charter is the constraint.

A3 is not a blockchain. It is an append-only event ledger over PostgreSQL with cryptographic provenance, sovereign-aware partitioning, and integration with external legal and registry systems. Where blockchain semantics are required (third-party verification of credit issuance, for example), they are layered on top of A3 rather than embedded in it.

---

## 2. Problem Statement

Robotanica's mission requires coordinating, over decades, across:

- **Many parties** — landowners, operators, communities, scientists, funders, regulators, certifiers.
- **Many jurisdictions** — each with its own property law, consent requirements, tax treatment, and dispute forums.
- **Many recipes** — drawn from Gaia, instantiated against specific parcels under specific conditions.
- **Many compensation arrangements** — lease payments, revenue shares, in-kind benefits, community benefits, credit revenues.
- **A long horizon** — fifty years and more per lease, with operators, recipes, and conditions changing within the term.

No existing platform handles this combination. Marketplace platforms handle coordination at scale but not multi-decade obligations. Contract-management platforms handle obligations but not marketplace coordination. Registry platforms handle records of state but not active brokering. Carbon-project platforms handle credits but not the full ecological-stewardship lifecycle. Land-trust software handles conservation easements but not federated operation.

A3 is built to integrate these capabilities under the discipline of the Charter and the Stewardship Lease.

---

## 3. Goals and Non-Goals

### 3.1 Goals

- Operationalize the Stewardship Lease as a living instrument: register, execute, monitor, amend, and (when necessary) terminate.
- Provide a marketplace through which Landowners and Operators discover each other and contract for services.
- Embed Ostrom's eight design principles as enforced constraints on the protocol.
- Enable federation membership: admit Operators and partner organizations under defined terms; support sovereignty across regions and indigenous communities.
- Issue, track, and reconcile credits (carbon, biodiversity, ecosystem service) honestly, without overissuance.
- Provide auditable, public-record-compatible governance: every decision of consequence is recorded, attributable, and reproducible.
- Operate across jurisdictions, with jurisdiction-specific lease variants and dispute forums.
- Maintain queryable, signed event history for the lifetime of every lease (50+ years).
- Be open-source and built on open-source components.

### 3.2 Non-Goals

- A3 is not the source of ecological state — that is Gaia.
- A3 is not the source of operational telemetry — that is OpenFactory.
- A3 is not a public land registry — it integrates with public registries where they exist; it does not replace them.
- A3 is not a banking or payment processor — it integrates with payment rails; it does not become one.
- A3 is not a blockchain or token platform — it is an append-only ledger with cryptographic provenance. Tokenization, where required for external credit markets, is layered on top.
- A3 does not draft legal instruments — that is the work of jurisdictional counsel, informed by the Lease Requirements Specification.
- A3 does not adjudicate disputes — it routes them to the appropriate forum (mediation, arbitration, indigenous customary process) and records outcomes.

---

## 4. Users and Personas

| Persona | Primary interaction | Concerns |
|---|---|---|
| Landowner | Submits land; reviews offers; signs leases; reads parcel state; receives compensation | Comprehensibility, trust, fair terms, withdrawal rights |
| Indigenous community representative | Provides FPIC; co-authors recipes; controls data access; receives benefit-sharing | Sovereignty, control, deference to customary process |
| Operator (federation member) | Offers services; bids on contracts; executes work; reports outcomes | Clear contracts, predictable revenue, fair dispatch |
| Stewardship Office officer | Holds leases as Federation counterparty; manages relationships; oversees succession | Long-horizon view, structural protection from short-term pressure |
| Science Council member | Reviews recipe instantiations; exercises veto authority; reviews dispute escalations | Independence, evidence access, time to deliberate |
| Auditor / certifier | Verifies credit issuance; audits compliance; signs attestations | Provenance chains, immutability, reproducibility |
| Regulator | Reviews jurisdiction-specific compliance; receives required disclosures | Jurisdictional accuracy, lawful structure |
| Funder | Reviews aggregate outcomes; provides capital; reviews use of funds | Transparency, mission alignment, structural protections |
| Public | Reads public record; surfaces concerns | Comprehensibility, access, ability to flag issues |
| **System actors** | | |
| Gaia | Provides recipes and parcel state; receives lease and contract events | Stable contract, low latency |
| OpenFactory | Receives operational dispatch; reports operations | Stable contract, durable writes |
| Agent (Tier 1) | Drafts contracts; surfaces matches; reviews proposals | RAG access, structured outputs, citation chains |
| Agent (Tier 2) | Proposes dispatch; flags anomalies | Strong typing, audit trail, human review |

---

## 5. Core Concepts and Domain Model

### 5.1 Primary Entities

- **Parcel** — A unit of land under stewardship. Reference to Gaia parcel URI; A3 holds the rights and lease state, Gaia holds the spatial and ecological state.
- **Party** — A Landowner, Operator, Community, Funder, or other entity in the Federation. Has a stable URI and a signing key.
- **Lease** — An instance of a Stewardship Lease over a Parcel, between a Landowner, an Operator, and the Federation. Includes the jurisdictional variant, the recipe binding, the compensation structure, and the term.
- **LeaseEvent** — An immutable record of any event in the lifecycle of a Lease: signing, amendment, recipe update, recipe-instance creation, monitoring report, breach notice, cure, succession, termination.
- **Consent** — A first-class record of FPIC or other consent, signed by the consenting party, with full provenance. Required for lease formation where applicable.
- **Service** — An offering by an Operator: planting, tending, monitoring, restoration consultation, etc. Typed and priced.
- **ServiceContract** — A specific contract for a Service, executed under a Lease, between a Landowner and an Operator.
- **CompensationFlow** — A defined flow of value between Parties under a Lease or ServiceContract: lease payment, revenue share, in-kind benefit, community benefit.
- **Credit** — A unit of restoration outcome (tonne CO₂ equivalent, biodiversity credit, ecosystem service credit) issued against a Parcel under a Lease. Has issuer, holder, vintage, and reconciliation state.
- **Reconciliation** — A correction event: voiding credits that did not occur, making whole credits affected by site failure.
- **DisputeCase** — A formal dispute between Parties, with state machine, escalation history, and resolution record.
- **AmendmentProposal** — A proposed amendment to a Lease, with state machine through the consent process.
- **GovernanceDecision** — A first-class record of decisions by the Science Council, Stewardship Office, regional governance, or Federation-wide governance.

### 5.2 Identity and Provenance

Every entity has a stable URI of the form:

```
a3://<type>/<region>/<id>[@<version>]
```

Every event is signed by the principal that authored it (Party signing key, service identity, or governance body key). Signatures are verifiable independently of A3's runtime — the signed event log is a self-contained record.

### 5.3 The Lease as a State Machine

Leases are state machines with states including: `proposed`, `consent-pending`, `signed`, `active`, `under-amendment`, `breach-notice`, `cure-period`, `under-mediation`, `under-arbitration`, `succession-pending`, `terminated`, `closed-out`.

State transitions are events. Every transition records the actor, the cause, and the resulting state. The full history is replayable.

### 5.4 Recipe Binding

A Lease binds to a Recipe at a specific Gaia version. The recipe URI is recorded in the Lease. When the recipe is updated in Gaia, the Lease does not automatically follow; recipe updates within a Lease are a structured form of amendment, requiring consent under the Lease Requirements Specification §11.3.

### 5.5 Credit Lifecycle

Credits move through states: `pending` (work performed but not yet verified), `issued` (verified and assigned to a holder), `transferred` (sold or moved to another holder), `retired` (claimed against an emission or biodiversity loss), `reconciled` (voided or made whole due to site change).

The credit lifecycle is auditable end-to-end: every credit can be traced to the Parcel, the Lease, the recipe instance, the verification event, and the underlying observations in Gaia.

---

## 6. Functional Requirements

Each requirement has an ID. Priority levels: **MUST**, **SHOULD**, **MAY**.

### 6.1 Land Submission and Lease Formation

- **A3-L-001 (MUST)** Allow Landowners to submit Parcels for stewardship, with title verification and disclosure of historical use, contamination, water rights, and existing easements.
- **A3-L-002 (MUST)** Verify title or equivalent rights through integration with public registries where available, and through documentary evidence where not.
- **A3-L-003 (MUST)** Detect and require disclosure of indigenous, customary, or community claims affecting the Parcel; require FPIC processes before lease formation in such cases.
- **A3-L-004 (MUST)** Support proposal-and-review of candidate Recipes for the Parcel, drawing from Gaia and informed by parcel conditions.
- **A3-L-005 (MUST)** Generate jurisdiction-specific Lease drafts from the Stewardship Lease Requirements and the chosen jurisdictional variant, with parameters bound (parties, parcel, recipe, compensation, term).
- **A3-L-006 (MUST)** Capture all required signatures and consents, including FPIC where applicable, with cryptographic provenance and timestamp.
- **A3-L-007 (MUST)** Register the Lease in the appropriate public registry where one exists (land registry, conservation easement registry, or A3's own registry where no public registry applies).

### 6.2 Lease Lifecycle Management

- **A3-L-010 (MUST)** Maintain Lease state machines per §5.3, with all transitions recorded as immutable LeaseEvents.
- **A3-L-011 (MUST)** Enforce term boundaries: prevent expired Leases from being treated as active; surface upcoming renewals or expirations within defined windows.
- **A3-L-012 (MUST)** Support Lease amendment with the consent processes specified in the Lease Requirements §11.
- **A3-L-013 (MUST)** Support Lease termination with the procedures specified in the Lease Requirements §6, including buyout, succession, and dissolution flows.
- **A3-L-014 (MUST)** Prevent abandonment: a Lease cannot transition to terminated without explicit closeout, including data delivery to the Landowner per the Lease Requirements §8.4.
- **A3-L-015 (SHOULD)** Surface Leases at risk of breach (missed monitoring, missed payments, recipe deviation reported by Gaia) before they become formal breaches.

### 6.3 Marketplace and Operator Coordination

- **A3-M-001 (MUST)** Allow Operators to register as federation members under the Federation Membership Agreement; verify their credentials and competencies.
- **A3-M-002 (MUST)** Allow Operators to publish Service offerings with type, region, capacity, and pricing.
- **A3-M-003 (MUST)** Match Service requests under Leases to Operator offerings, considering region, capacity, recipe expertise, and Landowner preferences.
- **A3-M-004 (MUST)** Support Landowner consent over Operator selection (per Lease Requirements §6.5 succession rights and §3.1 Landowner agency).
- **A3-M-005 (MUST)** Maintain ServiceContract state through proposal, acceptance, execution, completion, dispute, or termination.
- **A3-M-006 (SHOULD)** Surface Operator performance history (completion rates, outcome quality, dispute rates) to inform matching.
- **A3-M-007 (MUST)** Prevent dispatch to suspended or expelled Operators.
- **A3-M-008 (SHOULD)** Support cross-Operator coordination for parcels requiring multiple service types or capacities.

### 6.4 Consent and Sovereignty

- **A3-C-001 (MUST)** Implement FPIC as a structural workflow: information disclosure, consultation period, decision recording, with no shortcuts for operational urgency.
- **A3-C-002 (MUST)** Support indigenous community governance forms: consent decisions may be made by the community through their own governance processes, recorded in A3 by an authorized representative.
- **A3-C-003 (MUST)** Support consent revocation: where the underlying conditions of consent change materially, parties may revoke consent under defined processes; revocation triggers Lease review.
- **A3-C-004 (MUST)** Apply CARE Principles to data generated about indigenous and community parcels: collection, access, publication, and retention are subject to community decision.
- **A3-C-005 (MUST)** Support multilingual consent documents and processes; consent given in a language other than the legal language of the lease must be supported by translation provenance.

### 6.5 Compensation and Benefit-Sharing

- **A3-F-001 (MUST)** Support all compensation forms specified in the Lease Requirements §9: lease payments, revenue shares, in-kind compensation, community benefits.
- **A3-F-002 (MUST)** Schedule and track compensation flows; integrate with payment processors for execution; record completion.
- **A3-F-003 (MUST)** Compute revenue shares automatically from credit revenues, harvest revenues, and ecosystem service payments per the Lease's defined shares.
- **A3-F-004 (MUST)** Maintain transparency of compensation flows in summary form in the public record per Lease Requirements §9.4, with PII protected.
- **A3-F-005 (MUST)** Prevent flows that violate the "no free land" provision (Lease Requirements §9.2): reject Lease drafts where Landowner compensation is materially absent.
- **A3-F-006 (SHOULD)** Support multi-currency compensation; track exchange events transparently.

### 6.6 Credit Issuance and Reconciliation

- **A3-K-001 (MUST)** Issue credits only on the basis of verified outcomes recorded in Gaia; refuse issuance for unverified or projected outcomes.
- **A3-K-002 (MUST)** Maintain credit registries with full provenance: parcel, lease, recipe instance, verification event, holder, vintage, transfer history.
- **A3-K-003 (MUST)** Support credit transfer between holders, with full provenance preservation.
- **A3-K-004 (MUST)** Support credit retirement (claim against an emission or biodiversity loss); retired credits cannot be re-issued.
- **A3-K-005 (MUST)** Implement reconciliation: when a site fails or a recipe is found to have produced fewer outcomes than claimed, affected credits are voided or made whole through Federation reserves; reconciliation is recorded immutably.
- **A3-K-006 (MUST)** Refuse over-issuance: a parcel cannot issue more credits than its verified outcomes support.
- **A3-K-007 (SHOULD)** Integrate with external credit registries (Verra, Gold Standard, Plan Vivo, biodiversity credit registries) where required for market participation; integration must preserve A3's source-of-truth status.

### 6.7 Governance and Decisions

- **A3-G-001 (MUST)** Record GovernanceDecisions as first-class entities, with the question, options considered, decision, rationale, parties involved, and timestamp.
- **A3-G-002 (MUST)** Support Science Council veto authority over recipe approvals and recipe instance applications; Council decisions are recorded with rationale.
- **A3-G-003 (MUST)** Support Stewardship Office authority over Lease succession, dissolution, and structural amendment.
- **A3-G-004 (MUST)** Support nested governance per Charter §4.5: local site decisions, regional coordination, global protocol; decisions at higher layers do not silently override decisions at lower layers.
- **A3-G-005 (MUST)** Maintain the Federation Membership registry: admission, suspension, expulsion, withdrawal events recorded immutably.
- **A3-G-006 (SHOULD)** Surface governance metrics (decision volumes, decision latency, appeal rates, veto rates) for review.

### 6.8 Dispute Resolution

- **A3-D-001 (MUST)** Allow any Party to a Lease or ServiceContract to open a DisputeCase, with stated cause and supporting evidence.
- **A3-D-002 (MUST)** Route disputes through the levels specified in the Lease Requirements §12: direct, mediation, arbitration, jurisdictional courts, indigenous forums.
- **A3-D-003 (MUST)** Support indigenous customary dispute forums where the Indigenous Party invokes them; A3 records but does not adjudicate.
- **A3-D-004 (MUST)** Maintain DisputeCase state machines with evidence, communications, mediator/arbitrator decisions, and resolution.
- **A3-D-005 (MUST)** Record Dispute outcomes; support enforcement of arbitration awards through integration with relevant legal systems where applicable.
- **A3-D-006 (MUST)** Protect Parties from retaliation: a Party in dispute is not subject to discriminatory dispatch, suspension, or other adverse action during the dispute, except for cause unrelated to the dispute itself.

### 6.9 Audit Trail and Public Record

- **A3-A-001 (MUST)** Make every event in A3 immutable and cryptographically signed.
- **A3-A-002 (MUST)** Support point-in-time queries: the state of any Lease, Party, or Credit at any past timestamp is reconstructible from the event log.
- **A3-A-003 (MUST)** Publish a public record containing: aggregate Lease counts and outcomes, federation membership, governance decisions, recipe revisions, dispute outcomes, credit issuance and reconciliation summaries.
- **A3-A-004 (MUST)** Coarsen the public record per Charter privacy commitments and Lease Requirements §8: precise locations of vulnerable sites are obscured; PII is removed.
- **A3-A-005 (MUST)** Support auditor and regulator access at higher granularity than public, under defined credentials.
- **A3-A-006 (MUST)** Support data portability: Landowners and (where applicable) communities receive complete data exports on request and on Lease termination.

### 6.10 Federation Operation

- **A3-X-001 (MUST)** Support multi-tenant operation: federation members operate within their scope, with strong isolation.
- **A3-X-002 (MUST)** Support regional sovereignty: Lease and Party data default to storage in the relevant jurisdiction.
- **A3-X-003 (MUST)** Support partition-tolerant operation: a region can operate locally during loss of connectivity to other regions; rejoin reconciles via append-only logs.
- **A3-X-004 (SHOULD)** Support forking per Charter §5.4: a community or region may take A3's protocol and code and operate independently; A3's data export and protocol publication enable this.

---

## 7. Non-Functional Requirements

### 7.1 Scale

- **A3-N-001** Support 10⁶ active Leases at full deployment (corresponding to 10⁶ Parcels at scale).
- **A3-N-002** Support 10⁷ ServiceContracts per year at peak.
- **A3-N-003** Support 10⁸ events per year across the system.
- **A3-N-004** Support 10⁵ federation members.

A3's scale is much smaller than Gaia's by entity count, but every entity is legally consequential. The constraint is durability and integrity, not throughput.

### 7.2 Performance

- **A3-N-010** P95 latency for Lease state queries: < 200 ms.
- **A3-N-011** P95 latency for marketplace match queries: < 500 ms.
- **A3-N-012** P95 latency for credit registry queries: < 200 ms.
- **A3-N-013** P95 latency for governance decision recording (write): < 1 s.
- **A3-N-014** Public record updates: published within 1 hour of source event.

### 7.3 Durability and Integrity

- **A3-N-020** All events are append-only, cryptographically signed by the writing principal, and chained (each event references the hash of the prior event in its scope).
- **A3-N-021** Replication across at least three regions; loss tolerance is zero for any committed event.
- **A3-N-022** Event logs are exportable in open formats and verifiable independently of A3 runtime.
- **A3-N-023** Schema evolution preserves the ability to interpret prior events; no migration drops data semantics.
- **A3-N-024** Cryptographic algorithms used for signing are agile: the system supports rotation as cryptographic standards evolve over the 50+ year horizon.

### 7.4 Multi-Decade Operability

- **A3-N-030** Every Lease, Party, Credit, and DisputeCase is queryable at any future date for the full Lease term plus an archival period of at least 50 years post-term.
- **A3-N-031** All persistent state has a documented migration path; any component must be replaceable without data loss or interpretation loss.
- **A3-N-032** Identifiers are stable URIs; no identifier is ever reused.

### 7.5 Sovereignty and Jurisdiction

- **A3-N-040** Multi-tenant from day one with strong isolation between tenants.
- **A3-N-041** Regional data residency: Lease data defaults to storage in the parcel's jurisdiction; cross-region replication is policy-controlled and consent-bound for indigenous parcels.
- **A3-N-042** Indigenous data sovereignty: where applicable, data flows respect community policy and may exclude public APIs and external federation.
- **A3-N-043** Federation members may mirror their scope locally and operate during partition.
- **A3-N-044** Jurisdiction-specific lease variants are versioned independently per jurisdiction; updates in one variant do not propagate to others without explicit re-adoption.

### 7.6 Security

- **A3-N-050** All API access is authenticated (OIDC) and authorized (attribute-based, with parcel and lease scope).
- **A3-N-051** Service-to-service identity is SPIFFE-based.
- **A3-N-052** All write events are cryptographically signed by the writing principal; signature verification is part of the durability guarantee.
- **A3-N-053** Sensitive parcel locations are coarsened in public APIs.
- **A3-N-054** PII handling follows least-privilege; benefits are visible to recipients and their authorized representatives, not to the public.
- **A3-N-055** Compromise detection: anomalous signing patterns, unauthorized API access, and key compromise events are monitored and alerted.

### 7.7 Transparency

- **A3-N-060** All governance decisions are public unless they touch protected categories (PII, sensitive locations, indigenous data sovereignty).
- **A3-N-061** Aggregate Lease and Credit metrics are published continuously.
- **A3-N-062** Federation membership changes are public.
- **A3-N-063** Recipe revisions affecting active Leases are notified to affected parties within defined SLAs.

### 7.8 Observability

- **A3-N-070** All services emit OpenTelemetry traces, metrics, and logs.
- **A3-N-071** Lease lifecycle metrics, marketplace activity, and governance latency have dedicated dashboards.
- **A3-N-072** Every agent and human action is logged for evaluation and audit.

---

## 8. Architecture

### 8.1 Component Overview

```
                  ┌────────────────────────────────────────────────┐
                  │                   A3 API Surface               │
                  │ REST · GraphQL · Events Out · Public Registry  │
                  └────────────────────────────────────────────────┘
                            ▲              ▲              ▲
                            │              │              │
       ┌────────────────────┴───┐  ┌───────┴────────┐  ┌──┴─────────────────┐
       │  Lease & Lifecycle     │  │  Marketplace   │  │  Credit Registry   │
       │  (signing, amendment,  │  │  (services,    │  │  (issuance,        │
       │   succession, term)    │  │   matching)    │  │   reconciliation)  │
       └────────────────────────┘  └────────────────┘  └────────────────────┘
                            ▲              ▲              ▲
                            │              │              │
       ┌────────────────────┴──┐  ┌────────┴────────┐  ┌──┴────────────────┐
       │  Governance & Council  │  │  Disputes &     │  │  Compensation &   │
       │  (decisions, vetoes,   │  │  Mediation      │  │  Benefit-Sharing  │
       │   nested governance)   │  │                 │  │                   │
       └────────────────────────┘  └─────────────────┘  └───────────────────┘
                                          │
                            ┌─────────────┴───────────────┐
                            ▼                             ▼
              ┌──────────────────────┐       ┌──────────────────────────┐
              │   Event Ledger       │       │  Integration Edge        │
              │   PostgreSQL +       │       │  (Gaia, OpenFactory,     │
              │   signed event chain │       │   public registries,     │
              │                      │       │   payment rails,         │
              └──────────────────────┘       │   external credit regs)  │
                                             └──────────────────────────┘
                            │                             │
                            └──────┬──────────────────────┘
                                   ▼
                       ┌────────────────────────┐
                       │  Identity & Policy     │
                       │  OIDC · SPIFFE         │
                       │  Sovereign partitions  │
                       └────────────────────────┘
                                   │
                                   ▼
                       ┌────────────────────────┐
                       │  Durable Workflows     │
                       │  (Temporal)            │
                       │  Multi-decade leases   │
                       └────────────────────────┘
```

### 8.2 Storage Layout

- **PostgreSQL** with event sourcing — the canonical store. Append-only event tables; materialized views for state. All events are signed and chained.
- **Object storage** — long-term archival of signed event logs in open formats for independent verification.
- **Document store** — versioned storage of Lease documents (jurisdictional variants), consent documents, and governance decision documents.
- **Search index** — for marketplace and registry queries; rebuildable from the event log.

### 8.3 Cryptographic Provenance

Every Party has a signing key. Every event records its author's signature over a canonical serialization of the event content plus the prior event hash. The event log is independently verifiable: given a snapshot, any third party can verify integrity without trusting A3's runtime.

Key rotation is supported via key-history records signed by prior keys.

### 8.4 Sovereign Partitions

A3 is partitioned by sovereign region. Each region's data is stored within its jurisdiction by default. Cross-region replication is policy-controlled. Indigenous parcels operate as their own sovereign partition with community-controlled access.

The event log is partitioned, but the Federation-wide governance log spans all partitions for cross-region governance decisions.

### 8.5 Durable Workflows

Temporal hosts long-running workflows for: Lease term tracking, scheduled monitoring obligations, scheduled compensation flows, scheduled credit reconciliation, multi-step amendment and dispute processes. These workflows may run for years; they are checkpoint-restartable across deployments.

### 8.6 Event Bus

Kafka or Redpanda carries events to and from A3:

- **In:** Gaia outcome events (informing credit issuance), OpenFactory operation events (informing service contract completion), payment confirmations.
- **Out:** Lease lifecycle events, governance decisions, credit issuance/transfer/retirement, dispute openings/closings.

Schemas are versioned (AsyncAPI). Consumers declare schema compatibility at subscription time.

### 8.7 Integration with External Systems

- **Public land registries** — where they exist and accept the Lease as a recordable instrument.
- **Payment rails** — for compensation flows; A3 records the obligation and the confirmation, not the funds in transit.
- **External credit registries** — for credits that participate in regulated markets; A3 remains the source of truth.
- **Legal and arbitration systems** — for dispute escalation; A3 records but does not adjudicate.

---

## 9. APIs

### 9.1 External API Surface

- **REST** for CRUD-style access to Parcels, Parties, Leases, Services, ServiceContracts, Credits, DisputeCases, GovernanceDecisions.
- **GraphQL** for federated reads composing across entities.
- **Event subscriptions** on Kafka topics: `a3.lease.lifecycle`, `a3.service-contract.lifecycle`, `a3.credit.lifecycle`, `a3.governance.decision`, `a3.dispute.lifecycle`, `a3.federation.membership`.
- **Public registry** read-only endpoints for the public record.

### 9.2 Specifications

- All synchronous APIs specified in **OpenAPI 3.1**.
- All event APIs specified in **AsyncAPI 2.x**.
- All entity schemas specified in **JSON Schema** with stable `$id` URIs.
- Specifications are the contract; implementations are conformance-tested.

### 9.3 SDKs

Python and TypeScript SDKs are first-class. Other languages follow demand. SDKs are generated from specifications.

### 9.4 Lease as API

Every Lease exposes a programmatic interface: query state, request amendment, raise dispute, report monitoring, close out. The interface is uniform across jurisdictional variants; jurisdiction-specific differences are reflected in document content, not API shape.

---

## 10. Integrations

| System | Direction | Interface | Data flowing |
|---|---|---|---|
| Gaia | Bidirectional | REST + Events | Recipes (in), parcel state (in), outcome events (in); lease references (out), recipe-instance bindings (out) |
| OpenFactory | Bidirectional | REST + Events | Service dispatch (out), operation events (in), batch genealogy (in) |
| Public land registries | Outbound where supported | Jurisdiction-specific | Lease registration |
| Payment processors | Bidirectional | REST | Payment instructions (out), confirmations (in) |
| External credit registries | Bidirectional | Registry-specific | Credit issuance, transfer, retirement |
| Legal and arbitration systems | Outbound | Document delivery + manual escalation | Dispute escalation; arbitration award recording |
| Agents (all tiers) | Bidirectional | REST + retrieval API | Reads for grounding; writes for proposals subject to human review |

---

## 11. Success Metrics

### 11.1 System Health

- API availability (P95 over rolling 30 days): > 99.9%.
- Event ledger integrity: 100% (any failure is a Sev-1 incident).
- Event publication latency (source to public record summary): < 1 hour P95.

### 11.2 Lease Lifecycle Health

- Lease formation cycle time (proposal to signed): < 90 days median (allowing FPIC time).
- Active Leases meeting monitoring obligations: > 95%.
- Amendment cycle time (proposal to decision): < 60 days median for non-material; < 180 days for material.
- Lease closeout completeness (data delivered, registries updated): 100%.

### 11.3 Marketplace Health

- ServiceContract match latency: < 14 days median from request to acceptance.
- ServiceContract completion rate: > 95% on-time-and-spec.
- Operator suspension rate: tracked, not bounded.

### 11.4 Credit Integrity

- Credits issued per verified outcome: 1.0 (no over-issuance).
- Reconciliation completeness: every site failure or recipe revision triggers reconciliation within 90 days.
- External registry reconciliation: A3 source-of-truth is preserved; no divergence between A3 and external registries.

### 11.5 Governance Health

- Science Council veto exercises: tracked, not bounded.
- Governance decision latency: < 30 days median for non-escalated decisions.
- Dispute resolution latency: < 180 days median through mediation; arbitration follows arbitration-body SLAs.

### 11.6 Mission Alignment

- Aggregate Parcels under active stewardship.
- Aggregate land area under stewardship.
- Aggregate compensation flowing to Landowners and communities.
- Aggregate credits issued, retired, reconciled.

These are reported by A3 but are OKRs of Robotanica, not A3 in isolation.

---

## 12. Phasing

| Phase | Scope | Exit criteria |
|---|---|---|
| 0 — Foundations | Identity model, URI scheme, event ledger, single-region, first jurisdictional Lease variant | First Lease signed end-to-end; first GovernanceDecision recorded |
| 1 — Pilot | Operational marketplace; first credit issuance; basic dispute support | First ServiceContract completed under a Lease; first credit issued and verified |
| 2 — Federation | Multi-tenant, multi-region; Operator membership at scale; FPIC workflows for indigenous parcels in production | First indigenous-parcel Lease executed under FPIC; first cross-region Operator dispatch |
| 3 — Markets | External credit registry integrations; sophisticated benefit-sharing; reconciliation discipline at scale | First reconciliation event executed correctly; external credit market participation |
| 4 — Multi-jurisdictional scale | Multiple jurisdictional Lease variants in production; partition-tolerant operation; succession protocols exercised | Operations across at least five jurisdictions; succession scenario tested in production |

Phase boundaries are exit criteria, not dates.

---

## 13. Risks and Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Jurisdictional variance breaks the "same instrument" abstraction | Operational complexity; legal exposure | Variants must satisfy a common requirements specification; divergences are reported and reviewed |
| Capture of governance bodies (Council, Stewardship Office) | Erosion of mission discipline | Multi-disciplinary composition mandated; veto authority structurally protected; Charter-level un-amendable provisions |
| Over-issuance of credits | Market collapse, mission discredit | Hard refusal of unverified issuance; reconciliation discipline; external auditor access |
| Cryptographic compromise over decades | Loss of integrity of historical record | Algorithm agility; key rotation discipline; archival in open formats independently verifiable |
| Capture by a single funder or jurisdiction | Loss of independence | Federation structure; sovereign partitions; forkability per Charter §5.4 |
| Operator collusion to game the marketplace | Unfair dispatch; fraud | Performance history transparent; auditor access; randomized auditing; Operator suspension and expulsion procedures |
| FPIC reduced to procedural checkbox | Violation of indigenous sovereignty | FPIC as structural workflow with mandatory community-led process; indigenous representation in governance |
| Catastrophic site loss exceeds reconciliation reserves | Credit market dysfunction; party harm | Federation-level mutual or reinsurance arrangement; explicit catastrophe protocols; conservative initial credit issuance |
| Long-term storage cost or technology obsolescence | Loss of records | Open formats; multi-region replication; periodic archival migration exercises |
| Legal challenge to the Lease as a novel instrument | Operational disruption in a jurisdiction | Conservative jurisdictional variants drafted by local counsel; fallback to known-valid instruments where necessary |

---

## 14. Open Questions

- **Public registry integration where none exists.** In jurisdictions without a registry that will record the Lease, what substitute provides defense against subsequent purchasers in good faith?
- **Cross-jurisdictional credit reconciliation.** When a parcel in one jurisdiction issues credits sold in another and a reconciliation event occurs, how are the legal and financial implications handled?
- **The ecosystem as party.** Where ecosystems have legal standing (Ecuador, parts of New Zealand), can they be represented as a party in A3? What does that look like operationally?
- **Future-generations standing.** The Charter commits to future generations, but they cannot sign or be represented directly. Is the Stewardship Office sufficient as their proxy, or is a separate guardian role required?
- **Federation governance evolution.** As the Federation grows, how are governance bodies evolved, expanded, or replaced without disrupting operations?
- **Tokenization for external markets.** External credit markets are increasingly tokenized. How does A3 expose tokens for those markets while preserving its source-of-truth status and avoiding crypto-economic capture?
- **Dispute jurisdiction for federated operators.** When an Operator in jurisdiction A serves a parcel in jurisdiction B, and a dispute arises, which forum applies? The Lease specifies this, but operational corner cases need protocols.
- **Sunset of jurisdictional variants.** When a jurisdictional variant becomes outdated (legal change, evidence of weakness), how are existing Leases under that variant migrated, if at all?

---

## Appendix A — Glossary (A3-Specific)

- **AmendmentProposal** — A proposed amendment to a Lease, with state machine through consent.
- **CARE Principles** — Collective benefit, Authority to control, Responsibility, Ethics. Indigenous data governance principles.
- **CompensationFlow** — A defined value flow between Parties under a Lease or ServiceContract.
- **Consent** — A first-class signed record, including FPIC where applicable.
- **Credit** — A unit of restoration outcome (carbon, biodiversity, ecosystem service) issued against a Parcel.
- **DisputeCase** — A formal dispute with state machine, escalation history, and resolution record.
- **Federation** — Robotanica's federation; A3's primary tenant scope.
- **FPIC** — Free, Prior, and Informed Consent. Required for Lease formation involving indigenous or local communities.
- **GovernanceDecision** — A first-class record of a decision by a governance body.
- **Lease** — An instance of the Stewardship Lease over a Parcel.
- **LeaseEvent** — An immutable record of a lifecycle event within a Lease.
- **Operator** — A federation member offering services.
- **Parcel** — A unit of land under stewardship; A3 holds rights, Gaia holds spatial state.
- **Party** — A Landowner, Operator, Community, Funder, or other entity in the Federation.
- **Reconciliation** — A correction event for credits affected by site change or recipe revision.
- **ServiceContract** — A specific contract for a Service under a Lease.
- **Stewardship Office** — Robotanica's body holding Leases on behalf of the Federation.

---

## Appendix B — Standards and References

- **OpenAPI** 3.1, **AsyncAPI** 2.x, **JSON Schema**.
- **OIDC**, **SPIFFE**.
- **CARE Principles** for indigenous data governance.
- **FPIC** as defined under UN Declaration on the Rights of Indigenous Peoples.
- **Verra**, **Gold Standard**, **Plan Vivo** for external carbon registry integration.
- **New York Convention** for international arbitration award enforcement.
- **CAA / ICC / UNCITRAL** arbitration rules as candidate options for dispute resolution.

---

*This is v0.1 of the A3 PRD. It will evolve substantially as the Stewardship Lease is drafted in jurisdictional variants and as the first pilot Leases meet operational reality.*
