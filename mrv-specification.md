# Measurement, Reporting, and Verification (MRV)

## Specification (v0)

**Document type:** Methodology specification
**Status:** Draft for scientific and stakeholder review
**Companion documents:** Robotanica Charter, Gaia PRD, A3 PRD, Stewardship Lease Requirements

---

## 1. Purpose and Status

This specification defines how Robotanica measures, reports, and verifies the ecological outcomes of its work. Without it, the headline objective — one trillion adult trees — is unfalsifiable, which means it is also unprovable.

The document defines:

- What counts as an **adult tree** for the purposes of the headline metric.
- How **survival**, **outcomes**, and **ecological state** are measured.
- How **uncertainty** is quantified and reported.
- How **claims** (credits, attestations, public statements) are tied to verified evidence.
- How **independent verification** is structured.
- How **failures** are reconciled.

This specification is a methodology, not a software product. Its primary consumers are scientists, auditors, regulators, and the Federation itself. Its requirements are implemented by Gaia (which holds the data and computes the metrics), A3 (which issues credits and records attestations), and Robotanica's verification partners (who audit independently).

---

## 2. Why MRV Matters

The carbon market's credibility crisis is, in substantial part, an MRV failure. Projects have claimed outcomes that did not occur; baselines have been inflated; permanence has been overstated; verification has been performed by parties with conflicts of interest. The outcome has been a market in which credits often do not represent real climate benefit, and trust in the entire instrument has eroded.

Biodiversity credits are likely to repeat the failure unless MRV is built differently from the start. Ecosystem restoration claims more broadly — academic, philanthropic, governmental — frequently rely on planting figures rather than survival figures, on satellite-greenness rather than ecological function, and on self-reported outcomes rather than independently verified ones.

Robotanica cannot accept these failure modes. The Charter's commitment to evidence (§2.6) and to transparent failure (§2.9) demands a different posture. MRV is the operational form of those commitments.

---

## 3. Principles

These principles bind the methodology and may not be set aside for operational convenience.

### 3.1 Conservative Bias

Where evidence is uncertain, MRV reports less, not more. A tree whose survival cannot be confirmed is not counted as alive. A site whose ecological state is uncertain is not assigned the more favorable interpretation. This bias is structural, not optional.

### 3.2 Uncertainty as First-Class

Every measurement carries an explicit uncertainty value or, where direct uncertainty is unavailable, a documented method from which uncertainty can be derived. Headline metrics propagate uncertainty; aggregates report ranges, not single numbers.

### 3.3 Independent Verification

Verification is performed by parties without financial interest in the outcome. Robotanica does not grade its own homework, and Operators do not verify their own work. Verification independence is a structural requirement, not a procedural courtesy.

### 3.4 Permanence as a Trajectory

A tree alive at year five may be dead at year thirty. Restoration claims are conditional on continued survival, and credits issued early are subject to reconciliation if later outcomes diverge. MRV tracks permanence over the full ecological horizon, not the duration of intervention.

### 3.5 Attribution Discipline

Robotanica claims credit for outcomes that result from its work. Where a parcel would have recovered partially without intervention, only the marginal effect is claimed. Attribution is established through documented baselines, controls where feasible, and conservative counterfactuals where controls are not feasible.

### 3.6 Methodological Pluralism

Quantitative remote sensing, ground sampling, indigenous and community monitoring, expert ecological assessment, and species-specific protocols are all legitimate sources of evidence. No single method is privileged; each is documented with its assumptions and uncertainties.

### 3.7 Transparency by Default

Every measurement, every report, every verification, and every reconciliation is recorded in Gaia and published, subject to the sovereignty and sensitive-location protections of the Charter and the Lease. Concealment of failure is a violation of the Charter.

### 3.8 Reproducibility

Every claim is reproducible from the underlying data. A third party with access to the same data and methodology must be able to arrive at substantially the same conclusion. Where reproducibility is impossible, the claim is qualified accordingly.

### 3.9 Honest Reconciliation

When evidence shows that a prior claim was wrong — through site failure, methodological correction, or new information — the claim is reconciled openly. Credits are voided, attestations are corrected, and the public record is updated.

---

## 4. Core Definitions

### 4.1 Tree

For the purposes of this specification, a **tree** is a perennial woody plant of a species typically reaching at least 5 meters in height at maturity in its native ecosystem, with a single dominant stem at maturity. Multi-stemmed plants typical of an ecosystem (mallee, coppice forms) are recognized through species-specific protocols.

This definition aligns with FAO conventions but is qualified by ecosystem context: a 4-meter species in a krummholz or boreal-edge ecosystem is recognized as a tree where its ecosystem role is equivalent.

### 4.2 Adult Tree

An **adult tree** is a tree that has reached the species-specific reproductive maturity threshold defined in Gaia's interpretation layer. The threshold is one of:

- **Reproductive maturity** — the species has produced viable seed at least once on the parcel.
- **Structural maturity** — the species has reached defined diameter-at-breast-height (DBH) and height thresholds for its species and bioregion.
- **Functional maturity** — for species where reproductive and structural metrics are inadequate, ecological function thresholds (canopy contribution, habitat provisioning, soil stabilization) defined per species.

Adult thresholds are species- and bioregion-specific, peer-reviewed in the codex, and revised as evidence requires. A species without an adult-threshold definition cannot contribute to the trillion-tree count until one is established.

The headline OKR — one trillion adult trees — is the count of trees on Robotanica-stewarded parcels that have reached their species-specific adult threshold and remain alive at the time of counting.

### 4.3 Survival

A tree is **alive** if direct or indirect evidence within a defined currency window confirms its viability. Currency windows are species-, ecosystem-, and method-specific. A tree without recent confirming evidence is **of unknown status** and is not counted as alive for headline reporting.

A tree is **dead** if direct evidence confirms mortality, or if indirect evidence over a defined period (typically two consecutive monitoring cycles without canopy or other expected signals) establishes presumed mortality.

Survival rate is computed per cohort: the fraction of established plants confirmed alive at a given time, with explicit treatment of unknown-status plants (reported as a separate category, not assigned to either alive or dead).

### 4.4 Establishment

**Establishment** is the threshold beyond which a planted tree has survived initial transplant shock and is judged to have a reasonable prospect of long-term survival. The threshold is species- and ecosystem-specific, typically expressed as continuous survival through one growing season plus one defined stress period (dry season, dormancy, etc.).

Survival rate is reported separately for: from-planting, from-establishment, and from-each-subsequent-milestone.

### 4.5 Restoration

**Restoration** is the active or passive process of returning a degraded ecosystem toward its reference ecological state. Restoration claims are tied to a documented reference state in Gaia's interpretation layer, against which progress is measured.

Robotanica recognizes restoration in degrees: from minor recovery to substantial recovery to full restoration. Most claims will be partial; full restoration over decades is the goal, not the entry point.

### 4.6 Recipe Instance

A **recipe instance** (per the Gaia PRD) is the application of a recipe to a specific parcel and cohort. MRV is performed at the recipe-instance level: outcomes are measured, attributed, and verified for each instance, then aggregated.

### 4.7 Cohort

A **cohort** (per Gaia and A3) is a group of plants of common provenance, planted in a common event, on a common parcel, under a common recipe instance. MRV typically operates at cohort granularity for survival and outcome measurement; individual plant tracking is used where the parcel and species permit.

### 4.8 Baseline

A **baseline** is the documented state of a parcel before Robotanica's intervention, plus the documented expected trajectory of the parcel without intervention. Baselines are established before restoration begins; retrospective baselines are not accepted.

### 4.9 Additionality

**Additionality** is the difference between the parcel's actual trajectory under intervention and its expected trajectory without intervention. Only the additional outcome is attributable to Robotanica's work for credit issuance and headline metric purposes.

### 4.10 Permanence

**Permanence** is the durability of restoration outcomes over time. A 50-year survival is more permanent than a 5-year survival; an outcome durable through one drought cycle is more permanent than one untested by drought. Permanence is reported as a trajectory, not a single number.

### 4.11 Leakage

**Leakage** is restoration in one place that causes degradation in another — for example, displacement of agricultural or extractive activity to a previously intact site. Robotanica is responsible for monitoring and reporting leakage where its work could plausibly cause it.

---

## 5. Measurement

### 5.1 Multi-Modal Evidence

Measurements draw from multiple modalities, none privileged:

- **Satellite remote sensing** — broad-area indicators of canopy cover, NDVI, biomass, and change detection. Sources include Sentinel-2, Landsat, Planet, Maxar.
- **Drone and aerial surveys** — finer-resolution canopy and structural data, including LiDAR for biomass.
- **Ground sampling** — direct measurement of trees, plots, soils, and biota by trained surveyors using species-specific protocols.
- **Sensor networks** — continuous environmental telemetry: soil moisture, temperature, growth, pollinator activity.
- **Robotic perception** — observations from field robots during operational activity.
- **Indigenous and community monitoring** — ecological observation through traditional and locally-developed knowledge systems, recognized as first-class evidence per Charter §2.7.
- **Expert assessment** — ecologist-led site assessments where quantitative methods are inadequate or contested.

### 5.2 Sampling

Trillion-tree-scale measurement cannot be a census. Sampling design is documented per recipe instance and includes:

- **Sample frame** — the population from which samples are drawn (cohort, stand, parcel, region).
- **Sampling method** — random, stratified, systematic, or otherwise; with rationale.
- **Sample size** — sufficient for the target uncertainty; computed before sampling begins.
- **Sampling cadence** — frequency of resampling and the rationale for the cadence.
- **Estimator** — the method by which sample observations are extrapolated to population estimates.
- **Uncertainty quantification** — confidence intervals or equivalent for the resulting estimate.

Sampling protocols are species- and ecosystem-specific and are versioned in Gaia's interpretation layer.

### 5.3 Currency Windows

Each measurement type has a defined **currency window** — the period during which an observation is considered current evidence. Beyond the window, the observation is historical and a re-measurement is required to maintain current-state claims.

Currency windows are:

- **Survival (recent observation):** typically 1–2 monitoring cycles for active sites; longer for mature stands.
- **Adult status (structural):** typically annual updates for cohorts approaching threshold; less frequent for fully mature stands.
- **Soil and microbiome:** typically 2–5 year cycles unless intervention or disturbance triggers re-measurement.
- **Biodiversity surveys:** typically annual or biennial during seasons appropriate for the indicator taxa.

### 5.4 Species Identification

Species identification is reported with method (visual, expert, genetic, image classification) and confidence. Recipe instances bind to expected species lists in Gaia; deviations between expected and observed species are flagged for review.

Image classification by automated systems (vision models) is permitted but accompanied by confidence values and subject to review at calibration intervals.

### 5.5 Biomass Estimation

Biomass is estimated from species-specific allometric equations, with DBH and height as primary inputs and species- and ecosystem-corrected coefficients. LiDAR-derived biomass is accepted with calibration against ground truth.

Biomass is reported with explicit uncertainty; allometric error compounds quickly and is documented per estimate.

### 5.6 Soil Carbon

Soil organic carbon measurement requires direct soil sampling with appropriate depth profiles, lab analysis, and bulk-density correction. Remote-sensing-only soil carbon estimates are not accepted as the primary source of truth, though they may serve as monitoring proxies between direct samples.

Soil carbon claims are conservative: gains are recognized only after sufficient measurement intervals and statistical confidence.

### 5.7 Biodiversity Indicators

Biodiversity is measured through indicator taxa appropriate to the bioregion and recipe target: vascular plants, birds, soil arthropods, mycorrhizal fungi, pollinators, and others as recipe-relevant. Single-indicator biodiversity claims are not accepted; multi-indicator composite assessments are required.

Indicator selection is documented in the recipe and reviewed by the Science Council.

### 5.8 Holobiont and Ecological Function

Where recipe targets specify holobiont integrity or ecological function (water provisioning, pollinator support, soil stabilization), measurement protocols for these functions are defined per recipe and reported alongside structural metrics.

---

## 6. Reporting

### 6.1 Cadence

Reporting occurs on a defined cadence per recipe instance:

- **Operational reports** — monthly or quarterly, summarizing intervention activity and routine observations.
- **Outcome reports** — annual minimum, with finer cadence where data and recipe support it. Outcome reports update headline metrics.
- **Decadal reviews** — every 10 years per parcel, deep ecological assessment with full multi-modal evidence and Science Council review.

### 6.2 What Is Reported

Each outcome report includes:

- Cohort lifecycle state and survival statistics with uncertainty.
- Adult-threshold progression: number of trees having reached adult status this period, cumulative.
- Biomass and carbon stock with uncertainty.
- Biodiversity indicators against recipe targets.
- Recipe deviations and adaptations.
- Identified failures, near-misses, and recipe revision proposals.
- Verification status and any pending verification.

### 6.3 Aggregation

Aggregation across recipe instances, parcels, and regions follows uncertainty-propagating methods. Headline aggregate metrics (total adult trees, total stewarded area, total biomass restored) are reported with confidence intervals, never as single numbers.

### 6.4 Public Record

Outcome reports are published in the public record, subject to sovereignty and sensitive-location protections per the Charter. Aggregate metrics are public; per-parcel metrics may be restricted by Lease terms or community sovereignty decisions.

### 6.5 Reporting on Failure

Failures are reported on the same cadence as successes, in the same channels, with the same prominence. The Charter's commitment to transparent failure (§2.9) is operationalized through reporting symmetry: a failed cohort is reported with no less detail than a successful one.

### 6.6 Reporting to Specific Parties

- **Landowners** receive parcel-level reports per their Lease terms.
- **Indigenous and community parties** receive reports under their data sovereignty arrangements.
- **Auditors and certifiers** access reports at the granularity their role requires.
- **Regulators** receive jurisdiction-specific compliance reports as required.
- **Funders** receive aggregate and parcel-specific reports per their funding agreements.
- **The Federation and the Science Council** receive full reports for governance.

---

## 7. Verification

### 7.1 Independence

Verification is performed by parties without financial interest in the verified outcomes. Robotanica's internal monitoring is not verification. Operator self-reporting is not verification.

Acceptable verifiers include:

- Accredited third-party verification bodies (in regulated markets, those accredited under Verra, Gold Standard, Plan Vivo, or comparable).
- Academic institutions with relevant expertise and no conflicting financial interest.
- Federation-funded but governance-isolated verification corps, structured to prevent capture.
- Indigenous and community verification under their own protocols, where they are willing to perform it.

### 7.2 Verification Levels

Verification operates at multiple levels:

- **Routine verification** — sample-based audit of routine outcome reports. Cadence: every 1–2 reporting cycles per recipe instance.
- **Deep verification** — full audit of a recipe instance's entire history. Cadence: every decadal review or on triggered investigation.
- **Triggered verification** — audit triggered by suspicious patterns, complaints, or anomalies. Cadence: as needed.
- **Cross-verification** — comparison of independently produced verifications. Performed periodically as a check on the verification system itself.

### 7.3 What Verifiers Confirm

- Sample frame and sampling methods were as documented.
- Field measurements were conducted per protocol.
- Data integrity from observation through published metric is intact.
- Recipe instance bound to the correct version; deviations documented.
- Uncertainty quantification is honest and propagated correctly.
- Attribution and additionality claims are defensible.
- Failures are reported, not concealed.

### 7.4 Verification Provenance

Every verification produces a signed report stored in Gaia. The report includes the verifier identity, methodology, findings, and limitations. Verifier signatures are part of the integrity of the public record.

### 7.5 Verifier Accountability

Verifiers themselves are subject to review. Periodic cross-verification, public record of past verifications, and revocation procedures for verifiers found in breach are part of the system.

A verifier with repeated material errors or conflicts of interest is suspended; one with deliberate misconduct is expelled and reported.

### 7.6 Indigenous and Community Verification

Where verification is performed by indigenous or community parties under their own protocols, those protocols are recognized as legitimate verification per Charter §2.7. The community determines methodology and reporting form. The community's report is accepted as primary evidence for matters within its scope.

Where indigenous verification operates in parallel with quantitative verification, both are recorded and reported. Disagreements are surfaced and addressed in governance, not erased.

---

## 8. Uncertainty Quantification

### 8.1 Uncertainty Sources

Every measurement has multiple uncertainty sources:

- Sampling uncertainty (when sampling is used).
- Measurement error (instrument precision, observer variation).
- Allometric error (when biomass is estimated from structural measurements).
- Model error (when remote sensing uses inferred relationships).
- Currency error (when observations are not perfectly current).
- Attribution uncertainty (when additionality is contested).

Each source is quantified or, where direct quantification is unavailable, documented with the methodology that enables a third party to bound the uncertainty.

### 8.2 Propagation

Aggregate metrics propagate uncertainty from constituent measurements. Standard methods (Monte Carlo simulation, analytic propagation) are documented per metric. Headline aggregates are reported as ranges, not points.

### 8.3 Conservative Reporting

Where uncertainty is asymmetric, MRV reports the conservative tail. A range of 800,000–1,200,000 adult trees on a parcel is not reported as "1,000,000 adult trees"; it is reported as the range, with the public-facing summary using the lower end for headline claims.

### 8.4 Disclosed Limitations

Every report includes a section disclosing the limitations of its methodology, the categories of error not fully quantified, and the categories of outcome not measured at all.

---

## 9. Attribution and Additionality

### 9.1 Baseline Documentation

Every parcel begins with a documented baseline: state at intervention start plus expected trajectory without intervention. Baselines are produced before intervention begins and are independently reviewed.

### 9.2 Counterfactual Method

Counterfactuals are produced through one or more of:

- **Comparable controls** — adjacent or similar parcels not under intervention, monitored on the same cadence.
- **Historical trajectory analysis** — the parcel's documented state trajectory over years or decades prior to intervention.
- **Regional reference** — bioregion-typical trajectories derived from satellite and inventory data.
- **Expert ecological assessment** — qualified experts producing structured counterfactuals with documented assumptions.

No single counterfactual method is sufficient; multiple methods are used and disagreements are surfaced.

### 9.3 Additionality Tests

Restoration claims are subject to additionality tests:

- Would the outcome have occurred without intervention? With what likelihood?
- Was the intervention necessary, sufficient, or contributory to the outcome?
- Are there alternative explanations (climatic, regulatory, economic) that could account for the outcome?

Additionality is reported with the same uncertainty discipline as other measurements.

### 9.4 Conservative Attribution

Where additionality is uncertain, MRV attributes less, not more. Robotanica does not claim outcomes that would plausibly have occurred regardless of its work.

---

## 10. Permanence and the Trajectory of Claim

### 10.1 The Permanence Problem

A tree alive at year 5 may be dead at year 30. Issuing a credit for the year-5 survival assumes a permanence that is not yet established. This is the structural failure mode of most carbon credit programs.

### 10.2 Progressive Issuance

Robotanica's credit issuance is progressive: a fraction of expected lifetime credit is issued at each verified milestone (establishment, year 5, year 10, decadal reviews). The full credit is issued only after the species- and ecosystem-specific permanence threshold is reached.

The fractional issuance schedule is documented per recipe and reviewed by the Science Council.

### 10.3 Reconciliation Reserve

A portion of issued credits is held in a Federation reconciliation reserve. The reserve covers reconciliation events where prior issuance must be voided due to site failure or methodology correction. Reserve sizing is actuarial and reviewed periodically.

### 10.4 Buffer Pools

In addition to the reconciliation reserve, recipes participating in regulated credit markets contribute to buffer pools per market requirements (Verra, Gold Standard). Buffer pool participation does not substitute for the reconciliation reserve; both apply.

### 10.5 Permanence Reporting

Each parcel's permanence trajectory is reported continuously. A 90% survival at year 5 is reported alongside the projected year-30 survival under current conditions and the historical year-30 survival of comparable cohorts.

---

## 11. Leakage

### 11.1 Leakage Categories

- **Activity displacement** — restoration on one parcel displaces extractive or agricultural activity to another, causing degradation there.
- **Market leakage** — restoration reduces local supply of a commodity, raising prices and incentivizing degradation elsewhere.
- **Spatial leakage** — improvements in one site come at the expense of adjacent sites (water capture upstream depriving downstream, for example).

### 11.2 Leakage Monitoring

Each recipe instance includes leakage risk assessment and, where risk is non-trivial, monitoring at appropriate spatial scales. Leakage is reported and netted against gross outcomes for net-effect headline claims.

### 11.3 Boundary Conditions

Leakage assessment requires defined boundaries: the parcel, the surrounding zone, the bioregion, the global market. Assessment depth is proportional to the magnitude of the activity being displaced.

---

## 12. Integration with Robotanica's Platforms

### 12.1 Gaia

Gaia is the system of record for measurements, observations, and derived metrics. Every observation referenced in this specification is stored in Gaia with full provenance per the Gaia PRD. Recipes reference their MRV protocols by URI; recipe instances inherit the MRV obligations of their recipe.

### 12.2 A3

A3 issues credits, records attestations, and handles reconciliation. Credit issuance per A3-K-001 of the A3 PRD requires verified outcomes from Gaia under this specification. Reconciliation per A3-K-005 follows when this specification's reconciliation triggers fire.

A3's credit registry surfaces the MRV evidence underlying every credit: the parcel, the recipe instance, the verification report, the underlying observations.

### 12.3 OpenFactory

OpenFactory provides operational telemetry and biological-batch genealogy. MRV uses this data for attribution and for reconstructing the intervention history of a recipe instance.

### 12.4 The Science Council

The Science Council reviews and approves MRV methodologies, verifier accreditation, reconciliation events, and methodology revisions. The Council's veto authority extends to MRV practices that compromise the principles of this specification.

---

## 13. Independent Audit and Review

### 13.1 Annual Audit

The MRV system as a whole is audited annually by an independent body, separate from individual recipe-instance verifiers. The audit reviews methodology, verifier performance, reconciliation discipline, and aggregate integrity.

### 13.2 Public Audit Report

The annual audit report is public. It includes findings, recommendations, and the Federation's response to prior recommendations.

### 13.3 Methodology Review

This specification is subject to formal review every five years and informal review on a continuous basis. Revisions follow the proposal-review-merge protocol of Gaia's interpretation layer per the Gaia PRD.

### 13.4 External Critique

Robotanica welcomes external critique of its MRV methodology. Critique submitted through the Federation's open processes is logged, reviewed by the Science Council, and responded to in the public record. Substantive critique that surfaces methodological weaknesses is acted on.

---

## 14. Failure and Reconciliation

### 14.1 Failure Modes

MRV failure modes include:

- **Measurement error** — observations were inaccurate or unrepresentative.
- **Methodology error** — the protocol itself was flawed.
- **Integrity failure** — observations were falsified, omitted, or misreported.
- **Verification failure** — verification was inadequate or compromised.
- **Permanence failure** — outcomes that were verified later did not persist.

### 14.2 Reconciliation Triggers

Reconciliation is triggered when:

- A subsequent measurement contradicts a prior claim materially.
- A verification audit surfaces a measurement error.
- A site failure occurs that voids prior claims.
- A methodology review identifies a systematic error in past practice.
- A report from any party (operator, landowner, community, public) credibly alleges integrity failure and investigation confirms it.

### 14.3 Reconciliation Procedure

Reconciliation produces:

- An immutable record of the prior claim, the new evidence, and the resulting correction.
- Voiding or making-whole of affected credits per A3.
- Notification of affected parties (Landowners, credit holders, regulators).
- Update of the public record.
- Review by the Science Council and, where structural, by the broader Federation.

### 14.4 No Burying Failures

Reconciliation is reported on the same cadence and with the same prominence as routine outcomes. The Charter's commitment to transparent failure is operationalized through reconciliation symmetry: a corrected claim is no less visible than the original.

---

## 15. Phasing

| Phase | Scope | Exit criteria |
|---|---|---|
| 0 — Foundations | Adult-tree thresholds for first species; baseline methodology v0; Verifier accreditation v0 | First recipe instance with full MRV in operation |
| 1 — Pilot | Multiple recipe instances under MRV; first verification reports published; reconciliation reserve seeded | First verification cycle completed; first credit issued under progressive issuance |
| 2 — Federation | Indigenous and community verification protocols in production; jurisdiction-specific compliance reporting | First indigenous verification recognized in public record; first regulator-required compliance report filed |
| 3 — Multi-method | Full multi-modal evidence integration; uncertainty propagation across aggregates | Headline metrics published with confidence intervals; first decadal review completed |
| 4 — Mature | Continuous external audit; methodology versioning across multiple revisions | First five-year MRV methodology review completed; demonstrated reconciliation discipline at scale |

Phase boundaries are exit criteria, not dates.

---

## 16. Risks and Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Pressure to relax methodology to issue more credits | Restoration claims become unreliable; mission discredited | Science Council veto; un-amendable Charter principles; structural verifier independence |
| Gaming of sampling methods | Biased estimates favorable to claims | Sampling protocols pre-registered; verifier review of sample design; cross-verification |
| Verifier capture | Verification becomes ceremonial | Verifier accountability; rotation; cross-verification; expulsion procedures |
| Methodology stagnation | MRV becomes outdated as ecology and technology advance | Mandatory periodic review; external critique welcomed and acted on |
| Permanence overstatement | Credits issued for outcomes that will not persist | Progressive issuance; reconciliation reserve; conservative permanence assumptions |
| Leakage understatement | Net mission impact is overstated | Required leakage assessment per recipe; bioregion-scale monitoring |
| Attribution overclaim | Robotanica claims outcomes that would have occurred without it | Independent counterfactual review; conservative additionality default |
| Uncertainty hidden in aggregates | Public claims appear more certain than evidence supports | Uncertainty propagation mandatory in aggregates; ranges not points in headline reporting |
| Indigenous verification co-opted | Community evidence becomes legitimacy theater | Community-led methodology, community-controlled reporting, no Federation override |

---

## 17. Open Questions

- **Adult-threshold definition for novel ecosystem assemblages.** Where Robotanica's recipes produce species combinations not native to the parcel (assisted migration), how are adult thresholds defined? The codex needs entries that current ecological literature does not yet support.
- **Counterfactuals for landscapes already shaped by Robotanica.** As Robotanica works at scale, the bioregional baseline itself shifts. How are counterfactuals constructed when Robotanica's own work is part of the baseline?
- **Indigenous verification scope.** Where indigenous monitoring uses methods that produce qualitatively different evidence (oral records of bird abundance, for example), how does the Federation aggregate and report alongside quantitative evidence without subordinating either?
- **Permanence under climate change.** The species and ecosystems adopted today may not be viable in 50-year climates. How are permanence claims revised when the underlying ecological assumption shifts?
- **Verifier capacity at trillion scale.** The verifier corps needed at full scale may exceed current accredited capacity by orders of magnitude. How is verifier capacity grown without compromising independence?
- **Cross-bioregion methodology consistency.** Methodologies must be locally appropriate and globally comparable. The tension between these is unresolved in detail.
- **Liability for verifier error.** When a verifier signs a report later found materially wrong, what is the liability regime? Insurance markets for verification do not robustly exist.

---

## Appendix A — Glossary (MRV-Specific)

- **Additionality** — The marginal effect of intervention beyond the no-intervention counterfactual.
- **Adult tree** — A tree that has reached its species-specific reproductive, structural, or functional maturity threshold.
- **Allometric equation** — A statistical relationship between structural measurements (DBH, height) and biomass.
- **Attribution** — The assignment of an observed outcome to a specific cause (Robotanica's intervention).
- **Baseline** — Documented state at intervention start plus expected trajectory without intervention.
- **Buffer pool** — A reserve of credits required by external markets to cover non-permanence.
- **Cohort** — A group of plants of common provenance and planting event.
- **Counterfactual** — The hypothetical state of the parcel had intervention not occurred.
- **Currency window** — The period during which an observation is current evidence.
- **DBH** — Diameter at breast height. Standard structural tree measurement.
- **Establishment** — The threshold beyond which a planted tree is judged to have reasonable long-term survival prospects.
- **FAO** — Food and Agriculture Organization. Source of standardized forest definitions.
- **Leakage** — Restoration in one place that causes degradation elsewhere.
- **MRV** — Measurement, Reporting, Verification.
- **NDVI** — Normalized Difference Vegetation Index. Common remote-sensing greenness indicator.
- **Permanence** — The durability of restoration outcomes over time.
- **Progressive issuance** — Issuing credits in fractions over time as permanence is demonstrated.
- **Reconciliation** — Correction of prior claims in light of new evidence; voiding or making-whole of affected credits.
- **Recipe instance** — The application of a recipe to a specific parcel and cohort.
- **Reconciliation reserve** — A Federation reserve of credits held against future reconciliation events.
- **Verification** — Independent confirmation of measurement and reporting integrity.

---

## Appendix B — Standards and References

- **IPCC Guidelines for National Greenhouse Gas Inventories** (2006, 2019 refinement).
- **FAO Global Forest Resources Assessment** definitions for forest, tree, and related concepts.
- **Verra VCS** methodologies (as a comparison and integration point, not a model to follow uncritically).
- **Gold Standard** methodologies (same).
- **Plan Vivo** methodologies, particularly for community-led approaches.
- **Society for Ecological Restoration** International Standards for the Practice of Ecological Restoration.
- **CARE Principles** for indigenous data governance.
- **FPIC** as defined under UN Declaration on the Rights of Indigenous Peoples.
- **GHG Protocol** for emissions accounting comparison.
- **ART TREES** standard for jurisdictional REDD+.

---

*MRV is a discipline, not a software feature. This specification commits Robotanica to a posture that has historically been the exception, not the rule, in ecosystem restoration: that claims must be defensible, that uncertainty must be reported, that verification must be independent, and that failures must be reconciled openly. The headline objective is one trillion adult trees. This specification is the instrument that prevents that number from being a fiction.*
