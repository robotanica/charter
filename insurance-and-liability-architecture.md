# Insurance and Liability Architecture

## Specification (v0)

**Document type:** Operational and risk specification
**Status:** Draft for review
**Companion documents:** Robotanica Charter, Funding Strategy, Founding Capital Plan, MRV Specification, Threat Model, Stewardship Lease Requirements

---

## 1. Purpose and Status

This document specifies how Robotanica handles insurance and liability — the financial protection against losses and the legal allocation of responsibility when things go wrong.

The Funding Strategy briefly mentioned insurance (§4.7). The Threat Model identified scenarios where liability matters but did not allocate it. The Stewardship Lease Requirements specified that compensation discipline applies but did not specify catastrophe protection. The Founding Capital Plan identified reserves but did not address commercial insurance. The result: insurance and liability have been gestures rather than architecture.

This document provides the architecture.

The document is **honest about limits**. Some restoration risks are not commercially insurable today; markets may develop, may not, or may develop on terms incompatible with the Charter. Some liability questions are unsettled in law; jurisdictional variation is large. The architecture works within these limits, designs around them where possible, and acknowledges them where it cannot.

The document is **scaffolded for evolution**. Insurance arrangements at founding (when capital is small, sites are few, and the project is new) differ from arrangements at scale. This document covers founding through early scale; later phases require revision as the project matures.

---

## 2. The Risk Landscape

### 2.1 What Can Go Wrong

Restoration involves risks across several categories:

- **Site catastrophe** — fire, drought, flood, pest, disease, or other event causing partial or total cohort loss.
- **Operational accidents** — worker injury, equipment failure, vehicle accidents, biosecurity breach.
- **Property damage** — to landowner property, neighboring property, infrastructure.
- **Verifier error** — incorrect verification leading to incorrect credit issuance, requiring correction.
- **Operator misconduct** — fraud, gross negligence, intentional harm.
- **Cyber incidents** — data breach, system compromise, ransomware.
- **Litigation** — claims against Robotanica or federation parties.
- **Climate-driven catastrophe** — events at the high end of climate scenarios per the Climate Scenario Assumptions.
- **Reconciliation events** — credit invalidation requiring buyer compensation per MRV §14.
- **Personnel safety incidents** — death, serious injury, conflict-related events.
- **Indigenous and community harm** — direct or indirect harm to communities through Robotanica's work.

Each category creates potential liability and potential financial loss.

### 2.2 Who Bears the Risk

In conventional commercial restoration, risk allocation often defaults to:

- **Landowners** bearing site catastrophe risk after planting (project moves on).
- **Workers** bearing personal injury risk (limited by employment law).
- **Buyers** bearing some credit invalidation risk (if contracts permit).
- **No one** bearing some risks (community harm, ecosystem damage).

Robotanica's architecture restructures this:

- **Robotanica and federation parties** bear primary financial risk for site catastrophe through reconciliation reserves and commercial reinsurance where available.
- **Personnel** are protected through worker insurance, safety discipline, and the right of refusal.
- **Buyers** carry bounded risk through forward contract terms; reconciliation is structurally honored.
- **Communities** are protected through structural commitments (no abandonment, indigenous sovereignty, succession planning).
- **Landowners** are supported, not abandoned, when things go wrong on their land.

This restructuring has cost. The cost is part of doing restoration honestly.

### 2.3 The Limits

Some risks are not commercially insurable:

- Multi-decade catastrophe insurance for restoration outcomes does not exist as a developed market.
- Climate-driven event insurance is partial and increasingly priced out of accessibility.
- Liability for indigenous and community harm is poorly served by commercial markets.
- Reputational damage from systemic failures is not insurable.

The architecture works within these limits through reserves, mutual arrangements, and structural protections — not by pretending that commercial insurance covers everything.

---

## 3. Principles

These principles bind the insurance and liability architecture and may not be set aside for cost convenience.

### 3.1 Risk Allocation by Capability

**INS-001** Risks are allocated to the parties best positioned to manage them, not the parties least able to refuse the allocation.

**INS-002** Workers, communities, and Landowners are not loaded with risks they cannot manage.

### 3.2 No Externalization to Communities

**INS-010** Robotanica does not externalize restoration risk onto communities. Where communities partner with Robotanica, the partnership protects them from project-specific risks they did not create.

### 3.3 Worker Safety Funded

**INS-020** Worker safety is structurally funded. Workers' compensation, health, life, and disability coverage are not optional cost items.

### 3.4 Buyer Protection Bounded

**INS-030** Buyers are protected against credit invalidation per MRV §14 and contract terms. Protection is bounded; buyers do not get make-whole guarantees beyond defined contract scope.

### 3.5 Federation Parties Not Personally Liable

**INS-040** Federation parties (Operators, Verifiers, Scientific Contributors, etc.) are not personally liable for federation-level systemic risks beyond their own actions.

### 3.6 Insurance From Mission-Compatible Sources

**INS-050** Where commercial insurance is purchased, it is from carriers whose broader practices are compatible with the Funding Strategy refusals (§5). Insurance from fossil-fuel-heavy carriers is refused at material premiums or where alternatives exist.

### 3.7 Mutual Arrangements Preferred Where Markets Are Inadequate

**INS-060** Where commercial insurance markets are inadequate or compromised, federation-mutual arrangements are preferred over no protection.

### 3.8 Reserves as Primary Protection

**INS-070** Reconciliation and operational reserves are the primary structural protection. Insurance is supplementary to reserves, not a substitute.

### 3.9 Transparency

**INS-080** Insurance arrangements above material thresholds are publicly disclosed. The structural protection is part of the public record per Public Communication Doctrine §5.

### 3.10 Catastrophic Cap Acknowledged

**INS-090** Some catastrophic scenarios exceed any reasonable insurance and reserve discipline. The architecture acknowledges this rather than pretending against it.

---

## 4. Insurance Categories

The architecture covers seven primary insurance categories.

### 4.1 Worker Compensation and Personnel Insurance

**WORK-001** All Robotanica personnel are covered by:

- **Workers' compensation** per jurisdictional requirements (medical, disability, death benefits for workplace incidents).
- **Health insurance** for personnel and dependents per Personnel and Compensation Philosophy §4.1.
- **Life and long-term disability** for substantial coverage.
- **Hardship coverage** for personnel deployed to remote regions or hardship contexts.

**WORK-002** Coverage extends to:

- Direct employees.
- Contractors performing work substantially as employees.
- Field stewards in remote contexts where standard coverage is inadequate.
- Indigenous and community personnel where they participate in ways that warrant coverage and where coverage is consistent with community governance.

**WORK-003** Personnel coverage is paid by Robotanica or the relevant Federation Operator, not by the personnel themselves. Premium structure is part of compensation.

### 4.2 General Liability and Operational Insurance

**LIAB-001** General liability coverage protects against:

- Third-party bodily injury and property damage from operations.
- Premises liability at facilities and operating sites.
- Vehicle and equipment liability.
- Pollution liability where applicable.

**LIAB-002** Coverage limits scale with operational scope. Founding-phase coverage may be modest; planetary-scale coverage requires substantial primary and umbrella layers.

**LIAB-003** Specific operational risks (high-altitude work, marine work, work in conflict-adjacent regions) require specific endorsements.

### 4.3 Site Catastrophe (Cohort Insurance)

**CAT-001** Insurance against catastrophic loss of cohorts due to fire, severe weather, pest, disease, or other events that can be insured commercially is purchased where available and economical.

**CAT-002** Site catastrophe insurance is currently underdeveloped commercially:

- Some forestry insurance products exist for commercial timber operations.
- Adapting these to restoration cohorts requires negotiation with carriers.
- Coverage tends to be expensive and limited.

**CAT-003** Where commercial insurance is unavailable or uneconomical, **reconciliation reserves** (per MRV §10.3) and **federation-mutual arrangements** (per §6) cover the gap.

**CAT-004** Catastrophe insurance does not displace reconciliation discipline. Even where insurance pays, credits affected by catastrophe are reconciled per MRV §14.

### 4.4 Verifier Errors and Omissions

**VER-001** Independent verifiers carry errors and omissions (E&O) insurance per the Federation Membership Agreement §4.2.

**VER-002** E&O coverage handles:

- Honest errors in verification (incorrect classification, calculation mistakes).
- Methodology gaps where the verifier could not have known.

**VER-003** E&O does not cover:

- Intentional misconduct (which is grounds for expulsion).
- Verifier-buyer collusion.
- Pattern of negligence beyond bounds of honest error.

### 4.5 Cyber and Data

**CYB-001** Cyber insurance covers:

- Data breach response and notification.
- Forensics and recovery.
- Business interruption from cyber events.
- Some ransomware response (with discipline against payment per Threat Model defenses).

**CYB-002** Cyber insurance does not cover:

- Cryptographic compromise of the federation event ledger (per the architectural design, ledger integrity is verifiable independently of any single system).
- Reputational damage.
- Long-term loss of trust.

These are addressed through technical architecture and incident response, not insurance.

### 4.6 Directors and Officers

**DO-001** Directors and Officers (D&O) coverage protects governance bodies (Federation board, Stewardship Office leadership, Council, AIERB) against:

- Personal liability claims for governance decisions.
- Defense costs in actions related to governance.

**DO-002** D&O coverage is essential for recruiting governance volunteers; without it, qualified parties decline service.

**DO-003** D&O does not protect against intentional malfeasance, fraud, or actions outside the scope of authority.

### 4.7 Operator Insurance

**OP-001** Federation Operators carry their own operational insurance per their operational scope:

- General liability for their own operations.
- Workers' compensation for their employees.
- Property insurance for their facilities and equipment.
- Specific endorsements per their operational context.

**OP-002** Operator insurance is independent of Robotanica's institutional insurance. Each Operator carries its own.

**OP-003** Federation Membership Agreement (§4.1) requires Operators to maintain adequate insurance per their scope. Inadequate coverage is grounds for membership review.

---

## 5. Reconciliation Reserves

Reserves are the primary structural protection. Insurance is supplementary.

### 5.1 Reconciliation Reserve Sizing

**RES-001** Reconciliation reserves (per MRV §10.3 and Funding Strategy §6.6) are sized based on:

- Expected loss rates per cohort, per recipe, per bioregion.
- Climate scenario assumptions per Climate Scenario Assumptions §4.
- Stress test under Scenario C conditions.
- Audit and review by qualified actuaries.

**RES-002** Initial sizing during founding phases is conservative (over-reserved given limited operating history). As loss rates become known, sizing is calibrated.

### 5.2 Reserve Funding

**RES-010** Reserves are funded:

- A defined fraction of credit issuance revenue allocated to reserves (per MRV §10.3).
- Top-up from operating revenue or capital raises if reserves drop below threshold.
- Reserve growth ahead of expected loss curve.

**RES-011** Reserve allocation occurs **before** other downstream allocations. Reserves are not the residual; they are foundational.

### 5.3 Reserve Investment

**RES-020** Reserves are invested in:

- Treasury bills or comparable sovereign instruments.
- Mission-aligned fixed income (where instruments exist).
- Cash equivalents.

**RES-021** Reserves are not invested in:

- Equity markets (volatility incompatible with operational reliance).
- Cryptocurrency.
- Categorically refused industries (per Funding Strategy §5).
- Concentrated counterparty exposure.

### 5.4 Reserve Drawdown

**RES-030** Reserve drawdowns occur for:

- Reconciliation events per MRV §14.
- Catastrophic site loss compensation.
- Federation-wide systemic events affecting multiple sites.

**RES-031** Drawdowns are governed:

- Routine reconciliation drawdowns by MRV protocol.
- Major drawdowns require Federation governance approval.
- All drawdowns are publicly recorded.

### 5.5 Reserve Floor

**RES-040** Reserves have a floor (defined fraction of credit liability outstanding) below which reserve build-back is prioritized over other capital deployment.

**RES-041** If reserves fall below floor through drawdowns, additional capital raises are prioritized to restore reserves.

---

## 6. Federation-Mutual Arrangements

Where commercial markets are inadequate, federation-mutual arrangements provide protection.

### 6.1 Why Mutual Arrangements

Some restoration risks are:

- Too novel for commercial markets to price.
- Too multi-decade for current insurance product structures.
- Too geographically diverse for standard underwriting.
- Too aligned with mission for commercial carrier interest.

Federation-mutual arrangements pool risk across federation members at scale, offering protection in domains commercial markets cannot serve.

### 6.2 Structure of Mutual Arrangements

**MUT-001** Federation mutual arrangements (where established) include:

- Formal pool structure with documented governance.
- Defined risk categories covered.
- Defined contribution rates per federation member.
- Defined claims process.
- Defined surplus and deficit handling.
- Reinsurance back-up where available.

### 6.3 Voluntary Participation

**MUT-010** Federation members may voluntarily participate in mutual arrangements. Participation is not required.

**MUT-011** Federation members carrying their own commercial coverage may decline mutual participation; benefits and contributions are aligned.

### 6.4 Inter-Federation Mutuality

**MUT-020** Where forks (per Charter §5.4) exist or where multiple federations operate, inter-federation mutual arrangements are possible and may strengthen all participants.

**MUT-021** Inter-federation arrangements honor the discipline of each federation; weak-discipline federation participation is refused.

### 6.5 Mutual Arrangement Limits

**MUT-030** Mutual arrangements are not unlimited:

- Capacity is constrained by total contributions and reinsurance.
- Catastrophic events exceeding capacity are addressed through reserves and external capital.
- Mutual arrangements supplement, not substitute for, prudent operations.

### 6.6 Reinsurance Back-Up

**MUT-040** Where reinsurance markets exist for the categories covered, mutual arrangements cede appropriate risk to reinsurers. This protects the mutual against catastrophic events.

---

## 7. Liability Allocation

How responsibility is allocated when things go wrong.

### 7.1 Operator Liability

**LIAB-OP-001** Operators bear primary liability for:

- Their own operational decisions and execution.
- Worker safety in their employ.
- Compliance with Recipe and Lease terms.
- Truthful reporting per MRV.

**LIAB-OP-002** Operators are not liable for:

- Recipe failures (where the operator followed the recipe in good faith).
- Federation-systemic events (catastrophe, market collapse, etc.).
- Acts of nature beyond reasonable preparation.

### 7.2 Robotanica Institutional Liability

**LIAB-INST-001** Robotanica's institutional entity bears liability for:

- Charter violations attributable to institutional decisions.
- Platform failures (Gaia, A3, OpenFactory) attributable to engineering decisions.
- Federation-wide governance decisions.
- Misrepresentation in public communication.

**LIAB-INST-002** Robotanica is not personally liable for:

- Operator-specific actions.
- Force majeure events.
- Federation member misconduct (which results in member discipline, not Robotanica liability).

### 7.3 Federation Member Liability

**LIAB-MEM-001** Federation members are liable for their own conduct per the Federation Membership Agreement §9.

**LIAB-MEM-002** Federation members are not jointly liable for other members' conduct or for federation-wide systemic events.

### 7.4 Verifier Liability

**LIAB-VER-001** Verifiers are liable for:

- Errors in verification (covered by E&O).
- Intentional misconduct (not covered; subject to expulsion and possibly criminal liability).

**LIAB-VER-002** Verifiers are not liable for:

- Outcomes outside the verification scope.
- Failures arising from withheld evidence by other parties.

### 7.5 Funder and Buyer Liability

**LIAB-FUND-001** Funders and buyers bear liability only for:

- Failure to perform their funding or purchase commitments.
- Misrepresentation in their relationships.

**LIAB-FUND-002** Funders and buyers are not liable for restoration outcomes.

### 7.6 Landowner Liability

**LIAB-LO-001** Landowners are liable for:

- Compliance with their Lease commitments.
- Acts within their continuing authority on the land.

**LIAB-LO-002** Landowners are not liable for:

- Operator failures on their land.
- Recipe failures.
- Federation governance.
- Restoration outcomes generally.

### 7.7 Worker Liability

**LIAB-WORK-001** Workers are liable only for:

- Intentional misconduct or gross negligence.

**LIAB-WORK-002** Workers are not personally liable for:

- Restoration outcomes.
- Honest errors within their training and experience.
- Decisions made by their employers.

### 7.8 Indigenous and Community Liability

**LIAB-COMM-001** Indigenous and local communities are liable only for:

- Intentional misconduct beyond their governance.

**LIAB-COMM-002** Communities are not liable for:

- Restoration outcomes.
- Operator or federation member conduct.
- Decisions made through their governance, applied within their sovereignty.

### 7.9 Limitation of Liability Discipline

**LIAB-LIM-001** Each party's liability is bounded — no party bears unlimited exposure. Liability bounds are recorded in Federation Membership Agreement, Stewardship Lease, and Service Contracts.

**LIAB-LIM-002** Bounds are calibrated so that liability is meaningful (not nominal) but not catastrophic to individual parties for federation-systemic events.

---

## 8. Buyer Protection Architecture

Credit buyers carry specific risks. Protection is bounded but real.

### 8.1 Reconciliation Protection

**BUY-001** When credits are reconciled per MRV §14:

- Reconciled credits are voided or replaced per the buyer's contract.
- Replacement may come from reserves, alternative cohorts, or refund.
- Buyer is made whole within contract terms.

**BUY-002** Reconciliation does not require litigation; it is structural per the credit lifecycle.

### 8.2 Forward Contract Protection

**BUY-010** Forward purchase contracts include:

- Defined performance milestones.
- Refund or alternative delivery if performance fails.
- Reconciliation provisions specific to the contract.
- Limits on Robotanica's liability (capped at the contract value).

### 8.3 Buyer Risk Disclosure

**BUY-020** At purchase, buyers receive:

- Clear disclosure of the credit's underlying outcomes and uncertainties.
- Reconciliation policy.
- Reserve sizing relative to outstanding credits.
- Realistic risk assessment for the credit category.

### 8.4 Buyer Protections Are Bounded

**BUY-030** Buyer protections do not extend to:

- Reputational damage if the buyer's purchase is later criticized.
- Market price changes between purchase and use.
- Regulatory changes affecting the credit's compliance value.
- Use of the credit beyond the underlying outcome.

### 8.5 Class Action and Group Recourse

**BUY-040** Where multiple buyers are affected by a single event, group recourse is available through:

- Coordinated reconciliation handling.
- Federation-level claims processes.
- Mediation or arbitration as appropriate.

---

## 9. Community Protection

Indigenous and local communities receive specific protections beyond general liability.

### 9.1 No Externalized Risk

**COMM-001** Robotanica's restoration on community lands does not externalize risk to communities. Communities are not financially exposed to operational, recipe, or federation-systemic failures.

### 9.2 Compensation Continuity

**COMM-010** Where restoration on community lands fails, community compensation streams continue:

- Lease payments continue per terms.
- Benefit-sharing arrangements continue per partnership.
- Communities are not penalized for events outside their control.

### 9.3 Successor Operator Discipline

**COMM-020** Where an Operator fails on community-engaged parcels, succession is structured to honor community partnerships:

- Successor Operator inherits commitments to the community.
- Community has voice in succession choice (per Lease Requirements §6.6).
- Transition does not erode community position.

### 9.4 Community Legal Support

**COMM-030** Where communities face legal challenges related to Robotanica's work (regulatory, neighbor disputes, trespass claims), Robotanica provides legal support per partnership agreements.

### 9.5 Direct Harm Acknowledgment

**COMM-040** Where Robotanica's work directly harms communities (cultural sites disturbed, ceremonies disrupted, livelihoods affected), the harm is acknowledged honestly and compensation flows beyond contract terms.

**COMM-041** Direct harm response is not bounded by contract; it is bounded by Charter principles.

---

## 10. Personnel Protection

Personnel protection extends beyond worker compensation.

### 10.1 Right of Refusal

**PER-001** Personnel have absolute right to refuse unsafe or unethical work per Personnel Philosophy §3.7 and §12. Refusal does not affect compensation, standing, or assignment.

### 10.2 Whistleblower Protection

**PER-010** Whistleblowers are protected per Personnel Philosophy §11. Whistleblower protection includes legal support against retaliation by anyone, not just Robotanica.

### 10.3 Field Steward Specific Protection

**PER-020** Field stewards in remote and challenging contexts receive:

- Specific safety training.
- Equipment for safety.
- Emergency communication and evacuation protocols.
- Mental health support given the isolation and conditions.
- Family support during deployments.

### 10.4 Conflict-Region Personnel

**PER-030** Personnel in conflict-adjacent regions (within Charter and operational bounds) receive:

- Specific risk training and equipment.
- Insurance with adequate coverage for the region.
- Evacuation planning and capacity.
- Refusal authority is more salient — refusal in conflict regions is encouraged where conditions deteriorate.

### 10.5 Personnel-Caused Harm

**PER-040** When personnel cause harm through honest error within their training:

- Responsibility lies with the institutional discipline that trained and deployed them.
- Personnel are protected from personal liability for honest errors.
- Personal liability arises only for intentional or grossly negligent acts.

---

## 11. Litigation Discipline

How Robotanica engages with litigation.

### 11.1 Defending Mission and Commitments

**LIT-001** When sued, Robotanica defends consistent with its commitments:

- Charter principles are not abandoned in defense.
- Indigenous and community sovereignty is not weakened in defense.
- Transparency is maintained where consistent with effective defense.

### 11.2 Legal Settlements

**LIT-010** Settlements:

- Public when relevant to the mission and within legal constraints.
- Within reserves and insurance capacity (large settlements may require capital decisions).
- Not used to silence legitimate claims (e.g., not requiring confidentiality on substantive matters).

### 11.3 Initiating Litigation

**LIT-020** Robotanica initiates litigation rarely and reluctantly:

- Where necessary to defend the federation against external attack.
- Where necessary to enforce agreements after good-faith resolution failure.
- Where the litigation itself does not violate Charter principles.

### 11.4 Litigation Against Federation Members

**LIT-030** Internal disputes are resolved through Federation processes (mediation, dispute resolution, expulsion procedures) before litigation. Litigation is the last resort.

### 11.5 Litigation Reserves

**LIT-040** Reserves include allocation for legal defense costs and expected settlements:

- Defense reserves separate from operational reserves.
- Annual review of legal exposure.
- Adjustment for emerging legal risk patterns.

---

## 12. The Limits of Insurance

The architecture acknowledges what insurance cannot do.

### 12.1 Multi-Decade Catastrophe

Multi-decade catastrophe insurance for restoration outcomes does not exist as a developed market. The architecture relies on:

- Reconciliation reserves built progressively.
- Federation-mutual arrangements for risk pooling.
- Bioregional diversification reducing concentration risk.
- Climate scenario stress testing.

### 12.2 Reputation and Trust

No insurance protects against reputation loss from systemic failure. The architecture relies on:

- Disciplined operations preventing systemic failure.
- Transparent communication when failures occur (Public Communication Doctrine §9).
- Structural commitments that maintain trust through individual failures.

### 12.3 Existential Catastrophe

Some catastrophic scenarios (Scenario C climate, civilizational disruption, cascading ecosystem collapse) exceed any reasonable insurance and reserve discipline. The architecture acknowledges:

- These events would disrupt the federation, the credit market, the operating environment.
- Robotanica's response would be governance-led, not insurance-mediated.
- Survival of the mission depends on broader civilizational continuity, not just internal reserves.

### 12.4 Mission-Adjacent Risks

Some risks affect the mission without affecting Robotanica directly:

- Climate change accelerating beyond plan.
- Biodiversity catastrophe in non-restoration domains.
- Political and economic disruption in operating regions.

These are not insurable risks for Robotanica; they are conditions of operation.

---

## 13. Phasing

Insurance and liability architecture evolves through phases.

### 13.1 Founding Phase (Year 1-2)

- Worker compensation in place.
- General liability coverage at modest levels.
- D&O coverage for governance bodies.
- Initial reconciliation reserves accumulating.
- Operator insurance per member.
- No federation-mutual arrangements yet (insufficient scale).

### 13.2 Pilot Phase (Year 2-4)

- Worker and personnel coverage expanded.
- General liability scaled with operations.
- E&O coverage for Verifiers established.
- Reconciliation reserves at meaningful scale relative to credit liability.
- Cyber coverage added.
- Federation-mutual arrangements explored at pilot scale.

### 13.3 Scale Phase (Year 4+)

- Comprehensive insurance program.
- Federation-mutual arrangements operational.
- Catastrophe reinsurance where available.
- Reserves at sustained discipline levels.
- Inter-federation mutual arrangements where warranted.

### 13.4 Maturity Phase (Year 10+)

- Insurance integrated into operational discipline.
- Mutual arrangements robust and proven.
- Reserves at long-horizon-appropriate levels.
- Continuous review and adjustment.

---

## 14. Governance

### 14.1 Insurance Decisions

Insurance decisions of consequence are governed by:

- **CFO and Stewardship Office** for routine insurance procurement and review.
- **Funding Committee** for major insurance arrangements affecting capital.
- **Federation governance** for federation-mutual arrangement decisions.

### 14.2 Annual Review

**GOV-001** Insurance and liability architecture is reviewed annually:

- Coverage adequacy versus operations.
- Premium trends and market conditions.
- Reserve adequacy.
- Claim patterns.
- Mutual arrangement performance.
- Liability patterns.

### 14.3 Public Reporting

**GOV-010** The annual report includes:

- Insurance coverage in summary form.
- Reserve levels and changes.
- Major claims and resolutions.
- Forward priorities.

### 14.4 Material Changes

**GOV-020** Material changes (new categories, major coverage increases, mutual arrangement establishment) go through Funding Committee review and Federation governance ratification as appropriate.

---

## 15. Open Questions

These are unresolved questions in insurance and liability architecture:

- **Multi-decade restoration catastrophe insurance.** This market does not exist in adequate form. Whether it develops, on what terms, with what discipline is uncertain. The architecture works around the gap; market development would substantially change the architecture.
- **Federation-mutual arrangement structure.** Specific legal structure (cell captives, risk retention groups, mutual insurance companies, informal pools) requires legal work and may vary by jurisdiction.
- **Climate-driven catastrophe insurance.** As climate events accelerate, commercial insurance for affected categories is becoming more expensive or unavailable. Whether mutual or sovereign-backed alternatives emerge is uncertain.
- **Cross-jurisdictional liability.** Federation operations across jurisdictions create complex liability questions (whose law applies, where claims are heard, how judgments are enforced). Legal work is needed.
- **Indigenous community claims standing.** Whether indigenous communities have legal standing to bring claims for ecological harms is jurisdictionally variable. Robotanica supports community standing where applicable.
- **Future generations standing.** Some legal systems are developing standing for future generations or for ecosystems themselves. Robotanica's posture toward such standing is supportive but the legal landscape is evolving.
- **Personnel protection in conflict regions.** Operating in conflict-adjacent regions creates personnel risks that conventional insurance does not handle well. Whether to develop specialized coverage or to refuse such operations is a continuing judgment.
- **Reinsurance market access.** As Robotanica scales, reinsurance partnerships become important. Reinsurance market is concentrated and may be reluctant to engage with novel restoration risks.
- **Insurance carrier mission alignment.** Most major insurance carriers have substantial fossil fuel exposure. Finding mission-compatible coverage at scale may require either market shift or alternative structures.
- **Buyer recourse governance.** When credit buyers are dissatisfied with reconciliation, the recourse process (mediation, arbitration, litigation) needs more explicit specification.

---

## Appendix A — Insurance Categories Summary

| Category | Primary Risk Covered | Source |
|---|---|---|
| Worker compensation | Workplace injury, illness, death | Robotanica/Operator |
| General liability | Third-party harm from operations | Commercial |
| Site catastrophe | Cohort loss from defined events | Commercial + reserves + mutual |
| Verifier E&O | Verification errors | Commercial |
| Cyber | Data breach and cyber events | Commercial |
| D&O | Governance liability | Commercial |
| Operator | Operator-specific operations | Operator's own |

---

## Appendix B — Reserve Discipline Summary

- **Reconciliation reserve** — Funded fraction of credit revenue, primary catastrophe protection.
- **Operating reserve** — 6 months operating expense.
- **Contingency reserve** — Catastrophic events beyond reconciliation reserve.
- **Defense reserve** — Legal defense costs and expected settlements.

---

## Appendix C — Cross-References

- **Robotanica Charter** §3.5 (commitments to people)
- **Funding Strategy** §4.7 (reserve and contingency capital)
- **Founding Capital Plan** §9 (cash management and reserves)
- **MRV Specification** §10.3 (reconciliation reserve), §14 (reconciliation)
- **Threat Model** §4 (failure modes)
- **Stewardship Lease Requirements** §9 (compensation), §6 (succession)
- **Federation Membership Agreement** §4.1-4.6 (member obligations)
- **Personnel and Compensation Philosophy** §8 (safety), §11 (whistleblower protection)
- **Public Communication Doctrine** §5 (public record)
- **Climate Scenario Assumptions** §12 (climate-driven catastrophe)

---

## Appendix D — Glossary (Insurance-Specific)

- **D&O** — Directors and Officers liability insurance.
- **E&O** — Errors and Omissions insurance.
- **Federation-mutual** — Risk pooling arrangement among federation members.
- **Reconciliation reserve** — Reserves held against future credit reconciliation events.
- **Reinsurance** — Insurance for insurers, providing back-up capacity.
- **Risk retention group** — A specific form of mutual insurance entity.
- **Self-insurance** — Coverage of risk through internal reserves rather than external insurance.

---

*Insurance and liability architecture is the financial discipline by which Robotanica handles the events that prudent operations cannot fully prevent. It is not a substitute for prudent operations; it is what prudent operations include alongside everything else. The architecture allocates risk to those best able to manage it, protects communities and personnel from risks they did not create, and acknowledges honestly what insurance cannot do. Reserves are the foundation; insurance is supplementary; structural commitments are primary.*
