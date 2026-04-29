# Robotanica Protocol Specifications

## Federation Contract (v0)

**Document type:** Normative protocol specification
**Status:** Draft for ratification
**Companion documents:** Robotanica Charter, Gaia PRD, A3 PRD, OpenFactory PRD, Stewardship Lease Requirements, MRV Specification, Threat Model

---

## 1. Purpose and Status

This document specifies the protocols by which Robotanica's platforms and federation members interoperate. It is the cross-platform federation contract.

The Charter, PRDs, MRV Specification, and Lease Requirements describe what Robotanica builds and operates. This document describes what *anyone* must implement to participate in the federation as a peer. The PRDs are descriptions of Robotanica's reference implementations; this document is the contract those implementations satisfy.

The protocol is the most stable layer of Robotanica. The Charter's commitment to forkability (§5.4) depends on the protocol being implementable independently of Robotanica's specific code, organization, or jurisdiction. The protocol must therefore be:

- **Implementation-agnostic.** The protocol does not prescribe particular software, vendors, or runtimes.
- **Testable.** Conformance must be verifiable through defined test suites.
- **Stable.** Breaking changes are exceptional and follow a defined process.
- **Open.** The protocol is published openly and may be implemented without permission or fee.

This document is a starting structure. Where the protocol is incomplete or under-specified, this is acknowledged in the open questions and in the section-level status notes.

---

## 2. Status Conventions

Each protocol section has a status:

- **Stable** — the protocol is ratified and implementations should conform.
- **Draft** — the protocol is in active design; implementations should expect change.
- **Experimental** — the protocol is exploratory and may be withdrawn.

Each requirement uses the conventions of RFC 2119: **MUST**, **SHOULD**, **MAY**, **MUST NOT**, **SHOULD NOT**.

---

## 3. Core Invariants

These invariants apply to all protocols and may not be set aside. They are derived from the Charter and operationalize its principles at the protocol layer.

### 3.1 Append-Only Provenance

**INV-001 (MUST)** All events of consequence are append-only. Implementations MUST NOT silently alter or delete prior events.

**INV-002 (MUST)** All events of consequence are cryptographically signed by the originating principal.

**INV-003 (MUST)** Implementations MUST support point-in-time queries: the state of any entity at any past timestamp must be reconstructible from the event log.

### 3.2 Stable Identity

**INV-010 (MUST)** Every entity exposed by the protocol has a stable URI that is not reused.

**INV-011 (MUST)** URIs persist across schema migrations, organizational changes, and infrastructure replacements.

### 3.3 Open Formats

**INV-020 (MUST)** All data exposed by the protocol is exposed in open formats: JSON Schema, JSON-LD, Parquet, GeoParquet, RDF, or other OSI- or W3C-recognized open standards.

**INV-021 (MUST NOT)** Implementations MUST NOT require proprietary serialization formats for protocol-level interchange.

### 3.4 Sovereignty Honor

**INV-030 (MUST)** Implementations MUST honor sovereignty declarations associated with data: regional residency, indigenous community sovereignty, sensitive-location coarsening.

**INV-031 (MUST NOT)** Implementations MUST NOT propagate data in violation of declared sovereignty controls, even when technically able.

### 3.5 Charter Conformance

**INV-040 (MUST)** Federation members MUST adhere to the Charter's commitments in the work conducted under the federation's protocols.

**INV-041 (MUST)** Where the protocol is silent and the Charter is not, the Charter governs.

### 3.6 Reconciliation Honesty

**INV-050 (MUST)** When prior claims are found to be wrong, implementations MUST reconcile honestly: void or make-whole affected credits, correct attestations, update the public record. Concealment is a violation of the protocol.

---

## 4. Identity Protocol

**Status:** Stable

### 4.1 URI Scheme

Entities are identified by URIs of the form:

```
<authority>://<type>/<region>/<id>[@<version>]
```

Where:

- `<authority>` is one of `gaia`, `a3`, `of` for the platform-specific URIs, or `robotanica` for cross-platform federation entities.
- `<type>` is the entity type (`parcel`, `lease`, `recipe`, `cohort`, `robot`, `party`, etc.).
- `<region>` is a federation-recognized region identifier; defaults to `global` for non-spatial entities.
- `<id>` is a stable identifier unique within type and region.
- `<version>` is optional and applies where the entity is versioned (recipes, codex entries).

### 4.2 Party Identity

**ID-001 (MUST)** Every Party (Landowner, Operator, Community, Funder, etc.) has a Party URI of the form `robotanica://party/<region>/<id>`.

**ID-002 (MUST)** Every Party has at least one signing public key registered with the federation; signing keys are versioned and rotatable per §4.4.

**ID-003 (MUST)** Parties acting through delegates (a community represented by elected leadership; a corporation represented by an officer) record the delegation explicitly with the delegate's signing identity and authorization scope.

### 4.4 Key Rotation

**ID-010 (MUST)** Implementations MUST support key rotation: a Party may register a new signing key, and the rotation event is signed by the prior key.

**ID-011 (MUST)** Lost or compromised keys MUST be rotatable through a defined recovery process that involves attestation by at least one other federation principal.

**ID-012 (MUST)** Cryptographic algorithms used for signing are agile: the protocol supports algorithm replacement as cryptographic standards evolve.

### 4.5 Service Identity

**ID-020 (MUST)** Service-to-service identity is SPIFFE-based. Each service in a conforming implementation has a SPIFFE ID that is verifiable.

**ID-021 (MUST)** Service identities are not interchangeable with Party identities.

### 4.6 Federation Membership Identity

**ID-030 (MUST)** Federation members are Parties of type `federation-member`, with additional fields recording membership scope, admission date, and current status (active, suspended, expelled, withdrawn).

**ID-031 (MUST)** Membership status changes are recorded as immutable events, signed by the appropriate governance body.

---

## 5. Event Protocol

**Status:** Stable

### 5.1 Event Format

**EV-001 (MUST)** All cross-platform events conform to a common envelope:

```
{
  "id": "<event URI>",
  "type": "<event type URI>",
  "occurred_at": "<ISO 8601 timestamp>",
  "ingested_at": "<ISO 8601 timestamp>",
  "principal": "<Party or service URI>",
  "subject": "<entity URI the event concerns>",
  "schema_version": "<semver>",
  "payload": { ... },
  "signature": "<base64-encoded signature>",
  "prior_event_hash": "<hash of preceding event in scope, where applicable>"
}
```

**EV-002 (MUST)** Payload schemas are defined in JSON Schema with stable `$id` URIs.

**EV-003 (MUST)** Events are signed by the principal field's identity.

### 5.2 Event Topics

**EV-010 (MUST)** Cross-platform events are published on topics with the convention `robotanica.<source>.<entity-type>.<event-type>`.

**EV-011 (MUST)** Topic schemas are versioned and published in AsyncAPI 2.x.

**EV-012 (MUST)** Consumers declare schema compatibility at subscription time; producers MUST NOT silently break schema compatibility.

### 5.3 Event Chaining

**EV-020 (MUST)** Events affecting a stateful entity (Lease lifecycle, Cohort lifecycle, Credit lifecycle, etc.) chain to prior events in the same scope by including the prior event hash.

**EV-021 (MUST)** The event chain is independently verifiable: given any event, the chain back to the originating event of the entity must be reconstructible from signed records.

### 5.4 Event Replay

**EV-030 (MUST)** Implementations MUST support event replay for audit, recovery, and conformance testing.

**EV-031 (MUST)** Replayed events do not re-execute side effects: replay reconstructs state, not actions.

### 5.5 Event Retention

**EV-040 (MUST)** Events are retained for the lifetime of the entity they concern, plus a federation-defined archival period (default: 50 years post-entity-closeout).

**EV-041 (MUST)** Retention is in open formats per INV-020, in storage independent of any single vendor.

---

## 6. Recipe Protocol

**Status:** Stable

### 6.1 Recipe URIs

**RP-001 (MUST)** Recipes are entities in Gaia's interpretation layer with URIs of the form `gaia://recipe/<region>/<id>@<version>`.

**RP-002 (MUST)** Recipe URIs include the version. A recipe URI without version refers to the recipe across all versions.

**RP-003 (MUST)** Once a recipe version is published, it is immutable. New versions are new entities.

### 6.2 Recipe Content Schema

**RP-010 (MUST)** Recipes follow the schema defined in Gaia's interpretation layer (Gaia PRD §6.4), including:

- Target ecosystem and bioregion
- Species mix with proportions
- Density specifications
- Succession plan
- Tending operations and cadence
- Monitoring requirements (links to MRV protocols)
- Expected outcomes with thresholds

**RP-011 (MUST)** Recipes link to evidence: prior outcomes, scientific publications, expert testimony, traditional knowledge attestations.

**RP-012 (MUST)** Recipes are typed by methodology (Miyawaki, Savory, FMNR, etc.) and may inherit from methodology templates.

### 6.3 Recipe Binding

**RP-020 (MUST)** When a recipe is applied to a parcel, a `RecipeInstance` entity is created with URI `gaia://recipe-instance/<region>/<id>` linking the versioned recipe URI to the parcel URI and cohort URI.

**RP-021 (MUST)** RecipeInstance binding is signed by the Party authorizing the application (Landowner consent, Operator acceptance, Federation acknowledgment).

**RP-022 (MUST)** RecipeInstance is the bridge entity for outcome attribution: outcomes are computed per RecipeInstance and aggregated to recipes.

### 6.4 Recipe Deviation

**RP-030 (MUST)** Where execution diverges from the bound recipe, the deviation is recorded as an OperationEvent (per OpenFactory protocol) referencing the RecipeInstance and the specific deviation.

**RP-031 (MUST)** Material deviations (species substitution, density change, methodology variance) trigger review per Gaia's recipe revision protocol.

### 6.5 Recipe Revision

**RP-040 (MUST)** Recipe revisions follow the proposal-review-merge protocol of Gaia's interpretation layer (Gaia PRD §6.5).

**RP-041 (MUST)** Recipe revisions do not silently affect existing RecipeInstances: existing instances remain bound to the version they were bound to. Migration of an existing instance to a new recipe version is an explicit amendment under the Lease Protocol.

---

## 7. Lease Protocol

**Status:** Stable

### 7.1 Lease URIs

**LP-001 (MUST)** Stewardship Leases are entities in A3 with URIs of the form `a3://lease/<region>/<id>`.

**LP-002 (MUST)** Lease URIs are stable for the life of the lease and beyond closeout.

### 7.2 Lease Content

**LP-010 (MUST)** Each Lease conforms to the Stewardship Lease Requirements Specification, instantiated through a jurisdiction-specific variant signed by qualified counsel for the parcel's jurisdiction.

**LP-011 (MUST)** The Lease records:

- Parties (Landowner, Operator, Federation)
- Acknowledged Parties (Indigenous or Local Community where applicable)
- Parcel (Gaia parcel URI)
- Bound Recipe (Gaia recipe URI with version)
- Compensation structure
- Term
- Jurisdictional variant reference
- Consent records (FPIC where applicable)
- Public registry registration where applicable

### 7.3 Lease State Machine

**LP-020 (MUST)** Leases follow the state machine defined in A3 (PRD §5.3): `proposed`, `consent-pending`, `signed`, `active`, `under-amendment`, `breach-notice`, `cure-period`, `under-mediation`, `under-arbitration`, `succession-pending`, `terminated`, `closed-out`.

**LP-021 (MUST)** State transitions are signed events recorded immutably.

**LP-022 (MUST)** Conforming implementations MUST NOT permit state transitions outside the defined state machine.

### 7.4 Consent and FPIC

**LP-030 (MUST)** Where the parcel involves an Indigenous or Local Community, FPIC is required for lease formation. FPIC is recorded as a `Consent` entity with the community's signing identity and the documented consultation process.

**LP-031 (MUST)** FPIC may be revoked under the conditions defined in A3 (PRD §6.4 A3-C-003). Revocation triggers Lease review per the state machine.

**LP-032 (MUST NOT)** Implementations MUST NOT bypass FPIC for operational urgency.

### 7.5 Lease Amendment

**LP-040 (MUST)** Amendments follow the procedures of the Lease Requirements §11: routine, material, and recipe-update categories, each with defined consent requirements.

**LP-041 (MUST)** Amendments that would conflict with un-amendable Charter provisions (Charter §8.1) are void.

### 7.6 Lease Termination and Closeout

**LP-050 (MUST)** Termination follows Lease Requirements §6, with the no-abandonment provision strictly enforced.

**LP-051 (MUST)** Closeout includes data delivery to the Landowner per Lease Requirements §8.4.

---

## 8. Credit Protocol

**Status:** Stable

### 8.1 Credit URIs

**KP-001 (MUST)** Credits are entities in A3 with URIs of the form `a3://credit/<region>/<id>`.

**KP-002 (MUST)** Credit URIs are stable across transfer, retirement, and reconciliation.

### 8.2 Credit Content

**KP-010 (MUST)** Each Credit records:

- Type (carbon, biodiversity, ecosystem service, with subtype as applicable)
- Vintage
- Parcel URI
- Lease URI
- RecipeInstance URI
- Verification report URI(s)
- Issuer (typically the Federation)
- Current holder
- Lifecycle state (`pending`, `issued`, `transferred`, `retired`, `reconciled`)

### 8.3 Issuance

**KP-020 (MUST)** Credits are issued only on the basis of verified outcomes recorded in Gaia per the MRV Specification.

**KP-021 (MUST)** Implementations MUST refuse to issue Credits for unverified or projected outcomes.

**KP-022 (MUST)** Issuance follows progressive issuance discipline (MRV §10.2): a defined fraction at each verified milestone, with full credit only after the species- and ecosystem-specific permanence threshold.

**KP-023 (MUST)** Issuance is signed by the Federation governance body authorized for the credit type.

### 8.4 Transfer

**KP-030 (MUST)** Credit transfer is recorded as an event signed by both transferor and transferee.

**KP-031 (MUST)** Transfer preserves full provenance: the transferred credit retains its complete chain back to the issuance event.

### 8.5 Retirement

**KP-040 (MUST)** Credit retirement is the final lifecycle event for a credit; retired credits cannot be re-issued or re-transferred.

**KP-041 (MUST)** Retirement records the retirement reason (carbon offset claim, biodiversity offset claim, voluntary retirement) and the retiring Party.

### 8.6 Reconciliation

**KP-050 (MUST)** When site failure or methodology correction requires it, affected Credits are reconciled per MRV §14.

**KP-051 (MUST)** Reconciliation events are signed by the Federation governance body authorized for the credit type and are recorded immutably.

**KP-052 (MUST)** Reconciliation may void Credits or compensate via the Federation reconciliation reserve. Both options are recorded transparently.

### 8.7 External Registry Integration

**KP-060 (SHOULD)** Conforming implementations MAY integrate with external credit registries (Verra, Gold Standard, Plan Vivo) for credits participating in regulated markets.

**KP-061 (MUST)** Integration with external registries MUST preserve A3's source-of-truth status. Where external registry state diverges from A3 state, A3 is authoritative for federation-internal purposes; the integration layer reconciles.

---

## 9. Verification Protocol

**Status:** Stable

### 9.1 Verifier Identity

**VP-001 (MUST)** Verifiers are Parties of type `verifier`, with additional fields recording accreditation source, scope, and current status.

**VP-002 (MUST)** Verifiers MUST NOT have financial interest in the verified outcomes per MRV §3.3.

### 9.2 Verification Reports

**VP-010 (MUST)** Verification reports are entities with URIs of the form `gaia://verification/<region>/<id>`.

**VP-011 (MUST)** Verification reports record:

- The RecipeInstance verified
- The verification scope (routine, deep, triggered, cross)
- The methodology applied
- The findings
- The limitations and caveats
- The verifier's signed attestation

### 9.3 Cross-Verification

**VP-020 (SHOULD)** Implementations SHOULD support cross-verification: independently produced verifications of the same RecipeInstance, with public comparison.

### 9.4 Verifier Accountability

**VP-030 (MUST)** Verifier performance is tracked: verification volume, error rates from cross-verification, dispute outcomes.

**VP-031 (MUST)** Verifiers found to have material errors or conflicts of interest are subject to suspension or expulsion per MRV §7.5.

### 9.5 Indigenous and Community Verification

**VP-040 (MUST)** Indigenous and community verification under their own protocols is recognized as legitimate verification per MRV §7.6.

**VP-041 (MUST)** The community determines methodology and reporting form.

**VP-042 (MUST)** Where indigenous and quantitative verification disagree, both are recorded; disagreements are surfaced for governance, not erased.

---

## 10. Sovereignty Protocol

**Status:** Stable

### 10.1 Sovereignty Declarations

**SP-001 (MUST)** Every parcel and every entity associated with a parcel carries a sovereignty declaration that records:

- Jurisdiction
- Indigenous or community claims
- Data residency requirements
- Coarsening rules for sensitive locations
- Public-record disposition

**SP-002 (MUST)** Sovereignty declarations are first-class entities, signed by appropriate authorities at lease formation and updatable through defined consent processes.

### 10.2 Data Residency

**SP-010 (MUST)** Data tied to a parcel defaults to storage in the parcel's jurisdiction.

**SP-011 (MUST)** Cross-jurisdictional replication for redundancy is permitted only where the sovereignty declaration permits it, and never to jurisdictions where indigenous or community parties have specifically excluded data access.

### 10.3 Indigenous Sovereignty

**SP-020 (MUST)** Where indigenous or community parties are involved, the CARE Principles apply: collective benefit, authority to control, responsibility, ethics.

**SP-021 (MUST)** The community determines what data is collected, who has access, what may be published.

**SP-022 (MUST NOT)** Federation operations MUST NOT override community decisions regarding data scoped to community parcels.

### 10.4 Sensitive-Location Coarsening

**SP-030 (MUST)** Locations of vulnerable species, sacred sites, conflict-zone restoration sites, and other categories where exposure creates harm MUST be coarsened in public APIs.

**SP-031 (MUST)** Coarsening rules are recorded in the sovereignty declaration; implementations MUST enforce them at the API layer.

### 10.5 Forking and Sovereignty

**SP-040 (MUST)** A federation member that forks Robotanica's protocol or platforms (Charter §5.4) inherits sovereignty obligations: data they hold must continue to honor sovereignty declarations of the parties whose data it is.

**SP-041 (MUST NOT)** Forking MUST NOT be used to circumvent sovereignty.

---

## 11. Governance Protocol

**Status:** Stable

### 11.1 Governance Decisions

**GP-001 (MUST)** Decisions of consequence are recorded as `GovernanceDecision` entities with:

- The question
- Options considered
- Decision
- Rationale
- Parties involved
- Timestamp
- Authorizing body's signature

**GP-002 (MUST)** Decisions are public unless they touch protected categories (PII, sensitive locations, indigenous sovereignty); see SP-030.

### 11.2 Authority

**GP-010 (MUST)** Each decision type is associated with an authorized body:

- Recipe approvals → Science Council
- Lease succession and dissolution → Stewardship Office
- Federation membership → Federation governance body
- Charter amendments → Charter amendment process (Charter §8)
- Local site decisions → site stewards within constraints
- Regional coordination → regional governance bodies

**GP-011 (MUST)** Decisions made outside authorized bodies are not recognized by the protocol.

### 11.3 Veto and Appeal

**GP-020 (MUST)** Science Council veto authority over recipes is binding and cannot be overridden by operational governance bodies.

**GP-021 (MUST)** Appeals of Science Council decisions follow the Charter amendment process or future-defined procedures specifically authorized.

### 11.4 Nested Governance

**GP-030 (MUST)** Decisions are made at the lowest level competent (Charter §2.10 subsidiarity; Charter §4.5 nested governance).

**GP-031 (MUST NOT)** Higher governance bodies MUST NOT silently override lower-body decisions; override requires explicit, recorded process.

### 11.5 Federation Membership Lifecycle

**GP-040 (MUST)** Federation membership admission, suspension, expulsion, and withdrawal are recorded as immutable events signed by the relevant governance body.

**GP-041 (MUST)** Suspended or expelled members MUST NOT receive Service Contract dispatch or new Lease assignments.

---

## 12. Dispute Protocol

**Status:** Stable

### 12.1 Dispute Filing

**DP-001 (MUST)** Any Party to a Lease or ServiceContract may open a `DisputeCase` entity with stated cause, evidence, and requested resolution.

**DP-002 (MUST)** Dispute filings are recorded immutably and notify all affected Parties.

### 12.2 Dispute Routing

**DP-010 (MUST)** Disputes route through the levels specified in the Lease Requirements §12: direct, mediation, arbitration, jurisdictional courts, indigenous forums.

**DP-011 (MUST)** Where the dispute involves indigenous parties, indigenous customary forums take precedence if invoked by the indigenous party.

### 12.3 Resolution Recording

**DP-020 (MUST)** Dispute resolutions are recorded as immutable events, including the resolution body, the decision, and any compensation or remediation ordered.

**DP-021 (MUST)** Resolution outcomes affecting other entities (Lease termination, credit reconciliation, membership status change) propagate as appropriate events.

### 12.4 Non-Retaliation

**DP-030 (MUST)** Parties in dispute are protected from discriminatory dispatch, suspension, or other adverse action during the dispute, except for cause unrelated to the dispute.

---

## 13. Conformance Protocol

**Status:** Stable

### 13.1 Conformance Levels

**CP-001 (MUST)** Conformance is defined at three levels:

- **Read conformance** — Implementations that consume protocol-defined data (read-only federation members).
- **Write conformance** — Implementations that produce protocol-defined data (Operators, scientists, etc.).
- **Platform conformance** — Implementations that operate platform-class services (alternative Gaia, A3, or OpenFactory implementations).

### 13.2 Test Suites

**CP-010 (MUST)** Each conformance level has a published test suite that verifies protocol adherence.

**CP-011 (MUST)** Test suites cover: schema validity, signature verification, state machine adherence, sovereignty enforcement, immutability, event chaining.

**CP-012 (MUST)** Test suites are open-source and maintained by the Federation; federation members may contribute test cases.

### 13.3 Certification

**CP-020 (MUST)** New federation members complete the conformance test suite as a condition of admission.

**CP-021 (SHOULD)** Federation members re-certify on a defined cadence (default: annual) or on protocol version upgrade.

**CP-022 (MUST)** Certification is recorded as a `GovernanceDecision`.

### 13.4 Non-Conformance

**CP-030 (MUST)** Federation members found materially non-conforming are subject to graduated sanctions per Charter §6.4: warning, conditional suspension, suspension, expulsion.

**CP-031 (MUST)** Non-conformance affecting active Leases triggers Lease review and potentially Operator succession.

### 13.5 Conformance and Forks

**CP-040 (MUST)** A fork (Charter §5.4) that wishes to remain interoperable with the Federation must satisfy the relevant conformance level.

**CP-041 (MUST)** A fork that does not satisfy conformance operates outside the Federation; its claims are not recognized by the Federation's public record.

---

## 14. Versioning Protocol

**Status:** Stable

### 14.1 Versioning Scheme

**VR-001 (MUST)** Each protocol section is versioned independently using semantic versioning:

- **Major** — backwards-incompatible change.
- **Minor** — backwards-compatible feature addition.
- **Patch** — backwards-compatible clarification or correction.

### 14.2 Compatibility

**VR-010 (MUST)** Implementations declare the protocol versions they support; consumers verify compatibility before connecting.

**VR-011 (MUST)** Major version changes require parallel operation of old and new during a transition period of at least 18 months.

**VR-012 (MUST NOT)** Implementations MUST NOT silently change behavior across versions.

### 14.3 Change Process

**VR-020 (MUST)** Protocol changes are proposed through a public process with at least 90 days of comment.

**VR-021 (MUST)** Changes affecting un-amendable Charter provisions are not permitted at the protocol layer.

**VR-022 (MUST)** Approved changes are merged into the protocol document and signed by the Federation governance body.

### 14.4 Deprecation

**VR-030 (MUST)** Deprecated protocol features are announced in advance with a deprecation timeline.

**VR-031 (MUST)** Deprecated features remain operational for at least 18 months after deprecation announcement, unless deprecated for security reasons.

---

## 15. Reference Implementations

**Status:** Stable

### 15.1 Reference Implementations Are Not the Protocol

**RI-001** Reference implementations are illustrative, not normative. The protocol is defined in this document; implementations are conforming if they satisfy the protocol, even if they differ from the reference.

### 15.2 Robotanica's Reference Implementations

**RI-010** Robotanica maintains reference implementations for Gaia, A3, and OpenFactory per their respective PRDs. These implementations are open-source and serve as both production systems for Robotanica's operations and as reference material for federation members and forks.

### 15.3 Alternative Implementations

**RI-020** Alternative implementations are welcome and supported. Conformance tests verify that an alternative implementation meets the protocol; certification grants federation interoperability.

**RI-021** Alternative implementations may differ in language, runtime, storage, deployment, or many other dimensions, provided conformance is maintained.

### 15.4 Forks

**RI-030** Per Charter §5.4, forks are first-class. A fork that maintains conformance interoperates with the Federation. A fork that does not maintain conformance operates independently and is not recognized by the Federation's public record.

**RI-031** Forks inherit sovereignty obligations (SP-040).

---

## 16. Security Protocol

**Status:** Stable

### 16.1 Authentication

**SC-001 (MUST)** All API access is authenticated. Anonymous access is permitted only for explicitly public endpoints.

**SC-002 (MUST)** Human identity uses OIDC; service identity uses SPIFFE.

### 16.2 Authorization

**SC-010 (MUST)** Authorization is attribute-based, with attributes including: Party identity, federation membership status, parcel scope, recipe scope, sovereignty constraints.

**SC-011 (MUST)** Authorization decisions are logged.

### 16.3 Cryptographic Discipline

**SC-020 (MUST)** Signing algorithms in use are recommended by current NIST or equivalent guidance.

**SC-021 (MUST)** Implementations support algorithm rotation.

**SC-022 (MUST)** Long-term archival includes periodic re-signing with current algorithms.

### 16.4 Audit Logging

**SC-030 (MUST)** All security events (authentication, authorization decisions, key rotation, signature verification failures) are logged.

**SC-031 (MUST)** Audit logs are append-only and retained per the event retention requirements (EV-040).

---

## 17. Open Questions

These are areas where the protocol is incomplete or contested:

- **Cross-protocol-version event chaining.** When an entity's events span major protocol versions, event chain verification across the boundary needs detailed specification.
- **Token integration without crypto-economic capture.** External credit markets are increasingly tokenized. The protocol's posture toward tokenization (currently: tokens layered on top, not embedded) needs concrete design when external markets require it.
- **Recipe interop with external scientific knowledge graphs.** GBIF, iNaturalist, and others use different schemas. The interop pattern is sketched but not specified in detail.
- **Federation member governance evolution.** The governance protocol assumes Federation governance bodies exist and have authority. The evolution of those bodies (new bodies created, old bodies retired) is not yet specified at the protocol level.
- **Cross-jurisdictional dispute enforcement.** The dispute protocol routes disputes; enforcement of arbitration awards across jurisdictions requires more detail, particularly for the case where assets are in jurisdiction A and parties are in jurisdiction B.
- **Sovereignty declaration evolution.** When sovereignty declarations change (a community develops new policy; a jurisdiction passes new law), the propagation of the change to existing data and entities needs specification.
- **Conformance test suite governance.** Who maintains the test suite, who certifies, how are disagreements about conformance resolved? The protocol relies on the test suite but does not yet fully specify its own governance.
- **Public-record granularity at scale.** As the public record grows to billions of events, the structure for public consumers (researchers, journalists, communities) needs refinement.

---

## 18. Document Stewardship

This protocol document is stewarded by the Federation governance body. Changes follow §14.

The document is published openly at a stable URL with all prior versions retained.

This document is the contract. Where specific implementations of the protocol are described in PRDs and other documents, those documents are subordinate to this one.

---

## Appendix A — Glossary (Protocol-Specific)

- **Conformance** — Adherence to the protocol as verified by the test suite.
- **Event Chain** — A sequence of events linked by hash references, providing tamper-evident history.
- **Federation Member** — A Party with active membership status in the federation.
- **Fork** — An independent implementation or operation of Robotanica's protocols and platforms, per Charter §5.4.
- **Reference Implementation** — Robotanica's open-source implementations of Gaia, A3, OpenFactory; illustrative not normative.
- **Sovereignty Declaration** — A first-class entity recording the sovereignty obligations associated with a parcel or entity.
- **URI** — Uniform Resource Identifier; the stable identity for protocol-level entities.

---

## Appendix B — Standards and References

- **JSON Schema** for entity schemas.
- **JSON-LD** for linked data interchange.
- **OpenAPI 3.1** for synchronous API specifications.
- **AsyncAPI 2.x** for event API specifications.
- **OIDC** for human identity.
- **SPIFFE / SPIRE** for service identity.
- **RFC 2119** for requirement-level conventions.
- **W3C RDF 1.1, SPARQL 1.1** for semantic interchange.
- **OGC STAC** for spatiotemporal asset catalog.
- **ROS 2** and **Open-RMF** for robotics integration.
- **CARE Principles** for indigenous data governance.
- **FPIC** as defined under UN Declaration on the Rights of Indigenous Peoples.

---

*This document is the federation contract. Implementations that satisfy this contract are interoperable. Implementations that do not, are not. The contract is open. The contract is testable. The contract is stable. The contract may be forked.*
