# Data Lifecycle and Preservation Plan

## Specification (v0)

**Document type:** Operational specification
**Status:** Draft for ratification
**Companion documents:** Robotanica Charter, Gaia PRD, A3 PRD, OpenFactory PRD, Protocol Specifications, MRV Specification, Threat Model

---

## 1. Purpose and Status

This document specifies how Robotanica preserves its data across decades.

Every major document in the project has assumed multi-decade durability and reproducibility:

- Gaia PRD §7.4 — observations and codex entries queryable for 50+ years.
- A3 PRD §7.4 — Lease and credit history queryable through Lease term plus 50 years.
- OpenFactory PRD §7.5 — Robot and biological genealogies queryable for the lifetime of resulting Cohorts plus 50 years.
- MRV Specification §7.4 — verification reports retained as part of the integrity of the public record.
- Protocol Specifications §5.5 — events retained for entity lifetime plus federation-defined archival.

None of those documents specifies *how* preservation actually happens at operational scale, across format obsolescence, storage technology evolution, cryptographic decay, organizational change, jurisdictional disruption, and the simple passage of time.

This document is that specification. It operationalizes preservation with the rigor of a library science discipline applied to a digital, federated, planetary-scale corpus.

---

## 2. The Multi-Decade Challenge

### 2.1 Time Horizons

Restoration data is preserved across at least these horizons:

- **Operational horizon** — current and recent state used for live operations. Days to years.
- **Lease horizon** — duration of the Stewardship Lease, typically 50+ years. Required for full audit, succession, and outcome tracking.
- **Cohort horizon** — lifetime of a planted cohort plus an archival period. For long-lived species (oak, redwood), this can be hundreds of years.
- **Civilizational horizon** — the period over which the project's data may be referenced by future generations as record of restoration practice. Indefinite.

### 2.2 Failure Modes Over Time

Data that is not preserved fails in characteristic ways:

- **Format obsolescence** — proprietary or undocumented formats become unreadable as software ecosystems evolve.
- **Storage decay** — physical media (disks, tapes, optical) lose data over time.
- **Storage technology obsolescence** — entire storage paradigms (CD-ROM, ZIP disks, certain cloud APIs) become unsupported.
- **Cryptographic decay** — algorithms once secure (MD5, SHA-1, RSA-1024) become broken; signatures lose verification value.
- **Catalog loss** — without manifests and indices, even preserved data becomes effectively inaccessible.
- **Provenance loss** — data without context cannot be interpreted; a CSV file in 2070 means nothing without its schema.
- **Sovereignty drift** — sovereignty obligations recorded today may not be honored in a future organization that does not understand them.
- **Jurisdictional disruption** — political or legal changes can disrupt access or impose new constraints.

### 2.3 The Discipline Required

Multi-decade preservation is a discipline, not a feature. It requires:

- **Open formats** that can be parsed without proprietary tooling.
- **Multiple copies** in geographically and politically diverse locations.
- **Regular migration** as formats and technologies evolve.
- **Periodic verification** that the data is actually readable, not just present.
- **Catalog and manifest discipline** so that data can be located and interpreted.
- **Cryptographic agility** so that integrity protection adapts as algorithms weaken.
- **Sovereignty preservation** so that data sovereignty obligations persist across technical changes.
- **Sunset where appropriate** — some data should not persist forever.

These disciplines are not new. Libraries, archives, and scientific data repositories have practiced them for centuries (in non-digital form) and decades (in digital). Robotanica draws on these traditions.

---

## 3. Principles

These principles bind data preservation decisions and may not be set aside for storage cost or operational convenience.

### 3.1 Preservation Is a First-Class Concern

**PRES-001** Preservation is not an afterthought added to operational systems. It is a first-class concern with dedicated capacity, governance, and budget.

### 3.2 Open Formats Always

**PRES-010** All preserved data is stored in open formats per Protocol §3.3 (INV-020). Proprietary formats are not used for archival; where operational systems use proprietary formats, conversion to open formats occurs at preservation time.

### 3.3 Multiple Copies Always

**PRES-020** Preserved data exists in at least three geographically and politically diverse copies at all times.

**PRES-021** "Diverse" means: different countries, different regulatory regimes, different operational entities. Three copies in the same cloud region count as one copy.

### 3.4 Verification Periodically Required

**PRES-030** Preserved data is verified for readability and integrity on a defined cadence. A copy that has not been read in years may not actually be readable.

### 3.5 Migration Is Routine

**PRES-040** Format and storage migration is a routine operational practice, not a crisis response. Migration cycles are planned and budgeted.

### 3.6 Provenance Preserved With Data

**PRES-050** Data is preserved together with the metadata necessary to interpret it: schema, units, methodology, source, time, signing identity. Data without provenance is not preserved as authoritative.

### 3.7 Sovereignty Survives Technology

**PRES-060** Sovereignty obligations on preserved data persist across technical migrations. A data sovereignty declaration recorded today applies to the data wherever it is migrated, in whatever format.

### 3.8 Sunset Where Appropriate

**PRES-070** Some data should be deleted at defined points: PII beyond retention requirements, data subject to community withdrawal under sovereignty provisions, data whose continued existence creates harm. Sunset is a structural feature, not a failure of preservation.

### 3.9 Independent Verifiability

**PRES-080** Preservation discipline is independently verifiable. A third party with access to the preserved data, the manifests, and the format specifications must be able to verify integrity without trusting Robotanica's runtime.

---

## 4. Data Classification

Different data classes have different preservation requirements. The plan defines four classes.

### 4.1 Class I — Permanent Record

Data preserved for the lifetime of the relevant entity plus an archival period of 50+ years, and indefinitely for entities whose horizon is themselves indefinite.

Includes:

- Lease documents, signatures, consent records, and lifecycle events (A3).
- Stewardship Office relationship records and succession documents.
- Codex entries and their full revision history (Gaia interpretation layer).
- Verification reports and the underlying observations (Gaia, MRV).
- Aggregate restoration outcomes and credit lifecycle events (A3, MRV).
- Charter, governance decisions, and Federation governance records.
- Indigenous data sovereignty declarations and consent records.

Class I is the most stringent; the disciplines below apply with full rigor.

### 4.2 Class II — Operational Provenance

Data preserved for the lifetime of the relevant entity plus 25 years.

Includes:

- Operational events (planting, tending, monitoring) per OpenFactory.
- Genealogy records (BiologicalBatches, RobotAssemblyRecords).
- Production runs, work orders, BOMs.
- Routine MRV measurement records (the underlying samples and observations supporting verification reports).
- Federation membership lifecycle.

Class II supports auditability and learning; it must persist long enough for retrospective analysis and for honoring multi-decade Lease obligations.

### 4.3 Class III — Aggregate and Derived

Data preserved for 25 years from creation.

Includes:

- Time-series telemetry summaries (UMH-derived).
- Derived indices and aggregate metrics.
- Operational performance summaries.
- Communication and coordination records of routine character.

Class III supports learning over decades but is not the primary record. The primary record (Class I and II) supports reconstruction of any Class III data that is lost.

### 4.4 Class IV — Transient and Operational

Data with retention measured in months to a few years; not preserved long-term.

Includes:

- Live operational caches.
- Edge runtime buffers (per OpenFactory edge resilience).
- Monitoring telemetry beyond retention windows.
- Routine system logs not bearing on Class I-III content.

Class IV exists for current operations; once superseded by Class I-III records or by aged-out retention, it is allowed to be deleted.

---

## 5. Format Discipline

### 5.1 Format Hierarchy

For each data type, a primary archival format is specified. Formats are open, well-documented, widely-implemented, and where possible, supported by multiple independent reference implementations.

**Tabular and time-series:**

- **Apache Parquet** for analytical archives.
- **GeoParquet** for spatial-tabular data.
- **CSV with documented schema** for plain-text fallback.

**Spatial:**

- **GeoParquet** primary.
- **Cloud-Optimized GeoTIFF (COG)** for raster.
- **GeoPackage** for portable spatial bundles.
- **STAC** catalog for asset cataloging.

**Knowledge graph (Codex):**

- **RDF (Turtle, N-Quads)** and **JSON-LD** primary.
- **Neo4j-specific exports** are converted to RDF for archival.

**Documents:**

- **PDF/A** for archival document formats.
- **Markdown with explicit schema** for structured text.
- **HTML with embedded provenance metadata** for web-presentation archive.

**Events and ledger:**

- **JSON Lines (JSONL)** with **JSON Schema** for event archives.
- Cryptographic signatures preserved alongside event payloads.

**Imagery:**

- **COG (Cloud-Optimized GeoTIFF)** for raster imagery.
- **JPEG 2000** for high-fidelity preservation where COG is inadequate.
- Original imagery in source format alongside COG conversion when source format itself is open.

**Time-series telemetry summaries:**

- **Parquet** with **TimescaleDB-compatible** schema.

### 5.2 Format Documentation

**FORM-001** Every preserved file references its format specification by URI; if the format specification is itself an external document, a copy is preserved in the archive.

**FORM-002** Every preserved data set includes a manifest describing its structure, units, columns or fields, and creation methodology.

### 5.3 Format Migration

**FORM-010** Format choices are reviewed every five years. Migration to successor formats occurs when:

- The current format is deprecated or losing implementation support.
- A successor format provides material durability or accessibility advantages.
- External standards bodies recommend migration.

**FORM-011** Migration preserves bit-identical content where possible; where format changes are not bit-identical, migration is documented and the original format is preserved alongside the new format for at least one full migration cycle.

---

## 6. Storage Architecture

### 6.1 Storage Tiers

Preserved data exists in multiple storage tiers reflecting access patterns and durability requirements.

**Hot tier:** Frequently-accessed operational data. Stored in performant cloud or on-premises systems supporting current operations. Retention: weeks to a few years.

**Warm tier:** Infrequently-accessed but periodically-needed data. Stored in cost-efficient cloud storage with reasonable retrieval latency. Retention: years to decades.

**Cold archival tier:** Long-term preservation. Stored in maximally-durable formats with retrieval latency measured in hours. Retention: 25-50+ years per Class.

**Glacial archival tier:** Multi-generational preservation. Stored on physical media in geographically and politically diverse locations. Retention: indefinite.

### 6.2 Tier Distribution

**STOR-001** Class I data exists in all tiers, with a primary copy in cold archival and at least three copies across cold and glacial archival.

**STOR-002** Class II data exists in warm, cold, and glacial tiers, with at least three replicated copies across tiers.

**STOR-003** Class III data exists primarily in warm tier with periodic snapshots to cold archival.

**STOR-004** Class IV data exists in hot tier only.

### 6.3 Storage Technology Selection

**STOR-010** Storage technologies are selected for openness and durability, not exclusively for cost. Specifically:

- Object storage with documented access protocols (S3-compatible) is preferred for cloud-resident archives.
- LTO tape libraries are used for glacial archival.
- Optical media (M-DISC, archival Blu-ray) is used as a tertiary copy for long-horizon resistance to magnetic decay.
- Provider-specific storage (AWS Glacier, Azure Cold Blob) is used as one of the three copies, never as all three.

### 6.4 Geographic and Political Diversity

**STOR-020** The three minimum copies of preserved data are distributed across:

- **At least three jurisdictions** with different regulatory regimes.
- **At least three operational entities** (different cloud providers, or cloud + on-premises, or different countries' archival infrastructures).
- **At least two physical-storage paradigms** (e.g., disk + tape, or cloud + optical) for Class I data.

**STOR-021** No single storage provider, jurisdiction, or paradigm holds all copies of any preserved data.

### 6.5 Indigenous and Community Data Storage

**STOR-030** Where data is subject to indigenous or community sovereignty (per Protocol §10), storage location and access are determined by the sovereign party.

**STOR-031** Sovereignty constraints may require that data be stored only in specific jurisdictions, only on specific infrastructure, or only for specific durations. These constraints override the default storage architecture above.

---

## 7. Cryptographic and Integrity Discipline

### 7.1 Hashing

**CRY-001** Every preserved file is accompanied by a cryptographic hash (currently SHA-256 or stronger; subject to algorithm evolution).

**CRY-002** Hashes are stored separately from the data they verify, in a manifest that is itself cryptographically signed.

**CRY-003** Manifests are versioned; each archival snapshot has its own dated, signed manifest.

### 7.2 Signing

**CRY-010** Class I data is cryptographically signed by the originating principal at creation. Signatures are preserved as part of the data.

**CRY-011** Manifest signatures attest to the integrity of the snapshot. Manifests are signed by Federation governance keys whose identity is part of the preserved record.

### 7.3 Algorithm Agility

**CRY-020** All cryptographic implementations support algorithm rotation. The preservation plan does not assume that current algorithms will remain secure.

**CRY-021** Periodic re-signing of archival data with current-best algorithms is part of preservation discipline. Re-signing produces additional signatures; original signatures are preserved.

**CRY-022** Algorithm evolution is reviewed every five years; weakened algorithms trigger re-signing campaigns.

### 7.4 Quantum-Resistant Posture

**CRY-030** The preservation plan recognizes that current public-key algorithms (RSA, ECDSA) may become breakable by future quantum computing. Migration to post-quantum signature schemes is planned as those schemes mature and are standardized.

### 7.5 Independent Verifiability

**CRY-040** A third party with access to: the data, the manifest, the format specifications, and the public keys of the relevant signing principals must be able to verify integrity without any other Robotanica system being available.

---

## 8. Migration Cadence

### 8.1 Format Migration

**MIG-001** Format migration occurs:

- When the current format is deprecated by its standards body.
- When a successor format becomes adopted as the de facto archival standard.
- At regular five-year reviews if neither of the above triggers fires.

### 8.2 Storage Technology Migration

**MIG-010** Storage technology migration occurs:

- When the current technology is end-of-life.
- When a vendor exits the market.
- At regular ten-year intervals to ensure preservation across technology generations.

### 8.3 Cryptographic Migration

**MIG-020** Cryptographic algorithm migration occurs:

- When the current algorithm is deprecated by NIST or equivalent body.
- When practical attacks reduce security materially.
- When standards bodies recommend transition.

### 8.4 Migration as Exercise

**MIG-030** Migration is also performed as a planned exercise, even when not triggered by external events. Annual exercises restore representative samples from each storage tier and verify readability. This catches preservation failures before they become catastrophic.

### 8.5 Migration Records

**MIG-040** Every migration is recorded: the previous state, the new state, the rationale, the parties involved, the verification of completion. Migration records are themselves preserved as Class I data.

---

## 9. Verification and Testing

### 9.1 Continuous Integrity Checking

**VER-001** Hash verification on stored data runs continuously across all preserved tiers. Failures (corruption detected) trigger recovery from another copy.

### 9.2 Periodic Restoration Testing

**VER-010** On a defined cadence (default: monthly for sample-based testing, annually for comprehensive tier-wide testing), randomly-selected files from each tier are restored and verified for readability.

**VER-011** "Readability" means: the file can be parsed by a current implementation of the format specification and produces the expected content. Bit-level integrity alone is necessary but not sufficient.

### 9.3 End-to-End Reconstruction Testing

**VER-020** Annually, an end-to-end reconstruction exercise is performed: a Lease, a Cohort, or other representative entity is reconstructed entirely from preserved data, verifying that all referenced assets, manifests, and provenance are recoverable.

### 9.4 External Audit

**VER-030** Preservation discipline is audited by an external party with no operational dependency on Robotanica. The audit reviews: copy diversity, format conformance, hash integrity, restoration testing results, and migration discipline.

**VER-031** Audit findings are public.

---

## 10. Sovereignty Preservation

### 10.1 Sovereignty Travel With Data

**SOV-001** Every preserved file or dataset is associated with the sovereignty declaration applicable to it. Sovereignty declarations are preserved alongside the data they govern.

**SOV-002** When data is migrated (format, technology, location), the associated sovereignty declaration travels with it and continues to apply.

### 10.2 Sovereignty-Restricted Data

**SOV-010** Data subject to indigenous or community sovereignty is preserved subject to the sovereign party's directives, including:

- **Storage location** — limited to specified jurisdictions or infrastructures.
- **Access control** — limited to specified parties and purposes.
- **Publication** — limited to specified scope and form.
- **Retention** — limited to specified duration; sunset is honored where required.

**SOV-011** Where sovereignty constraints conflict with default preservation architecture, sovereignty prevails.

### 10.3 Sovereignty Decision Updates

**SOV-020** Sovereign parties may update sovereignty declarations through their governance processes. Updates apply prospectively; preservation discipline reflects the most current declaration.

**SOV-021** Where a sovereign party requests deletion or restriction of previously-preserved data, the request is honored per the sunset discipline of §11.

### 10.4 Forking and Sovereignty

**SOV-030** Where forks (Charter §5.4) inherit Robotanica data, sovereignty obligations carry with the inherited data. A fork that does not honor sovereignty is in violation of the protocol and is not recognized by the Federation.

---

## 11. Sunset and Deletion

### 11.1 When Data Is Deleted

Some data is deliberately deleted at defined points:

- **PII beyond retention requirement** — personal information unnecessary beyond legal retention period is deleted.
- **Sovereignty-mandated deletion** — community withdrawal of consent, indigenous sovereignty decisions, individual privacy requests where applicable.
- **Class IV data aging out** — transient operational data is allowed to be deleted when its retention window expires.
- **Data whose continued existence creates harm** — exposure that would harm vulnerable parties beyond the protections of coarsening.

### 11.2 Sunset Discipline

**SUN-001** Sunset is structured: identified categories with defined triggers, not ad hoc deletion.

**SUN-002** Every sunset event is recorded: what data, by whom requested, on what authority, with what verification. The sunset event itself is preserved as Class I data; the data sunset is not preserved.

**SUN-003** Where sunset conflicts with audit or legal-retention obligations, the conflict is surfaced and resolved through governance. Sovereign parties' deletion rights are typically primary; legal retention obligations may require limited preservation in restricted form.

### 11.3 Verification of Deletion

**SUN-010** Deletion is performed across all copies in all tiers. Verification confirms no residual copies remain, including in backups beyond formal preservation tiers.

**SUN-011** Where verification of deletion is not technically possible (e.g., data inadvertently propagated to systems outside Robotanica's control), the situation is documented and harm-reduction measures are taken.

### 11.4 Right to be Forgotten

**SUN-020** Where applicable jurisdictional law (GDPR equivalents) creates rights to deletion of personal data, those rights are honored. PII handling discipline minimizes the data subject to such rights from the start.

---

## 12. Catastrophe and Recovery

### 12.1 Catastrophic Loss Scenarios

The plan accounts for catastrophic scenarios:

- **Single-region disaster** — fire, flood, or hardware failure at one storage site.
- **Cloud provider exit** — a major provider exits a market or service.
- **Jurisdictional shutdown** — government action restricting access in one country.
- **Civilizational disruption** — pandemic, war, or comparable disruption affecting multiple regions.
- **Cyber attack** — targeted attack compromising one or more storage systems.

### 12.2 Recovery Capability

**REC-001** Loss of any single copy of preserved data must not cause data loss. Recovery from another copy must be possible within defined recovery time objectives.

**REC-002** Loss of any single jurisdiction's storage must not cause data loss. The remaining copies in other jurisdictions must be sufficient.

**REC-003** Loss of two simultaneous copies is a Sev-1 incident requiring immediate response and rebuilding the third copy.

### 12.3 Recovery Drills

**REC-010** Recovery drills are conducted at least annually, simulating loss scenarios and exercising recovery procedures.

**REC-011** Drill results are evaluated for: time to recover, completeness, integrity verification, and process gaps.

### 12.4 Civilizational Disruption Posture

**REC-020** For multi-region or civilizational disruption, the plan relies on the diversity of preservation infrastructure: glacial archives in multiple countries, on multiple media, with format and integrity discipline that does not depend on any specific operational entity remaining functional.

**REC-021** The most durable copy of Class I data is on physical media in geographically diverse locations, not in any cloud system.

### 12.5 Cyber Attack Posture

**REC-030** Preservation systems are defended against compromise:

- Glacial archives are write-once, read-many: cannot be silently altered.
- Manifests and signatures are stored separately from data they verify.
- Recovery uses independently-verified copies, not the most-recent state which may be compromised.

---

## 13. Governance

### 13.1 Preservation Office

**GOV-001** A dedicated Preservation Office within Robotanica's organization holds responsibility for this Plan's implementation. The Preservation Office:

- Maintains preservation infrastructure and migration cadence.
- Conducts verification and audit cycles.
- Coordinates with sovereign parties on sovereignty-aware preservation.
- Reports to the Stewardship Office on preservation health.

### 13.2 Preservation Budget

**GOV-010** Preservation has a dedicated budget line, not allocated from operational budgets. The budget is multi-year and protected from short-term cost pressure.

**GOV-011** Preservation cost is accepted as a structural commitment, not an optimization target. Cheaper preservation is welcomed; cheaper preservation that compromises the principles is refused.

### 13.3 Annual Preservation Report

**GOV-020** The Preservation Office publishes an annual report covering:

- Preserved volume by class and tier.
- Migration activities completed and planned.
- Verification and audit results.
- Recovery drill outcomes.
- Sovereignty handling.
- Sunset events.

### 13.4 External Audit

**GOV-030** Preservation discipline is audited by an external party annually per §9.4.

### 13.5 Preservation Plan Review

**GOV-040** This Plan is reviewed every five years comprehensively. Amendments follow Charter and Federation governance processes.

---

## 14. Open Questions

These are unresolved questions in the preservation plan:

- **Permanence of cryptographic chains over civilizational time.** Cryptographic verification depends on continuous chain of trust through algorithm migrations. A 200-year-old signed event is verifiable only if every intermediate algorithm migration was performed correctly. Long-horizon trust models for cryptographic preservation need more development than the current plan provides.
- **Format ecosystems beyond current technology.** Open formats today (Parquet, COG, RDF) may not have the same status in 50 years. Format migration discipline assumes successor formats will exist; in some cases they may not, requiring the data itself to be self-describing in formats that can be reverse-engineered from first principles.
- **Storage media for civilizational horizons.** Magnetic media and current optical media do not survive 100+ years reliably. Multi-generational preservation may require media not yet widely deployed (5D optical storage, archival glass, DNA-based storage). The plan's glacial tier needs to evolve.
- **Independent verification at scale.** External audit of preservation depends on auditor capacity. As data scales to planetary volumes, audit becomes a larger undertaking. The plan's audit discipline needs scaling.
- **Sunset for distributed data.** Once data has been published or replicated to non-Robotanica systems, deletion may not be enforceable. The plan acknowledges this; mitigation through publication discipline (publishing only what truly needs to be public) requires ongoing review.
- **Climate change and physical archives.** Physical archive locations may themselves be at risk from climate change (flooding, fires, political instability driven by climate). Physical archive site selection needs climate-aware risk assessment.
- **AI-generated content and preservation provenance.** As agents generate content, distinguishing human-authored from agent-authored preserved content becomes important. The agent-provenance discipline of Gaia §7.5 needs to extend into preservation.
- **Funding preservation across organizational change.** Robotanica's preservation depends on continued institutional capacity. If Robotanica dissolves, preservation must transfer to a successor steward (per Charter §7.4). The transfer mechanism, including funding, needs to be specified at greater detail.

---

## Appendix A — Summary Format Catalog

| Data Type | Primary Archive Format | Secondary | Rationale |
|---|---|---|---|
| Tabular data | Parquet | CSV | Wide implementation; column-oriented; schema-aware |
| Spatial-tabular | GeoParquet | GeoPackage | Spatial extension to Parquet; OGC standard |
| Spatial raster | Cloud-Optimized GeoTIFF | JPEG 2000 | OGC-standard; cloud-friendly access |
| Knowledge graph | RDF (Turtle, N-Quads) | JSON-LD | W3C standard; widely-implemented |
| Documents | PDF/A | Markdown | ISO archival standard; long-supported |
| Events | JSONL with JSON Schema | — | Plain-text; schema documents structure |
| Imagery | Cloud-Optimized GeoTIFF | Source format alongside | Open; preserves geospatial metadata |

---

## Appendix B — Cross-References

- **Robotanica Charter** §2.4 (open by default), §5.2 (open formats)
- **Gaia PRD** §7.4 (multi-decade operability)
- **A3 PRD** §7.4 (multi-decade operability)
- **OpenFactory PRD** §7.5 (multi-decade operability)
- **Protocol Specifications** §3.1 (append-only provenance), §3.3 (open formats), §5.5 (event retention)
- **MRV Specification** §7.4 (verification provenance), §14.4 (no burying failures)
- **Threat Model** §4.4 (data integrity compromise), §4.8 (technology catastrophe)

---

## Appendix C — Glossary (Preservation-Specific)

- **Algorithm agility** — The capacity to rotate cryptographic algorithms as standards evolve.
- **Class I-IV** — Data classification tiers per §4.
- **Cold archival tier** — Long-term preservation tier; retrieval in hours.
- **Glacial archival tier** — Multi-generational preservation tier; physical media in diverse locations.
- **Hot tier** — Operational tier supporting current work.
- **Manifest** — Cryptographically-signed catalog of preserved files with hashes and metadata.
- **Migration** — Planned movement of data across format, storage, or cryptographic generations.
- **Preservation Office** — Robotanica organization unit responsible for this Plan.
- **Restoration test** — Exercise of reading back preserved data to verify readability.
- **Sunset** — Deliberate, structured deletion of data per defined triggers.
- **Sovereignty travel** — The principle that sovereignty constraints follow data through migrations.
- **Warm tier** — Cost-efficient cloud storage tier; retrieval latency in seconds to minutes.

---

*Data preservation is the discipline by which the work continues to mean something across decades. It is mundane. It is unglamorous. It is essential. Without it, the verification of restoration, the genealogy of life, the record of decision, and the continuity of stewardship all decay into stories about what once was, with no way to tell whether the stories are true. This Plan is the discipline that keeps the stories verifiable.*
