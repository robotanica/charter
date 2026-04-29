# Dependencies and Partnerships Map

## Operational Specification (v0)

**Document type:** Operational and risk specification
**Status:** Draft for review
**Companion documents:** Robotanica Charter, Technical Architecture Plan, Threat Model, Funding Strategy, Federation Membership Agreement

---

## 1. Purpose and Status

This document maps Robotanica's critical dependencies and partnerships — the external relationships and infrastructure on which the project relies and the partnerships through which it operates.

The corpus has been silent on this. The Technical Architecture Plan named technologies but didn't address vendor and infrastructure dependencies as risk. The Threat Model identified failure modes but didn't enumerate the specific dependencies whose failure would create them. The Federation Membership Agreement specified member commitments but didn't specify the broader partnership ecosystem.

This document fills the gap. It distinguishes:

- **Dependencies** — single points of failure or near-failure where Robotanica relies on an external party. Loss of the dependency disrupts operations.
- **Partnerships** — mutual relationships where both parties contribute and benefit. Loss of a partnership is consequential but not necessarily disrupting.

Both matter. The document maps both, with appropriate attention to risk diversification, exit paths, and governance.

The document is **honest about reality**. Robotanica depends on infrastructure it does not control. It would be dishonest to pretend self-sufficiency. The discipline is to name dependencies clearly, manage them appropriately, and maintain exit paths where the dependency could become problematic.

---

## 2. Why This Matters

### 2.1 The Reality of External Dependencies

Modern operations at planetary scale depend on infrastructure provided by others:

- Cloud computing infrastructure operated by a small number of providers.
- Satellite imagery and remote sensing from public and commercial providers.
- Foundation AI models from a few major providers.
- Scientific data from institutions and databases.
- Communications and logistics infrastructure.
- Financial systems for payments and accounting.

Pretending Robotanica is self-sufficient would be fantasy. Naming dependencies allows them to be managed.

### 2.2 The Risk of Hidden Dependencies

Unidentified dependencies create unmanaged risk:

- A cloud provider exits a market and operations halt.
- A foundation model is deprecated and AI features fail.
- A satellite imagery provider raises prices and MRV becomes uneconomical.
- A scientific database changes terms and Codex linkages break.

Each of these is a real failure mode. The Threat Model addresses some at the category level; this document addresses them at the specific-dependency level.

### 2.3 The Difference From Partnerships

Partnerships are different from dependencies:

- A federation member is a partner, not a dependency. The federation continues if any single member leaves.
- An indigenous federation is a partner. Robotanica engages with multiple indigenous communities and federations; relationships are mutual.
- A scientific collaborator is a partner. Knowledge flows in both directions.

The discipline is to design relationships as partnerships where possible, dependencies where necessary, and to manage each appropriately.

---

## 3. Principles

These principles bind dependency and partnership management.

### 3.1 Honest Mapping

**DEP-001** Dependencies and partnerships are mapped honestly. The map is reviewed annually and updated as relationships change.

### 3.2 Diversification of Critical Dependencies

**DEP-002** Critical dependencies (those whose loss would significantly disrupt operations) are diversified where feasible. Single-vendor lock-in is avoided.

### 3.3 Exit Paths

**DEP-003** Critical dependencies have documented exit paths. Robotanica maintains the ability to migrate away from any dependency, even if the migration would be costly.

### 3.4 Open Source Default

**DEP-004** Where dependencies can be open source, they are. Per Charter §5.2, open formats and tools are preferred. Proprietary dependencies require justification and exit-path documentation.

### 3.5 Mission Compatibility

**DEP-005** Dependencies are evaluated for mission compatibility. Critical dependence on parties whose broader practices conflict with Charter is reduced over time per §3.3.

### 3.6 Partnership Reciprocity

**DEP-006** Partnerships are mutual. Robotanica contributes to partners as well as receiving from them. Partnerships that become unilateral extraction are reformed or ended.

### 3.7 Sovereignty Honored in Partnerships

**DEP-007** Partnerships with indigenous federations, communities, and other sovereign-claiming parties honor sovereignty. Robotanica does not subordinate partner sovereignty to operational convenience.

### 3.8 Concentration Risk Tracked

**DEP-008** Concentration of dependencies in single vendors, jurisdictions, or providers is tracked. Excessive concentration triggers diversification.

### 3.9 Vendor Lock-In Refused

**DEP-009** Dependencies that create lock-in (proprietary formats, exclusive contracts, non-portable data) are refused or replaced.

### 3.10 Public Disclosure

**DEP-010** Material dependencies and partnerships are publicly disclosed. The map itself is part of the public record.

---

## 4. Critical Infrastructure Dependencies

These are dependencies whose loss would significantly disrupt operations. Each requires explicit management.

### 4.1 Cloud Infrastructure

**Dependency:** Cloud computing platforms hosting Robotanica's platforms (Gaia, A3, OpenFactory).

**Current dependency profile:**

- Multi-cloud strategy per Technical Architecture Plan §3.6 (Kubernetes-based, portable across clouds).
- Initial deployment may concentrate in 1-2 cloud providers; migration capability designed in from start.
- Open-source orchestration (Kubernetes), GitOps (Argo CD), and other cross-cloud-portable choices.

**Risk:** Cloud provider exit, pricing shifts, regulatory action against provider, technical incident.

**Mitigation:**

- Multi-region deployment within and across clouds.
- Data portability through open formats (per Data Lifecycle Plan §5).
- Deployment portability through container orchestration.
- Documented migration runbooks tested annually.

**Partner candidates:** AWS, Google Cloud, Microsoft Azure, sovereign cloud providers, mission-aligned cloud cooperatives if they emerge at scale.

**Concentration limit:** No single cloud provider above 60% of compute/storage at any time post-Phase 1.

### 4.2 Satellite Imagery and Remote Sensing

**Dependency:** Satellite imagery for Gaia parcel monitoring, MRV verification, and outcome tracking.

**Current dependency profile:**

- **Public sources:** Sentinel-1 and Sentinel-2 (EU Copernicus program), Landsat (US Geological Survey, public free).
- **Commercial sources:** Planet, Maxar, Airbus, others where higher resolution or specific bands needed.
- **Mission-specific:** Some upcoming missions (Earth Caregivers, etc.) may provide additional public imagery.

**Risk:** Public missions retired or restricted; commercial providers raise prices or restrict access; geopolitical restrictions on imagery access.

**Mitigation:**

- Primary reliance on public Sentinel and Landsat where adequate.
- Commercial supplements where required, with multi-vendor relationships.
- Cached imagery for offline analysis where licensing permits.
- STAC catalog (per Gaia PRD) supports multi-source imagery management.

**Concentration limit:** No single commercial provider above defined fraction of imagery costs.

**Refused:** Imagery providers whose primary military or surveillance use creates ethical conflicts.

### 4.3 Foundation Models for AI Agents

**Dependency:** Foundation language and vision models underlying Robotanica's AI agents.

**Current dependency profile:**

- AI agents use foundation models from major providers per AI Ethical Review Framework.
- Models change rapidly; deprecation risk is real and ongoing.
- Open-source alternatives (Llama, Mistral, others) maturing as fallbacks.

**Risk:** Model deprecation, pricing shifts, capability changes affecting agent behavior, model provider exit, regulatory action.

**Mitigation:**

- Multi-model strategy where feasible.
- Open-source model evaluation and deployment as fallback.
- Agent design abstracted from specific model details.
- Model selection reviewed per AI Ethical Review Framework §15.5.

**Concentration limit:** Critical agent functionality not tied to any single foundation model provider.

**Sovereignty consideration:** Foundation models trained on data without indigenous and community consent raise sovereignty questions per Plurality of Knowledge Protocol. Use is reviewed accordingly.

### 4.4 Scientific Databases

**Dependency:** Reference scientific databases for taxonomy, ecology, climate, and other domains underlying Codex content.

**Critical databases:**

- GBIF (biodiversity occurrence records).
- Catalogue of Life (taxonomic backbone).
- IUCN Red List (species conservation status).
- TRY plant trait database.
- IPCC/CMIP climate projection data.
- World Soil Information (ISRIC).
- Various national and regional ecological databases.

**Risk:** Database closure, terms changes, funding loss, data quality degradation.

**Mitigation:**

- Multiple sources where possible.
- Local caching of critical reference data with appropriate update cycles.
- Codex resilience to upstream changes (not assuming any single database is permanent).
- Contributing to database sustainability through funding or technical support where feasible.

**Partnership opportunities:** Robotanica contributes data back to databases that accept contributions, supporting their sustainability.

### 4.5 Identity and Security Infrastructure

**Dependency:** Identity providers, certificate authorities, secrets management.

**Current dependency profile per Technical Architecture Plan §3.1:**

- OIDC for human identity (open standard, multiple providers).
- SPIFFE for service identity (open standard).
- HashiCorp Vault for secrets management.
- Standard Internet Public Key Infrastructure for certificates.

**Risk:** Vault provider issues; certificate authority compromise; identity provider exit.

**Mitigation:**

- Open standards reduce lock-in.
- Multiple certificate authorities considered.
- Hardware-backed signing keys where feasible.
- Documented migration paths.

### 4.6 Communication Infrastructure

**Dependency:** Email, messaging, video conferencing, document collaboration.

**Current dependency profile:**

- Various commercial providers, with some federation member preference variability.
- Open-source alternatives (Element/Matrix, Mattermost) considered for sensitive communications.

**Risk:** Vendor-related risks; data subpoena and legal access issues.

**Mitigation:**

- Sensitive communications (governance, FPIC, dispute) use systems with appropriate confidentiality.
- Avoid lock-in by using portable formats.
- Some communications via open-source self-hosted infrastructure.

### 4.7 Financial and Payment Infrastructure

**Dependency:** Banks, payment processors, accounting software, treasury management.

**Current dependency profile:**

- Banking relationships in multiple jurisdictions.
- Payment processors for credit market and partnership payments.
- Standard accounting and treasury software.

**Risk:** Banking exit; payment processor refusal of mission-related transactions; accounting software vendor issues.

**Mitigation:**

- Multiple banking relationships across jurisdictions.
- Multiple payment processor capabilities.
- Mission-aligned banking where viable (community development banks, cooperative banks).
- Standards-based accounting permitting software portability.

**Refused:** Financial institutions whose primary practices are categorically refused per Funding Strategy §5.

### 4.8 Logistics and Transportation

**Dependency:** Shipping, transportation, customs, supply chain for biological materials, equipment, and personnel.

**Current dependency profile:**

- Standard commercial shipping providers.
- Specialized biological material shipping where needed.
- Local logistics partners in operating regions.

**Risk:** Shipping disruption (geopolitical, climate, pandemic); biological material customs restrictions; specialized cargo handler exit.

**Mitigation:**

- Local production where possible (per OpenFactory regional facilities).
- Multiple logistics partners.
- Buffer stock and reserves for critical materials.

### 4.9 Software and Infrastructure Dependencies

**Dependency:** Open-source projects underlying the technical stack (PostgreSQL, Kafka, Kubernetes, etc.).

**Risk:** Project discontinuation, license change, security vulnerability without timely patch, hostile fork, governance compromise.

**Mitigation:**

- Choose well-governed projects with multiple maintainers.
- Contribute to project sustainability through code, documentation, funding.
- Track project health.
- Maintain forks if upstream becomes problematic.

**Specific concentrations to monitor:** Most critical OSS projects depend on small core teams. Robotanica's contribution to project sustainability is mission-aligned.

---

## 5. Critical Partnerships

These are partnerships — mutual relationships — distinct from dependencies. Partnership health affects operations but is not single-point-of-failure.

### 5.1 Indigenous Federations and Councils

**Partnership category:** Indigenous federations representing communities Robotanica works with or might work with.

**Examples** (illustrative):

- COICA (Coordinator of Indigenous Organizations of the Amazon River Basin).
- COIAB (Coordination of Indigenous Organizations of the Brazilian Amazon).
- AIPP (Asia Indigenous Peoples Pact).
- Regional indigenous councils.
- National indigenous representative bodies.

**Mutuality:**

- Robotanica receives: cultural and ecological knowledge, partnership in restoration, sovereignty over indigenous lands engaged.
- Indigenous federations receive: support for their priorities, restoration of degraded lands, capacity, recognition.

**Risk to relationship:** Cultural mismatches, sovereignty conflicts, overcommitment, leadership changes on either side.

**Discipline:** Per Charter §3.3, Plurality of Knowledge Protocol, Public Communication Doctrine §13. Communities and federations lead; Robotanica supports.

### 5.2 Scientific Institutions

**Partnership category:** Universities, research institutes, herbaria, and scientific organizations relevant to restoration ecology.

**Examples** (illustrative):

- Universities with restoration ecology programs.
- IUFRO (International Union of Forest Research Organizations).
- Society for Ecological Restoration.
- Indigenous-led research institutions.
- Regional research centers in operating bioregions.

**Mutuality:**

- Robotanica receives: scientific expertise, data, methodology contributions.
- Scientific institutions receive: research opportunities, real-world data, funding for restoration-related research.

**Risk to relationship:** Funding instability of institutions, IP and authorship conflicts, alignment drift.

**Discipline:** Open scientific publication; appropriate authorship; no proprietary lock-in; institutional sustainability supported where appropriate.

### 5.3 Conservation Organizations

**Partnership category:** Mission-aligned conservation NGOs, working in landscapes Robotanica restores.

**Examples** (illustrative, not endorsements):

- WWF, Conservation International, Nature Conservancy (large international NGOs with often-aligned but sometimes-misaligned approaches).
- BirdLife International, regional conservation networks.
- Locally-led conservation organizations.
- Indigenous-led conservation networks.

**Mutuality:**

- Robotanica receives: landscape-level conservation context, advocacy alignment, operational partnership in some regions.
- Conservation organizations receive: restoration capacity in their landscapes, methodology contributions, partner in policy advocacy.

**Risk to relationship:** Strategy divergence, governance differences, NGO capture concerns, scale mismatches.

**Discipline:** Selective alignment per principle and practice; refusal to partner with organizations whose practices conflict with Charter; willingness to coordinate without merging.

### 5.4 Government Counterparts

**Partnership category:** Government agencies (national and subnational) responsible for environmental, restoration, indigenous affairs, and related portfolios.

**Examples per region:**

- National environment ministries.
- Forest service equivalents.
- Indigenous affairs agencies.
- Regional environmental agencies.
- Local governments where relevant.

**Mutuality:**

- Robotanica receives: regulatory permission, public funding access, scientific data sharing.
- Government partners receive: restoration outcomes contributing to their objectives, technical capacity.

**Risk to relationship:** Political change, leadership turnover, policy shifts, jurisdictional conflicts.

**Discipline:** Per Regulatory Engagement Strategy. Engagement is bilateral and limited; politics is acknowledged but not endorsed.

### 5.5 Multilateral Institutions

**Partnership category:** Multilateral funders and policy bodies.

**Examples:**

- Green Climate Fund.
- Global Environment Facility.
- World Bank Forest Carbon Partnership.
- Regional development banks.
- UN agencies (UNEP, UNDP, FAO).

**Mutuality:**

- Robotanica receives: funding, policy platform, multilateral legitimacy.
- Multilateral institutions receive: implementation partner, restoration capacity, accountable use of funding.

**Risk to relationship:** Shifting institution priorities, conditionality conflicts with mission.

**Discipline:** Per Funding Strategy. Funding accepted only where conditions are compatible.

### 5.6 Civil Society Allies

**Partnership category:** Mission-aligned civil society organizations.

**Examples:**

- Environmental advocacy organizations.
- Climate justice movements.
- Land rights movements.
- Open-source and free knowledge movements.

**Mutuality:**

- Robotanica receives: advocacy support, public legitimacy, coalition reach.
- Civil society receives: a credible restoration project to support, data and evidence, alignment in shared advocacy.

**Risk to relationship:** Strategic divergence, internal civil society conflicts, alignment drift.

**Discipline:** Selective coalition participation; respect for civil society's distinctness; no co-optation.

### 5.7 Federation Members

**Partnership category:** All Federation members per Federation Membership Agreement.

This is the most operational partnership category. The Federation Membership Agreement details its terms.

### 5.8 Verifier Networks

**Partnership category:** Independent verification organizations and networks.

**Examples:**

- Established carbon market verifiers (DOEs in CDM context, validation/verification bodies in voluntary markets).
- Emerging restoration-specific verifier organizations.
- Indigenous-led verification networks.
- Academic verification programs.

**Mutuality:**

- Robotanica receives: independent verification.
- Verifier networks receive: work, methodology development, market presence.

**Discipline:** Per MRV §7. Independence is structural; verifier network must remain genuinely independent of Robotanica.

### 5.9 Other Restoration Practitioners

**Partnership category:** Other restoration projects and federations operating in similar bioregions or with similar discipline.

**Mutuality:**

- Mutual learning, methodology sharing, coalition advocacy, peer review.

**Discipline:** Cooperative not competitive. Robotanica does not seek to dominate the restoration space; multiple federations and projects strengthen the field.

### 5.10 Funders and Funding Networks

**Partnership category:** Foundations, individual funders, mission-aligned funder networks.

**Mutuality:**

- Robotanica receives: capital.
- Funders receive: mission impact, learning, transparent reporting.

**Discipline:** Per Funding Strategy. Funder relationships are partnerships, not patron-client structures.

---

## 6. Concentration and Diversification

Beyond category-specific risks, concentration patterns affect overall risk.

### 6.1 Geographic Concentration

**CONC-001** Operations, partnerships, and dependencies are tracked by geography:

- No single country above defined fraction of operations or capital.
- No single region above defined fraction.
- Bioregional diversification per Bioregional Strategy.

### 6.2 Vendor Concentration

**CONC-010** Vendor concentration tracked across categories:

- Cloud, satellite, foundation models, scientific databases.
- No single vendor above defined fraction of dependency in any critical category.

### 6.3 Relationship Concentration

**CONC-020** Relationship concentration tracked:

- No single partner organization holds disproportionate influence.
- No single category of partner dominates the relationship portfolio.

### 6.4 Funding Concentration

**CONC-030** Per Funding Strategy §3.1 and Founding Capital Plan §5: funder concentration limits enforced.

### 6.5 Personnel Concentration

**CONC-040** Knowledge and capability concentration in individuals tracked:

- Critical knowledge documented to avoid single-person dependencies.
- Succession planning for key roles.
- Knowledge transfer ongoing.

### 6.6 Concentration Reviews

**CONC-050** Annual concentration review by Stewardship Office:

- Identifies emerging concentrations.
- Plans diversification where warranted.
- Acknowledges where concentration is transitional and acceptable.

---

## 7. Exit Paths

Each critical dependency has a documented exit path.

### 7.1 What an Exit Path Includes

**EXIT-001** A documented exit path includes:

- The specific dependency.
- Alternative providers or technologies.
- Migration cost estimate.
- Migration time estimate.
- Triggering conditions (when migration would be initiated).
- Pre-migration testing approach.

### 7.2 Exit Path Maintenance

**EXIT-010** Exit paths are reviewed annually:

- Are alternatives still viable?
- Have migration costs changed materially?
- Have triggering conditions arisen?

### 7.3 Pre-Migration Testing

**EXIT-020** Where critical, exit paths are tested without full migration:

- Technical compatibility verified.
- Performance assessed.
- Mock migrations conducted at appropriate cadence.

### 7.4 Exit Path Triggers

**EXIT-030** Exit path execution may be triggered by:

- Vendor exit or significant pricing change.
- Vendor mission incompatibility per §3.5.
- Technical inadequacy.
- Concentration risk per §6.

### 7.5 Communicated Exit Paths

**EXIT-040** Critical exit paths are communicated:

- Internal: documented for the operations team.
- Federation: shared with federation members where dependencies are shared.
- Public: high-level acknowledgment that exit paths exist for major dependencies.

---

## 8. Partnership Health

Partnership management is distinct from dependency management.

### 8.1 Partnership Health Indicators

**PART-001** Partnership health is monitored across:

- Mutual contribution and benefit.
- Communication frequency and quality.
- Alignment on principles and practices.
- Conflict resolution effectiveness.
- Long-term commitment from both sides.

### 8.2 Partnership Reviews

**PART-010** Major partnerships undergo periodic review:

- Annual: routine partnerships.
- 5-year: comprehensive review of major partnerships.
- Triggered: when material changes occur.

### 8.3 Partnership Endings

**PART-020** Partnerships sometimes end:

- Honestly when ending.
- Through governance, not by drift.
- With acknowledgment to both parties.
- With learning captured.

### 8.4 New Partnership Formation

**PART-030** New partnerships:

- Require alignment on Charter and Federation Membership Agreement principles where applicable.
- Receive Stewardship Office review for major partnerships.
- Are publicly disclosed where material.

---

## 9. Specific Partnership Categories Discipline

### 9.1 Indigenous Federation Partnerships

Indigenous federations and councils operate as autonomous bodies. Robotanica:

- Does not become a clearinghouse for indigenous knowledge across federations.
- Engages each on their terms and through their governance.
- Respects inter-federation boundaries that they establish.
- Supports their broader work where consistent and consented.

### 9.2 Scientific Institution Partnerships

Academic and research institutions vary substantially in mission, governance, and approach. Partnerships:

- Are with specific programs and people, not entire institutions.
- Document clear mutual contribution.
- Respect institutional norms (publication rights, IP, attribution).
- Avoid institutional dependency on single research relationships.

### 9.3 Multilateral and Government Partnerships

Multilateral and government partnerships are heavily formalized. Robotanica:

- Maintains diplomatic relationships through designated representatives.
- Honors formal commitments rigorously.
- Distinguishes operational compliance from political endorsement.
- Operates legally even where in disagreement with policy.

### 9.4 Conservation NGO Partnerships

Conservation NGOs vary substantially in approach and scale. Robotanica:

- Selects partners per Charter alignment, not institutional prestige.
- Recognizes that some large NGOs have practices conflicting with Charter (e.g., enclosure-style conservation displacing communities).
- Refuses partnerships that require alignment with such practices.
- Engages locally-led and community-led conservation organizations preferentially.

---

## 10. Open Source Community Engagement

Open source project dependencies require specific engagement.

### 10.1 Engagement as Stewardship

**OSS-001** Open source projects on which Robotanica depends are engaged as stewardship, not consumption:

- Bug reports and fixes contributed back.
- Feature improvements proposed and contributed.
- Documentation supported.
- Funding for project sustainability where appropriate.

### 10.2 Project Health Tracking

**OSS-010** Open source project health is tracked:

- Maintainer activity and diversity.
- Security responsiveness.
- Governance health.
- License stability.
- Funding adequacy.

### 10.3 Project Sustainability Support

**OSS-020** Where Robotanica's dependence on a project is significant:

- Funding contribution to project sustainability.
- Personnel time contribution where mission-aligned.
- Public acknowledgment of dependence.

### 10.4 Refusal of License Capture

**OSS-030** Robotanica does not contribute to projects that subsequently relicense to non-open licenses. Where this risk exists, contributions are structured to maintain open availability.

---

## 11. Dependencies of Federation Members

Federation members have their own dependencies. Robotanica's discipline applies to its institutional dependencies; member dependencies are members' own concern.

### 11.1 Indirect Dependencies

**MEM-001** Where federation member dependencies create indirect dependence for Robotanica (operator dependency on specific equipment vendor; verifier dependency on specific tools), this is acknowledged.

**MEM-002** Robotanica supports member capacity and resilience but does not direct member operational choices.

### 11.2 Member Sustainability

**MEM-010** Robotanica considers member sustainability in federation health:

- Supporting members' viability as part of federation health.
- Refusing arrangements that would unsustainably extract from members.
- Capacity building to strengthen member sustainability.

---

## 12. Sovereignty in Partnerships

Sovereignty (per Charter §3.3 and Plurality of Knowledge Protocol) extends to partnerships.

### 12.1 Indigenous Sovereignty Structural

**SOV-001** Indigenous federations and communities exercise sovereignty over partnership decisions. Robotanica does not direct partnership scope; communities determine what partnership means for them.

### 12.2 Federation Member Sovereignty

**SOV-010** Federation members operate under their own governance within federation principles. Partnership terms respect member governance.

### 12.3 Partner Sovereignty in Communications

**SOV-020** Public communication about partnerships honors partner sovereignty per Public Communication Doctrine §13. Partners speak for themselves.

### 12.4 Refusal to Trade Sovereignty for Partnership

**SOV-030** Robotanica does not seek partnerships requiring sovereignty compromise. Partners with sovereignty are engaged as sovereign; their consent is structural.

---

## 13. Risk Concentration Analysis

This section identifies concentration risks worth highlighting.

### 13.1 Cloud Concentration

Even with multi-cloud strategy, a small number of providers serve almost all cloud computing globally. The market itself is concentrated. Mitigation through internal multi-vendor doesn't solve market-level concentration.

### 13.2 Foundation Model Concentration

Foundation AI models are produced by a handful of providers. This is a market-level concentration that Robotanica's individual choices cannot solve. Open-source alternatives reduce dependence but don't eliminate concentration.

### 13.3 Satellite Imagery Concentration

Public satellite imagery is concentrated in a few national programs. Commercial imagery is concentrated in a few major providers. Robotanica's multi-source strategy mitigates but doesn't eliminate this concentration.

### 13.4 Acknowledgment

These concentrations are real and partly outside Robotanica's control. Acknowledging them is honest. Mitigation extends as far as Robotanica's choices reach; beyond that, the concentrations are structural conditions of operation.

---

## 14. Governance

### 14.1 Dependency and Partnership Governance

**GOV-001** Dependencies and partnerships are governed by:

- **Stewardship Office** for routine relationships and operational dependencies.
- **Federation governance** for major partnerships and structural decisions.
- **Funding Committee** for funding-related dependencies.
- **AIERB** for AI infrastructure dependencies.

### 14.2 Annual Review

**GOV-010** Stewardship Office publishes annual review:

- Critical dependencies and concentration metrics.
- Partnership health summary.
- Concentration risks identified.
- Diversification progress.
- Material changes during the year.

### 14.3 Material Change Communication

**GOV-020** Material changes (new critical dependencies, major partnership formation or ending) are communicated:

- Internal: to operations and governance.
- Federation: to affected members.
- Public: per Public Communication Doctrine.

---

## 15. Open Questions

These are unresolved questions in dependency and partnership management:

- **Cloud sovereignty.** Whether dependence on specific cloud providers compatible with sovereign data control in operating regions becomes infeasible. Sovereign cloud alternatives are emerging but limited.
- **AI model dependency evolution.** Foundation model landscape may shift substantially over project horizon. Long-term strategy requires ongoing adaptation.
- **Inter-federation partnerships.** When federation forks (per Charter §5.4) emerge, inter-federation partnership protocols are needed but unspecified.
- **Indigenous federation engagement scaling.** Engaging hundreds of indigenous federations and communities at scale operationally is complex. Patterns and protocols need development.
- **Conservation NGO sector dynamics.** Major conservation NGOs face their own challenges (funding, governance, indigenous rights). Robotanica's posture toward these organizations is selective; specific cases are evaluated as they arise.
- **Open source project funding obligations.** As Robotanica scales, contribution to open source project sustainability scales. Specific funding allocation discipline needs refinement.
- **Government partnership in changing politics.** Government partnerships span political cycles. Building and maintaining relationships through political shifts requires sustained attention.
- **Partnership-dependency boundaries.** Some relationships start as partnerships and become dependencies, or vice versa. Boundary management is judgment-based.
- **Vendor-client power asymmetry.** Robotanica is small relative to major cloud providers, foundation model providers. Vendor-client power is asymmetric. Negotiating power grows with scale; pre-scale, alternative arrangements may be needed.

---

## Appendix A — Critical Dependency Summary

| Dependency | Concentration Limit | Exit Path | Risk Level |
|---|---|---|---|
| Cloud infrastructure | <60% single provider | Container portability | Moderate |
| Satellite imagery | Multi-source | Public + commercial mix | Lower |
| Foundation AI models | Multi-model | Open-source fallback | Higher |
| Scientific databases | Local caching | Multi-source | Lower |
| Identity / Security | Open standards | Standard protocols | Lower |
| Communication | Multi-vendor | Open alternatives | Lower |
| Banking and finance | Multi-jurisdictional | Alternative providers | Lower |
| Logistics | Multi-vendor | Local where possible | Moderate |
| Open-source projects | Diversified | Maintained forks | Variable |

---

## Appendix B — Critical Partnership Categories

| Category | Mutuality Type | Discipline |
|---|---|---|
| Indigenous federations | Sovereignty respect | Charter §3.3 |
| Scientific institutions | Knowledge exchange | Open publication |
| Conservation NGOs | Selective coalition | Per principle |
| Government counterparts | Operational cooperation | Per Regulatory Engagement |
| Multilateral institutions | Funding + policy | Per Funding Strategy |
| Civil society | Coalition advocacy | Per principle |
| Federation members | Federation framework | Federation Membership Agreement |
| Verifier networks | Independent verification | Per MRV §7 |
| Other restoration practitioners | Mutual learning | Per principle |
| Funders | Capital + reporting | Per Funding Strategy |

---

## Appendix C — Cross-References

- **Robotanica Charter** §3.3 (commitments to communities), §5 (openness)
- **Technical Architecture Plan** (technology choices producing dependencies)
- **Threat Model** (failure modes including dependency failures)
- **Funding Strategy** (funder relationships as partnerships)
- **Federation Membership Agreement** (member relationships)
- **Public Communication Doctrine** §13 (partnership voice)
- **Plurality of Knowledge Operational Protocol** (indigenous partnerships)
- **Regulatory Engagement Strategy** (government relationships)
- **Insurance and Liability Architecture** (allocation of risk in relationships)
- **AI Ethical Review Framework** (foundation model dependencies)

---

## Appendix D — Glossary (Dependency-Specific)

- **Concentration risk** — Risk arising from disproportionate dependence on a single party.
- **Critical dependency** — A dependency whose loss would significantly disrupt operations.
- **Dependency** — A relationship where Robotanica relies on another party for something it cannot easily replace.
- **Exit path** — A documented plan for migrating away from a dependency.
- **Lock-in** — A dependency structure that makes migration prohibitively expensive.
- **Mutuality** — The bidirectional contribution and benefit that distinguishes partnership from dependency.
- **Open source default** — The principle that dependencies are open-source where viable.
- **Partnership** — A mutual relationship with bidirectional contribution.
- **Single point of failure** — A dependency whose loss disrupts operations without backup.

---

*Robotanica operates within an ecosystem of dependencies and partnerships that it does not control. Pretending otherwise would be dishonest. Naming the dependencies, managing them through diversification and exit paths, and building partnerships on mutual terms is the discipline. The map is the work of acknowledgment; the management is the work of resilience.*
