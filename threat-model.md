# Threat Model and Adversarial Analysis

## Specification (v0)

**Document type:** Adversarial analysis and risk specification
**Status:** Draft for review by leadership, Science Council, and Stewardship Office
**Companion documents:** Robotanica Charter, all platform PRDs, Stewardship Lease Requirements, MRV Specification

---

## 1. Purpose and Status

This document names the ways Robotanica could fail. It is the structured adversarial analysis of the project: who would attack it, how, why, and what protects it.

The document exists because every prior document — the Charter, the PRDs, the Lease Requirements, the MRV Specification — describes Robotanica as it is intended to operate. None of them adequately stress-test what happens when actors try to break, capture, or weaponize it. A project committing to multi-decade stewardship of land it does not own, in jurisdictions it does not control, with technologies that will be replaced, in a political and ecological climate that will shift unpredictably, must reason adversarially about its own failure modes.

The document is uncomfortable. That is its point. It names threats that are usually unspoken in mission-driven organizations because naming them is awkward, embarrassing, or politically costly. Robotanica's commitment to transparency (Charter §2.9) and to the Charter's broader discipline requires that the threats be named anyway.

This document is not a finished analysis. It is a starting structure. It is reviewed annually and updated when material new threats are identified.

---

## 2. Methodology

### 2.1 Approach

The analysis proceeds by:

1. **Enumerating adversaries** — who has motive to harm, capture, or weaponize Robotanica.
2. **Enumerating threat surfaces** — which parts of Robotanica are exposed to which adversaries.
3. **Detailing attack scenarios** — concrete narratives of how adversaries might act.
4. **Mapping mitigations** — what existing structural protections defend against each scenario, and where gaps remain.
5. **Surfacing residual risk** — what cannot be fully mitigated and must be accepted, monitored, or escalated.

### 2.2 Scope

The analysis covers:

- **Adversarial actors** — those who deliberately seek to harm Robotanica.
- **Extractive actors** — those who seek to use Robotanica for purposes incompatible with the mission.
- **Internal failure modes** — drift, capture, and decay from within.
- **Structural failures** — failures of design that no specific actor causes but that the structure permits.
- **Catastrophes** — events outside any actor's control that the project must survive.

The analysis does not cover routine operational risk (the standard category of risk register entries) except where it has adversarial dimensions.

### 2.3 Honest Limitations

This document is written by parties with skin in the game. Authors are inside the system they are analyzing. The strongest critique comes from outside; this document invites it.

Further, the most consequential threats are usually the ones not yet imagined. The categories below are an enumeration of known threats. The unknown ones are the risk this document does not directly reduce.

---

## 3. Adversaries

### 3.1 Industries Threatened by Restoration

Restoration at scale displaces extractive industries: industrial agriculture on degraded land, logging, fossil-fuel extraction at restoration sites, mining, certain forms of livestock production. These industries have legal, political, and economic capacity to oppose Robotanica.

Their tactics include legal challenge to Lease validity, regulatory pressure in jurisdictions where they hold influence, public-relations campaigns framing Robotanica as anti-development or anti-livelihood, infiltration of federation membership to surface or fabricate scandal, lobbying against credit market participation, and (in worst cases) physical interference with restoration sites.

The threat is real but bounded by Robotanica's structural transparency and federation breadth. A campaign against Robotanica is also a campaign against thousands of federation members, indigenous communities, and Landowners.

### 3.2 Hostile State Actors

Some governments will oppose Robotanica for reasons that include: incompatibility with development plans, perceived foreign influence, alignment with opposition political movements, suspicion of indigenous land-rights organizing, or simple authoritarian preference for centralized control.

Tactics include expropriation of land or operations, expulsion of personnel, regulatory shutdown, criminalization of federation members, surveillance of stewards and communities, and (in worst cases) violence against personnel.

This is the threat the federation structure most directly addresses: Robotanica must remain operable when individual jurisdictions become hostile, with succession protocols (Lease §6.5, Charter §7.3) that protect Landowners and communities even when Robotanica itself cannot operate locally.

### 3.3 Hostile Acquirers and Asset-Strippers

Robotanica's stewardship leases, credit reserves, biological IP (kept open per Charter §5.3 but still valuable), and platform infrastructure represent significant economic value. Financial actors will see this and seek to capture it through acquisition, hostile board changes, or pressure on funders to install pliable leadership.

The Charter's un-amendable provisions (§8.1) and the dissolution discipline (§7.4) are the structural defenses. The threat manifests as pressure to make those provisions amendable.

### 3.4 Greenwashing Partners

Major emitters and extractive companies will offer to fund Robotanica in exchange for branding rights, offset claims, or association that improves their public position without changing their actual practices. The offers will be lucrative and seductive, and they will be made by people who genuinely believe the partnership is helpful.

The threat is not the bad-faith greenwasher — those are easy to refuse. The threat is the partnership that looks good on paper, fits within the rules as written, and over time normalizes the use of Robotanica's credibility for purposes incompatible with the mission. The first such partnership sets a precedent for the next.

### 3.5 Bad-Faith Critics

Some critique of Robotanica will be in good faith and welcomed. Some will be bad-faith: paid campaigns to undermine the project, ideological actors opposed to ecological restoration on principle, or competitors using critique as a market tactic.

Distinguishing good-faith from bad-faith critique is itself a threat surface: dismissing legitimate critique as bad-faith is a failure mode; treating bad-faith critique as legitimate burns time and credibility. The Charter's commitment to transparency reduces this threat by making the underlying record available; it does not eliminate it.

### 3.6 Federation Insiders Acting in Bad Faith

Operators may misreport outcomes, falsify FPIC, or collude with verifiers. Scientists may submit recipes that serve their commercial interests. Stewardship Office staff may favor preferred Landowners. Federation members may use access to Gaia for unauthorized data extraction.

These threats are pervasive and cannot be eliminated; the discipline is to make them detectable and to respond predictably when detected. Verifier independence (MRV §7), audit trail immutability (A3 §6.9, Gaia §7.3), and graduated sanctions (Charter §6.4) are the structural responses.

### 3.7 Founders and Early Leadership

Founders are an adversary class. Not because they are malicious, but because:

- Their attachment to the project's early form may resist necessary evolution.
- Their personal reputation is tied to specific outcomes, biasing decisions toward favorable reporting.
- Their equity, influence, or ego may attract acquirers, governments, or partners they should refuse.
- Their successors face pressure to either preserve or repudiate founder choices, neither of which may be the right answer.

The Charter's un-amendable provisions, the Stewardship Office's structural insulation, and the Science Council's veto authority are designed in part to protect Robotanica from its own founders, not just from external adversaries.

### 3.8 Single-Point Funders

A single funder providing a disproportionate share of Robotanica's capital becomes an adversary by virtue of leverage, regardless of intent. Funding decisions become mission decisions. Withdrawal threats become governance threats.

This is structurally addressed through funding diversity (a topic for the forthcoming Funding Strategy document) and through the Charter's refusal-of-incompatible-funding provision (§3.6). It cannot be fully eliminated.

### 3.9 Adversarial Users of Platforms

Platforms create attack surface. A3 invites Sybil-style attacks on the marketplace and governance; Gaia invites data poisoning, false observation injection, and unauthorized extraction; OpenFactory invites supply-chain compromise of robots and biological inputs. Each attack pattern requires platform-specific defenses (covered in §5).

### 3.10 Communities and Landowners Acting Against the Project

Communities and Landowners may, with full justification, decide that Robotanica's continued presence is not in their interest. This is not adversarial behavior in a moral sense — it is the legitimate exercise of sovereignty. But it is a category of threat to project continuity.

The Charter's stewardship-not-ownership commitment, Lease termination rights, and consent-revocation procedures (A3 §6.4) make this threat acceptable: Robotanica must operate in a way where community or Landowner withdrawal is honored, not resisted.

---

## 4. Threat Categories

### 4.1 Mission Drift

The most consequential threat is not external attack but internal drift: the slow accumulation of small compromises that, over decades, erode the principles of the Charter. Mission drift is hard to detect because each step seems reasonable; it is hard to reverse because the new state is normalized.

Drift vectors include:

- **Metric drift** — reporting metrics that look favorable replacing metrics that test the mission.
- **Partner drift** — accepting partners whose other activities are incompatible with the mission, justified by their capital or capacity.
- **Recipe drift** — selecting recipes that are operationally easier (monoculture, exotic fast-growing species) over recipes that match ecological best practice.
- **Governance drift** — decisions migrating from public to private, from collective to individual, from documented to undocumented.
- **Transparency drift** — failure reporting becoming softer, qualified, eventually omitted.
- **Sovereignty drift** — indigenous and community sovereignty becoming procedural rather than structural.

The Charter, Science Council, Stewardship Office, and un-amendable provisions are the structural defenses. The annual Charter review (§8.2) is one detection mechanism. External critique (§3.5) is another.

### 4.2 Greenwashing Capture

Greenwashing capture is mission drift weaponized. Robotanica becomes a tool by which other actors launder their environmental reputation while continuing harmful practices.

Capture happens through:

- Funding partnerships that grant the funder claim to Robotanica's outcomes.
- Credit purchases by emitters who use them to offset rather than reduce.
- Co-branded initiatives that imply endorsement of the partner's broader practices.
- Personnel exchanges that bring greenwashing-aligned advisors into the project.
- Academic partnerships that produce favorable studies tied to ongoing emissions.

The Charter's funding-refusal provision and the MRV Specification's reconciliation discipline reduce but do not eliminate this. The strongest defense is reputation: Robotanica's consistent willingness to refuse partnerships becomes a deterrent.

### 4.3 Governance Capture

Governance capture is the gradual replacement of independent governance bodies with actors aligned to particular interests. The Science Council becomes dominated by a single methodology school. The Stewardship Office is restructured into a product function. Federation governance becomes dominated by the largest operators.

Capture is gradual. Each appointment is reasonable. Each restructuring is justified. The end state is that the structural defenses of the Charter no longer function in practice.

The un-amendable provisions of the Charter (§8.1) cover the most foundational structures. Below that, capture is possible in principle and must be defended through:

- Multi-disciplinary composition mandates (Charter §4.2).
- Independent appointment processes that no single actor controls.
- Public records of decisions enabling external detection of capture.
- Federation-level review of governance body composition.

### 4.4 Data Integrity Compromise

Robotanica's claims rest on its data. If observations are falsified, if records are tampered with, if verification is circumvented, the entire structure becomes unreliable.

Threat vectors include:

- **Insider tampering** — staff with access alter records.
- **Observation falsification** — Operators report outcomes that did not occur.
- **Verifier collusion** — verifiers accept falsified evidence in exchange for value.
- **System compromise** — external actors gain write access through technical compromise.
- **Cryptographic decay** — old records become tamperable as cryptographic algorithms weaken over decades.

The append-only event ledgers of A3 and Gaia (A3 §7.3, Gaia §7.3) and the cryptographic chaining provide strong defenses. The MRV Specification's verification independence (§7) provides another. Algorithm agility (A3 §7.3) addresses cryptographic decay.

The residual risk is non-zero. Any system can be compromised given sufficient effort and time. Detection through redundancy and external audit is the operational defense.

### 4.5 Site-Level Catastrophe

A site can fail catastrophically through wildfire, hurricane, drought, flood, pest outbreak, contamination, or human destruction. At scale, some sites will fail in any year.

The MRV Specification's reconciliation discipline (§14), A3's reconciliation reserve (§10.3), and the Charter's transparent-failure commitment (§2.9) make site failure operationally manageable. The threat is not failure itself; it is failure mishandled — concealed, denied, or used to shift blame.

### 4.6 Climate Catastrophe Beyond Plan

Robotanica plans against current climate projections. The plans assume that climates shift but remain within bounds where current ecological knowledge applies. If climate change exceeds the assumptions — through tipping points, abrupt regional shifts, or compounding crises — Robotanica's recipes, baselines, and timelines may all become inapplicable.

This is not a threat against Robotanica specifically; it is a threat against all human planning. The defenses are: scenario planning that includes high-warming scenarios, recipe diversity that includes assisted-migration options, and structural humility in claims about long-horizon outcomes.

### 4.7 Regulatory and Legal Catastrophe

A jurisdiction can change its laws in ways that void existing Leases, prohibit Federation operation, or expropriate stewarded land. International instruments can shift in ways that change credit market structures. Litigation can challenge novel legal instruments.

The defenses are: jurisdictional diversity (no single jurisdiction is critical), conservative jurisdictional Lease variants drafted by local counsel, succession protocols that can transfer obligations to other parties, and federation structures that survive individual-jurisdiction failure.

### 4.8 Technology Catastrophe

Cryptographic algorithms weaken; storage formats become unreadable; cloud providers exit markets; geopolitical events disrupt internet infrastructure; the underlying tech stack becomes unsupported.

Defenses are: open formats for all archival data (Gaia §7.3, A3 §7.3), multi-region replication, periodic format-migration exercises, and the Charter's dissolution discipline that ensures the work can continue if Robotanica's specific technology stack cannot.

### 4.9 Civilizational Disruption

Pandemic, war, financial collapse, or other civilizational disruption can interrupt operations for years. The fifty-year horizon of stewardship leases ensures that any reasonable time-window includes such events.

The defense is operational: federation members operate locally during partition (A3 §7.5), data is durable across disruption, and the Charter's dissolution provisions ensure the work transfers if Robotanica itself does not survive.

### 4.10 AI Agent Failure Modes

The agent architecture (Gaia §7) introduces threats specific to AI systems:

- **Reward hacking** — agents optimize for measured metrics in ways that diverge from intended outcomes.
- **Recommendation bias** — agents systematically favor certain recipes, operators, or species due to training data or feedback dynamics.
- **Codex corruption** — agents submitting proposals to the codex create feedback loops that shift the knowledge base toward agent preferences.
- **Compromise** — adversaries inject prompts, poison training data, or corrupt the retrieval set.
- **Over-reliance** — operators and stewards defer to agent recommendations beyond what the evidence warrants.

Defenses include: tier-based stake limits (Gaia §7.1–7.3), human review at every codex write (A3 §6.7), agent-write provenance distinct from human-write provenance, evaluation against historical ground truth (Gaia §7.4), and agent-output logging for retrospective audit.

The residual risk is unique to AI systems: subtle alignment failures may not be detected for years, and the fix may be difficult if the failure is built into a model now-deprecated.

### 4.11 Insider Risk

Personnel risks include: bad-faith insider action, well-intentioned insider error at scale, whistleblower suppression, unsafe field conditions, founder personal compromise, and key-person dependency.

Defenses include: separation of duties for high-stakes actions, immutable audit trails, whistleblower protection (Charter §3.5), succession planning at every leadership level, and structural distribution of knowledge to prevent dangerous concentration.

### 4.12 Threats to People

Field stewards in conflict zones, indigenous community representatives advocating against extractive interests, whistleblowers, and other personnel may face physical danger as a consequence of their work.

This threat cannot be designed away. The Charter's commitment to its people (§3.5) operationalizes as: physical security protocols where warranted, legal support, evacuation provisions, refusal to operate in conditions that endanger personnel beyond bounds the personnel themselves accept, and refusal to ask any individual to sacrifice their life or health to the mission.

---

## 5. Platform-Specific Threats

### 5.1 Gaia

| Threat | Vector | Mitigation |
|---|---|---|
| False observation injection | Compromised operator account; compromised sensor; insider | Cryptographic event signing; provenance per observation; cross-source corroboration; anomaly detection on observation streams |
| Sensitive location exposure | API misuse; insider leak; aggregation attack | Coarsening in public APIs; sovereignty-aware access controls; audit logging; differential-privacy techniques for aggregate queries |
| Codex corruption | Bad-faith contributor; agent feedback loop | Proposal-review-merge protocol; Council veto; agent-write distinct provenance; revision history immutable |
| Knowledge graph manipulation | Targeted edits to influence recipe selection | Cross-reference verification; revision review SLAs; contestation protocol |
| Long-term data loss | Format obsolescence; storage failure; jurisdictional shutdown | Open formats; multi-region replication; archival migration exercises |
| Cryptographic decay | Algorithm weakening over decades | Algorithm agility; key rotation; periodic re-signing of critical archives |

### 5.2 A3

| Threat | Vector | Mitigation |
|---|---|---|
| Lease fraud | Forged consent; fabricated FPIC; impersonation | Multi-party consent ceremony; signing key verification; community-side verification of FPIC; recording with public registries |
| Sybil marketplace attacks | Fake operator accounts | Federation membership vetting; verified credentials; performance history; manual review for new entrants |
| Credit over-issuance | Operator-verifier collusion; methodology gaming | Hard refusal of unverified issuance; reconciliation discipline; cross-verification; reconciliation reserve |
| Governance vote manipulation | Capture of governance bodies | Multi-disciplinary composition; un-amendable Charter provisions; public records |
| Reconciliation evasion | Hiding site failures to preserve credits | Mandatory reporting cadence; verifier independence; whistleblower channels; audit trail immutability |
| Indigenous sovereignty breach | Decisions made without proper FPIC | FPIC as structural workflow; community-side verification; consent revocation rights |
| Token speculation (if tokens introduced) | Crypto-market dynamics distorting governance | Refusal to introduce tokens for governance; tokens (if any) restricted to credit market interface |

### 5.3 OpenFactory

| Threat | Vector | Mitigation |
|---|---|---|
| Supply chain compromise | Malicious components in robot fabrication; compromised firmware | Verified component sourcing; supply chain attestation; firmware signing; runtime integrity checks |
| Biological contamination | Pathogen introduction in nursery or inoculant production | Biosecurity protocols; batch genealogy; quarantine procedures; multi-source production for critical inputs |
| Robot tampering | Field robots compromised to falsify observations or cause harm | Edge integrity checks; perception cross-verification; operational-bound enforcement; remote disable capability |
| Production data manipulation | False batch records; falsified genealogy | Append-only batch records; cross-system reconciliation with Gaia; ERPNext audit trail |
| Worker safety | Field operations in dangerous conditions | Safety protocols; refusal authority for field workers; insurance and support |
| Genetic drift | Inadvertent or deliberate deviation from intended genetic stock | Batch traceability to seed source; periodic genetic verification; codex-bound species references |

---

## 6. Detailed Adversarial Scenarios

### 6.1 The Friendly Acquisition

A well-funded entity with strong environmental branding offers to acquire Robotanica. The terms are generous: leadership retained, mission preserved on paper, expanded resources for the work. The acquirer's other holdings are mostly compatible with the mission. Refusal seems ungrateful and may cost Robotanica the relationship and the resources it would bring.

**How this fails Robotanica:** The acquirer's quarterly accountability and equity holders introduce pressures incompatible with the multi-decade horizon. Mission preservation on paper does not survive operational integration. Within five to ten years, mission drift accumulates to capture.

**Existing defenses:** Charter §2.3 (stewardship not ownership), §3.6 (refusal of incompatible funding), §8.1 (un-amendable provisions including stewardship-not-ownership). The federation structure means an acquirer cannot acquire what it values most — the federation members and indigenous partnerships — only the central organization.

**Residual risk:** High. Acquisition pressure compounds over decades. The structural defenses depend on leadership willing to refuse. The Charter is the strongest defense, and the un-amendable provisions are designed for exactly this scenario.

**What to do now:** Public commitment to acquisition refusal as part of the founding posture. Reputation as a project that cannot be acquired is the operational form of the structural defense.

### 6.2 The Greenwashing Partnership

A major fossil-fuel company offers $500M over ten years to fund restoration in exchange for: co-branded initiatives, prominent placement of their logo on outcome reports, and public statements that the company is "investing in nature-based climate solutions." They commit to no operational changes in their core business. They emphasize the funds will plant millions of additional trees that would not otherwise exist.

**How this fails Robotanica:** The partnership normalizes fossil-fuel branding adjacent to restoration. Robotanica becomes the legitimacy infrastructure for continued fossil extraction. The trees planted under the partnership are real, but the broader system effect is negative.

**Existing defenses:** Charter §3.6 (refusal of incompatible funding). Funding diversity requirement. Public record of partnerships and funders.

**Residual risk:** Moderate. The temptation is real and the rationalizations are sophisticated. The first such partnership accepted establishes precedent.

**What to do now:** Define explicit categorical refusals at founding (e.g., no funding from companies whose primary business is fossil fuel extraction, regardless of restoration commitment). Make the categorical refusal public and irrevocable.

### 6.3 The Council Capture

Over fifteen years, the Science Council's composition gradually shifts. Each individual appointment is reasonable. Members chosen for "operational realism" replace members chosen for "ecological rigor." The veto authority remains formally intact but is exercised less and less. By year fifteen, the Council approves recipes that the founding Council would have vetoed.

**How this fails Robotanica:** Slowly, then suddenly. The structural defense of the Charter relies on the Council functioning. A captured Council provides the appearance of governance without the substance.

**Existing defenses:** Charter §4.2 (multi-disciplinary composition mandate). Public records of Council decisions. Federation-level review of Council composition. Charter review every ten years.

**Residual risk:** High. Capture is gradual and detection is delayed. The defenses depend on either external pressure or new leadership willing to confront the captured body.

**What to do now:** Specify Council appointment processes that no single party can dominate. Explicit composition requirements (representation by methodology, by region, by indigenous and community voices). Term limits that prevent entrenched factions. Public reporting of Council voting patterns.

### 6.4 The Falsified Outcome

An Operator with a struggling recipe instance reports survival rates substantially better than reality. The verifier they nominally work with — accredited but underpaid and overstretched — signs off without rigorous sampling. Credits are issued. The Operator profits. The Landowner is told the parcel is doing well. Reality on the ground continues to diverge.

**How this fails Robotanica:** The credits represent outcomes that did not occur. When the discrepancy is eventually detected, Robotanica's credibility takes the hit, not just the Operator's.

**Existing defenses:** MRV Specification §3.3 (verifier independence), §7.4 (verifier provenance), §7.5 (verifier accountability). Cross-verification. Random and triggered audits. Whistleblower channels. The verifier's signed report is part of the immutable record.

**Residual risk:** Moderate. Verifier capture is a known failure mode in carbon markets. Detection is possible but not guaranteed.

**What to do now:** Design verifier accreditation and rotation to prevent cozy long-term Operator-verifier relationships. Fund cross-verification at meaningful sample rates. Make verifier performance public.

### 6.5 The Catastrophic Site

A flagship restoration site, prominently featured in fundraising and public communication, suffers catastrophic loss in year four — wildfire fueled by a drought intensified beyond projections. Survival drops below 20%. The site was a symbol; its loss is news.

**How this fails Robotanica:** Two ways. First, by attempting to spin or downplay the loss, which violates the Charter and is detectable. Second, by allowing the loss to be portrayed as evidence that the entire project is failing, when it is in fact a single site within a portfolio.

**Existing defenses:** Charter §2.9 (transparent failure). MRV §6.5 (reporting symmetry). A3 §6.6 reconciliation discipline. The portfolio approach: aggregate metrics absorb single-site failures.

**Residual risk:** Moderate. The reputational risk is real even with perfect handling.

**What to do now:** Pre-commit to public communication doctrine for site failures (a topic for the Public Communication Doctrine, forthcoming). Make portfolio-level metrics the primary public-facing metric, with site-level included for transparency but not foregrounded.

### 6.6 The Indigenous Conflict

A community whose representatives signed a Lease five years ago — under what was at the time considered legitimate FPIC — now disputes the lease. New community leadership argues the original FPIC was inadequate, that compensation has been insufficient, or that the recipe is causing harm not anticipated. They demand termination.

**How this fails Robotanica:** Two ways. By resisting termination, Robotanica violates Charter §3.3 and exposes itself to legitimate accusations of colonial extraction. By terminating without operational competence, Robotanica abandons a partially-restored parcel and harms the ecosystem.

**Existing defenses:** Charter §3.3 (FPIC and indigenous sovereignty), Lease Requirements §6 (termination procedures), A3 §6.4 (consent revocation).

**Residual risk:** Moderate. Sovereignty conflicts of this kind are inevitable at scale.

**What to do now:** Make consent revocation rights explicit and well-understood at FPIC. Build operational reserves for parcels in mid-restoration that need transitional stewardship after lease termination. Maintain ongoing community relationships beyond the formal Lease relationship.

### 6.7 The Hostile Jurisdiction

A government in a country where Robotanica operates 200 active Leases declares the project a national security threat, expels personnel, and seizes operations. The reasons may be: alignment with opposition movements, suspicion of foreign influence, conflict with extractive interests, or simple authoritarian preference.

**How this fails Robotanica:** Lease commitments to Landowners and communities cannot be honored. Restoration on the ground is interrupted. Personnel may be detained or worse.

**Existing defenses:** Charter §7.3 (succession and dissolution). Jurisdictional diversity (no single jurisdiction is critical). Federation structure (members operate locally during partition, A3 §7.5).

**Residual risk:** High in any specific jurisdiction; manageable at the project level if jurisdictional diversity is maintained.

**What to do now:** Conduct jurisdictional risk assessment continuously. Maintain succession protocols for each jurisdiction. Refuse to concentrate operations in single high-risk jurisdictions even when local conditions seem favorable.

### 6.8 The Founder Departure

The founders of Robotanica leave, are pushed out, or die unexpectedly. The successor leadership faces pressure from funders, partners, and the media to either preserve every founder choice or repudiate them entirely.

**How this fails Robotanica:** Both extremes are wrong. Preservation prevents necessary evolution; repudiation breaks continuity.

**Existing defenses:** Charter as durable structure independent of founders. Stewardship Office structurally insulated from leadership changes. Multi-decade commitments encoded in Lease and protocol terms.

**Residual risk:** Moderate. Leadership transitions are always disruptive.

**What to do now:** Make Charter primacy clear from founding: founders are bound by it, not the other way around. Plan for succession from the start, not as crisis response.

### 6.9 The Data Breach

A misconfiguration or compromise exposes precise locations of vulnerable sites — endangered species, indigenous community territories, restoration sites in conflict zones. Bad actors use the data for poaching, encroachment, or targeted violence.

**How this fails Robotanica:** Direct harm to ecosystems and people. Loss of trust from communities who shared sensitive information.

**Existing defenses:** Gaia §7.6 (security), §7.5 (sovereignty), API coarsening for sensitive locations, sovereignty-aware access controls.

**Residual risk:** Moderate. No system is perfectly secure.

**What to do now:** Treat sensitive-location data with extreme conservatism: do not collect what is not needed, do not store what is not collected, do not expose what is stored. Default to less data, not more. Periodic security audits.

### 6.10 The Agent Drift

Over five years, the agent infrastructure subtly biases recipe recommendations toward operationally simpler recipes — those that complete faster, report cleaner metrics, and integrate more easily with OpenFactory's fleet patterns. The biases are individually small but compound. The Codex over time accumulates revisions that favor these recipes. Ecological outcomes degrade subtly relative to what would have been recommended without agent involvement.

**How this fails Robotanica:** The mission is undermined slowly by the technology meant to serve it. Detection is difficult because the metrics agents optimize are still met.

**Existing defenses:** Gaia §7.5 (prompt and recipe discipline), human review of codex writes, agent provenance, evaluation against historical ground truth.

**Residual risk:** High. AI alignment failures are particularly hard to detect when subtle.

**What to do now:** Maintain human-led recipe authoring as the default; agents propose, humans dispose. Periodic blind comparison of agent recommendations vs. expert ecological recommendations. Long-term ecological outcomes (year 10, year 20) as the dominant agent evaluation metric, not short-term proxies. External agent audits as part of annual MRV audit.

---

## 7. Cross-Cutting Mitigations

### 7.1 Charter Primacy

The Charter is the strongest cross-cutting defense. Its un-amendable provisions defend against the largest category of capture and drift. Its annual review surfaces drift before it normalizes.

### 7.2 Federation Structure

Federation distributes risk: an attack on Robotanica's central organization does not destroy the federation members, indigenous partnerships, and stewardship leases. An attack on individual members does not destroy the federation. Each layer is defensible because it can survive the loss of others.

### 7.3 Public Record

Most threats — capture, drift, fraud — depend on opacity. The Charter's transparency commitments and the platforms' public record make detection by external parties possible. External detection is the failsafe when internal detection fails.

### 7.4 Forkability

Charter §5.4 preserves the right to fork. This is not just permissive; it is disciplinary. A Robotanica that strays from its mission can be forked by communities and members willing to continue the original mission. Forkability is the deepest accountability.

### 7.5 Structural Multi-Disciplinarity

No single discipline, methodology, or interest group dominates governance. Science, indigenous voice, operations, and Landowner perspectives all have structural standing. Capture requires capturing all, which is much harder than capturing one.

### 7.6 Long-Horizon Insulation

The Stewardship Office, the multi-decade Leases, and the un-amendable provisions all operate on a timescale longer than any specific funder, partner, or government. Threats that play out on shorter timescales are absorbed by structures that outlast them.

---

## 8. Residual Risk Acceptance

The threats this document names cannot all be eliminated. Some must be accepted, monitored, and revisited.

Accepted residual risks include:

- **Slow drift** that escapes annual review.
- **Insider risk** that defeats audit trails.
- **AI alignment failure** that is subtle enough to avoid detection.
- **Climate catastrophe** beyond planning bounds.
- **Civilizational disruption** beyond the project's control.
- **Bad-faith critique** that succeeds despite transparency.

Accepting residual risk does not mean ignoring it. It means: monitoring continues, structural protections are maintained, and the project is built to survive when residual risks materialize, even if not in the form expected.

---

## 9. Review and Revision

### 9.1 Cadence

This document is reviewed annually by:

- Robotanica leadership (operational threats, mitigation effectiveness).
- The Science Council (ecological and scientific threats).
- The Stewardship Office (Landowner, community, and lease threats).
- An external review body (capture and drift threats most accurately seen from outside).

### 9.2 Triggered Review

Material new threats — newly identified attack patterns, regulatory changes, ecological shifts — trigger out-of-cycle revision.

### 9.3 Public Posting

This document is public. The threats are public. The mitigations are public. The residual risks are public. This is consistent with Charter §2.4 (open by default) and §2.9 (transparent failure).

---

## 10. Open Questions

- **External review structure.** Who conducts the external review? Independence requires an entity not funded by Robotanica, but funding is the natural compensation mechanism. Reciprocal arrangements with peer organizations may be one answer.
- **Whistleblower protection at scale.** The Charter commits to whistleblower protection, but operationalizing this for a federated, multi-jurisdictional project is non-trivial.
- **Threat model for AI agents at deeper capability.** As agents become more capable, the threat surface shifts. The current threat model assumes human-in-the-loop for high-stakes decisions; future capability levels may force re-examination.
- **Climate scenarios beyond plan.** What is the planning posture for climate scenarios that current restoration ecology cannot address? The Charter does not yet specify when and how the project would acknowledge irreducible failure of the underlying premises.
- **Catastrophic insider scenario.** A senior insider with broad access acting in coordinated bad faith is the worst-case insider scenario. The current defenses — separation of duties, audit trails — are necessary but may not be sufficient. Stronger insider-threat programs may be required at scale.
- **Adversaries not yet enumerated.** This document is incomplete by definition. The threats not yet imagined are the risk this document does not directly reduce.

---

## Appendix A — Glossary (Threat-Model-Specific)

- **Adversary** — An actor with motive and capacity to harm, capture, or weaponize Robotanica.
- **Attack surface** — A part of Robotanica exposed to potential adversarial action.
- **Capture** — Gradual replacement of independent governance, decision, or operational structures with actors aligned to particular interests.
- **Drift** — Slow accumulation of small compromises that erode mission discipline.
- **FPIC** — Free, Prior, and Informed Consent.
- **Greenwashing** — Use of environmental association to legitimize practices incompatible with environmental outcomes.
- **Reconciliation** — Correction of prior claims in light of new evidence.
- **Residual risk** — Risk remaining after applicable mitigations.
- **Sybil attack** — Attack on a system through creation of many false identities.
- **Threat surface** — Synonym for attack surface; the set of points where threats can act.

---

## Appendix B — References

- **STRIDE** threat modeling framework (as a comparison, not a model).
- **Bruce Schneier**, on long-horizon security and trust.
- **Carbon Market Watch**, on observed failure modes in carbon markets.
- **Survival International**, on indigenous-rights protection in conservation contexts.
- **Tightening the Belt: Civil Society Accountability for Climate Pledges** (and similar accountability literature).
- **Anthropic, OpenAI, and other AI labs' public threat models** for AI agent threats.
- **Climate Risk Assessment frameworks** (TCFD, PCAF) for climate risk aspects.

---

*This document names what the others assume: that adversaries exist, that institutions decay, that catastrophes happen, that good intentions compound into bad outcomes. Naming is not enough. The mitigations are real, the residual risks are accepted, and the discipline is to revisit this document when the world reveals new threats and to act on what it surfaces.*
