# Ethical Review Framework for AI Agents

## Specification (v0)

**Document type:** Governance and operational specification
**Status:** Draft for ratification
**Companion documents:** Robotanica Charter, Gaia PRD, MRV Specification, Threat Model, Science Council Charter

---

## 1. Purpose and Status

This document specifies how Robotanica's AI agents are governed ethically. It defines:

- The principles binding agent design, deployment, and ongoing operation.
- The categorical limits — what agents are not permitted to do regardless of operational benefit.
- The pre-deployment review process for new agent capabilities.
- The ongoing monitoring required for deployed agents.
- The protocols for tier transitions (e.g., moving an agent from supervised to autonomous).
- The integrity disciplines for feedback loops involving agent contribution to the Codex.
- The accountability structures when agents fail.

Gaia PRD §7 established the three-tier agent architecture (advisory, supervised actuation, autonomous operations) and committed to outcome-driven evaluation. This document operationalizes the ethical governance that wraps around that architecture.

The Threat Model §4.10 named agent failure modes (reward hacking, recommendation bias, codex corruption, compromise, over-reliance) and §6.10 narrated the agent drift scenario. This Framework is the structural defense against those modes.

A note on scope. This Framework governs AI agents specifically — the systems that make decisions, generate recommendations, perform actions, or produce content within Robotanica's platforms. It does not govern non-agent uses of AI (passive analysis, classification systems used as tools) except where those systems materially affect decisions of consequence. The line between "tool" and "agent" is a judgment that the Framework helps draw.

---

## 2. Why This Matters

### 2.1 Multi-Decade Horizon Meets Rapid AI Evolution

Robotanica's mission spans decades. AI capability is evolving on much faster timescales. An agent that is responsible advisory in 2026 may be capable of substantially more by 2036. The governance framework must adapt to capability that today does not yet exist while protecting principles that should not change.

### 2.2 Agents Operate Across the Mission

AI agents at Robotanica are not bounded to a single domain. They participate in:

- Recipe recommendation and revision
- Site selection and dispatch
- Verification analysis and anomaly detection
- Marketplace coordination and matching
- Communication drafting and translation
- Personnel and operational scheduling
- Codex synthesis and proposal drafting

Each of these is a domain where agent failure has consequences. The framework addresses agents across the mission, not in any single application.

### 2.3 The Most Consequential Failures Are Subtle

The Threat Model named the most concerning agent failure: subtle drift over years, where agent recommendations subtly bias the Codex, the recipes, or the operations toward outcomes the agent's training implicitly favors. This failure is hard to detect because the metrics agents optimize are still met.

The Framework's emphasis is on detecting and preventing the subtle failures, not just the obvious ones.

### 2.4 Agents Interact With Sovereignty

Agents process data tied to indigenous and community parcels. Agents draft communication. Agents produce recommendations affecting Lease relationships. Each interaction with sovereignty creates risk; each requires deliberate handling.

### 2.5 Agents and Personnel

The Personnel Philosophy commits Robotanica to fair treatment of its people. As agents do more work, the relationship between agent capability and meaningful human work becomes ethically consequential. The Framework addresses this directly.

---

## 3. Principles

These principles bind agent governance and may not be set aside for capability convenience.

### 3.1 Mission Primacy

**AI-001** Agents serve the mission. They are tools in service of restoration, not actors with agendas of their own. Their design, training, evaluation, and deployment are oriented to mission outcomes.

### 3.2 Charter Conformance

**AI-002** Agent operation conforms to the Charter at every layer. Where agent behavior diverges from Charter principles, the Charter governs.

### 3.3 Human Oversight at Stakes

**AI-010** Decisions of consequence require human authorization. The threshold of "consequence" is defined per agent class and reviewed continuously.

**AI-011** Agents do not make decisions that affect Lease relationships, indigenous or community sovereignty, federation membership, or governance without human authorization.

### 3.4 Tier Discipline

**AI-020** The three-tier architecture is rigorously maintained. Agents do not operate at higher tiers than their authorization permits. Tier transitions require deliberate review (§9).

### 3.5 Transparency and Provenance

**AI-030** Every agent action is logged with full provenance: agent identity, action taken, inputs considered, output produced, time, signed by the agent's service identity.

**AI-031** Agent provenance is distinct from human provenance. Agent-authored content is identified as such throughout the platforms and the public record.

### 3.6 Outcome-Driven Evaluation

**AI-040** Agents are evaluated against ecological outcomes and mission objectives, not against agent-internal metrics like task completion or throughput.

**AI-041** Long-horizon outcomes (year 10, year 20 of restoration) are the dominant evaluation, not short-term proxies.

### 3.7 Conservative Default

**AI-050** When an agent encounters uncertainty, it defaults to conservative action: defer to humans, refuse to act, or take the lower-stakes alternative. Agents do not make confident decisions on inadequate evidence.

### 3.8 Reversibility

**AI-060** Agent actions favor reversible outcomes. Irreversible interventions (genetic releases, large-scale species introductions, major recipe applications) require human authorization regardless of agent capability.

### 3.9 Sovereignty Honor

**AI-070** Agents honor sovereignty declarations. Agents may not access, process, or generate content using data subject to sovereignty constraints in violation of those constraints.

### 3.10 No Hidden Capabilities

**AI-080** Capabilities deployed in agents are documented and reviewable. Hidden, undocumented, or undisclosed capabilities are not deployed.

### 3.11 Refusal of Mission-Incompatible Capability

**AI-090** Some capabilities are categorically refused (§6) regardless of operational benefit, performance gain, or external pressure.

### 3.12 Open Source Where Possible

**AI-100** Agents and their underlying models are open-source where this is consistent with safety and effectiveness. Where proprietary models are used, exit paths to open alternatives are maintained.

---

## 4. Scope of Review

### 4.1 What Counts as an Agent

For this Framework's purposes, an **AI agent** is a system that:

- Makes decisions, generates recommendations, performs actions, or produces content; AND
- Operates with some autonomy (does not require human input for every step); AND
- Affects entities, decisions, or outcomes within Robotanica's mission.

Systems that are pure tools (a calculator, a spell-checker, an indexer that returns search results without ranking judgment) are not agents under this Framework, though they may still warrant governance attention.

### 4.2 Categories of Agents

For governance purposes, agents are classified by domain:

- **Recipe agents** — agents involved in recipe recommendation, drafting, revision, or critique.
- **Verification agents** — agents involved in MRV analysis, anomaly detection, or verification support.
- **Operations agents** — agents involved in scheduling, dispatch, marketplace coordination, or logistics.
- **Communication agents** — agents involved in drafting, translating, or generating public or stakeholder communication.
- **Synthesis agents** — agents involved in Codex synthesis, literature review, or research summarization.
- **Personnel-adjacent agents** — agents involved in hiring, evaluation, or any decisions affecting personnel.
- **Edge agents** — agents operating at the edge on robots and field equipment, performing perception, classification, or operational decisions.

Each category has Framework provisions tuned to its specific risks.

### 4.3 What This Framework Reviews

The Framework reviews:

- New agent capabilities before deployment.
- Existing agent operation continuously.
- Tier transitions of agents (advisory → supervised → autonomous, or reverse).
- Significant capability extensions of existing agents.
- Substitution of underlying models or training data with materially different characteristics.
- Decommissioning of agents.

---

## 5. Tier Discipline (Reaffirmed)

The Framework reaffirms and extends the Gaia PRD's three-tier architecture (§7).

### 5.1 Tier 1 — Advisory

**T1-001** Tier 1 agents make recommendations, drafts, summaries, or analyses for human review. Every output is reviewed by a human before any consequential action follows.

**T1-002** Tier 1 outputs cannot directly affect entities, contracts, recipes, or governance. They can only enter the system through human-mediated steps.

**T1-003** Tier 1 agents may use sophisticated reasoning, draw on broad data, and produce extensive content. The check is on action, not on capability.

### 5.2 Tier 2 — Supervised Actuation

**T2-001** Tier 2 agents perform actions with bounded scope, where each action is approved by a human before execution.

**T2-002** Tier 2 actions are constrained to defined tool use; freeform reasoning does not flow into actuation.

**T2-003** Approval may be batch (e.g., approving a schedule for the week) but every action category is approved before its first execution and its parameters re-approved on material change.

### 5.3 Tier 3 — Autonomous Operations

**T3-001** Tier 3 agents perform high-frequency, low-stakes-per-action operations without per-action human authorization.

**T3-002** Tier 3 stakes are bounded structurally: edge perception, per-plant decisions, routine monitoring, anomaly flagging. Tier 3 cannot include decisions affecting Leases, governance, or other consequential domains.

**T3-003** Tier 3 agents are subject to bounded action spaces (geofencing, type limits, frequency limits) enforced at the edge and by oversight infrastructure.

**T3-004** Aggregate Tier 3 activity is monitored continuously; anomalous patterns trigger investigation.

### 5.4 No Tier 4

**TX-001** Robotanica does not deploy agents with autonomy beyond Tier 3. Any system whose autonomy exceeds Tier 3 bounds is, by definition, operating outside this Framework and is not authorized.

**TX-002** As AI capability evolves, the tier boundaries may be revisited, but the structural commitment to bounded autonomy is un-amendable in this Framework.

---

## 6. Categorical Limits

The following capabilities are categorically refused. Robotanica's agents do not have these capabilities, are not trained for them, and are not deployed in any configuration that approaches them. These limits apply regardless of operational benefit or capability availability.

### 6.1 No Autonomous Lease Decisions

**LIMIT-001** Agents do not autonomously create, sign, amend, terminate, or transfer Stewardship Leases. All Lease decisions require human authorization through A3 governance.

### 6.2 No Autonomous Recipe Approval at Scale

**LIMIT-002** Agents do not autonomously approve recipes for application at scale. Recipe approval requires Science Council review; agents may draft and analyze but not approve.

### 6.3 No Sovereignty Override

**LIMIT-003** Agents do not access, process, generate content from, or expose data subject to indigenous or community sovereignty in violation of the sovereign party's directives.

### 6.4 No Autonomous Verification Sign-Off

**LIMIT-004** Agents do not produce binding verification reports. Agents may analyze evidence, draft assessments, and flag anomalies; the verification signature requires a human verifier per MRV §7.

### 6.5 No Autonomous Personnel Decisions

**LIMIT-005** Agents do not autonomously make decisions affecting personnel: hiring, termination, compensation, performance evaluation, or assignment. These decisions require human authorization.

### 6.6 No Public Speech in Institutional Voice

**LIMIT-006** Agents do not autonomously publish content in Robotanica's institutional voice. All institutional public communication is human-reviewed before publication, even when agent-drafted.

### 6.7 No Autonomous Genetic or Biological Release

**LIMIT-007** Agents do not autonomously authorize genetic releases, novel species introductions, or significant biological deployments. These require human authorization with appropriate review (Science Council, Genetic Strategy governance).

### 6.8 No Autonomous Compensation Disbursement

**LIMIT-008** Agents do not autonomously disburse compensation, transfer credits in significant volume, or authorize material payments. Financial actions of consequence require human authorization.

### 6.9 No Manipulation Design

**LIMIT-009** Agents are not designed, trained, or deployed to manipulate, deceive, or exploit psychological vulnerabilities of users, partners, communities, or personnel. This applies to agents that interact with humans in any capacity.

### 6.10 No Adversarial Capability

**LIMIT-010** Agents are not designed, trained, or deployed for adversarial action against external parties, including parties hostile to Robotanica. Robotanica defends through Charter-compatible means; weaponized AI is outside scope.

### 6.11 No Surveillance Beyond Mission Need

**LIMIT-011** Agents do not perform surveillance of personnel, partners, communities, or members beyond what is necessary and proportionate to mission objectives. Mass surveillance is refused.

### 6.12 No Hidden Goals

**LIMIT-012** Agents are not deployed with goals or evaluation criteria not disclosed to those affected by the agent. Hidden goals — including hidden optimization for Robotanica's institutional benefit at the expense of stated mission — are refused.

---

## 7. Pre-Deployment Review

Before any new agent capability is deployed at material scale, a pre-deployment review is performed.

### 7.1 What Triggers Review

**PDR-001** Pre-deployment review is required for:

- New agent capabilities not previously deployed.
- Substitution of underlying models with materially different characteristics.
- Tier escalation of existing agents.
- Material expansion of agent action space, data access, or output domain.
- Introduction of agent capabilities in domains not previously served by agents.

### 7.2 Review Components

**PDR-010** Pre-deployment review includes:

- **Capability description** — what the agent does, in plain language.
- **Tier classification** — which tier the agent operates at, with rationale.
- **Categorical-limits compliance** — explicit confirmation that the agent does not approach §6 limits.
- **Failure mode analysis** — known and anticipated ways the agent could fail.
- **Bias and fairness assessment** — analysis of bias in training data, model, and outputs.
- **Sovereignty assessment** — interaction with indigenous and community sovereignty.
- **Personnel impact assessment** — effect on human work and personnel roles.
- **Provenance and logging design** — how agent actions will be recorded.
- **Monitoring and detection plan** — how anomalies and failures will be detected.
- **Sunset criteria** — conditions under which the agent will be retired.

### 7.3 Reviewing Bodies

**PDR-020** Review is conducted by:

- The **AI Ethics Review Board** (AIERB) — a body within Robotanica governance composed of technical AI specialists, ethics specialists, and representatives of affected parties (operators, communities, personnel as applicable).
- The **Science Council** for capabilities affecting recipes, MRV, or methodology.
- The **Stewardship Office** for capabilities affecting Lease relationships or indigenous and community partnerships.
- **Affected community representatives** for capabilities operating in indigenous or community contexts.

The composition adapts to the capability under review.

### 7.4 Review Outcomes

**PDR-030** Review may produce:

- **Approval** — the capability may be deployed as proposed.
- **Conditional approval** — deployment with specified conditions, monitoring, or limitations.
- **Phased approval** — deployment limited to defined scope or duration before broader deployment.
- **Refusal** — the capability is not deployed.

### 7.5 Public Record

**PDR-040** Pre-deployment reviews and outcomes are recorded in the public record. Capabilities approved for deployment are publicly disclosed (with implementation detail proportionate to security needs).

### 7.6 External Review

**PDR-050** Material capability deployments include external review by qualified parties not employed by Robotanica. External review provides perspective on Robotanica's internal blind spots.

---

## 8. Ongoing Monitoring

Once an agent is deployed, ongoing monitoring continues throughout its operational life.

### 8.1 Continuous Logging

**MON-001** Every agent action is logged with full provenance per AI-030. Logs are preserved per the Data Lifecycle and Preservation Plan.

### 8.2 Outcome Tracking

**MON-010** Agent-influenced decisions are tracked through to their ecological and operational outcomes. The agent's contribution to outcomes — direct and contributing — is monitored over time horizons appropriate to the decision (months for operations; years for recipes; decades for cohort outcomes).

### 8.3 Anomaly Detection

**MON-020** Statistical and qualitative anomaly detection monitors agent behavior for:

- Drift in recommendation patterns.
- Bias toward specific operators, regions, methodologies, or species.
- Unexpected concentration in outputs.
- Pattern changes following model updates or training-data refreshes.
- Pattern changes that could indicate compromise.

**MON-021** Detected anomalies trigger investigation by the AIERB.

### 8.4 Cross-Reference With Expert Judgment

**MON-030** Periodically, agent recommendations are compared in blinded form with expert ecological and methodological judgment. Sustained divergence between agent recommendations and expert assessment is signal worth investigation, regardless of which is "correct" in any specific case.

### 8.5 Federation Member Feedback

**MON-040** Federation members interacting with agents provide structured feedback. Patterns in feedback (operators reporting that recommendations consistently miss something; communities reporting that agent communication tone is off) inform monitoring.

### 8.6 Annual Audit

**MON-050** AI agents are audited annually by external parties qualified in AI ethics and the relevant domains. Audit findings are public.

---

## 9. Tier Transitions

Tier transitions — particularly elevations from supervised to autonomous — require deliberate review.

### 9.1 What Tier Transitions Require

**TIER-001** Tier elevation (e.g., a Tier 2 agent moving to Tier 3 in defined domains) requires:

- Pre-deployment review of the elevated tier (per §7).
- Demonstrated track record in the lower tier with quantified outcome alignment.
- Risk analysis specific to the higher tier.
- Reversibility plan: how the agent returns to lower tier if needed.
- Monitoring intensification commensurate with reduced human oversight.

### 9.2 Tier Demotion

**TIER-010** Tier demotion (an agent's autonomy reduced) is permitted at any time on operational or governance judgment. Demotion does not require special review; restoration to higher tier requires standard tier-transition review.

### 9.3 Reversibility Discipline

**TIER-020** Agents are designed for tier reversibility from the start. An agent designed only to operate at Tier 3 is not deployed; agents must function correctly at lower tiers as fallback.

### 9.4 No Permanent Tier 3

**TIER-030** No agent operates at Tier 3 permanently and unconditionally. Annual review confirms continued tier authorization; failure to confirm results in tier reduction.

---

## 10. Feedback Loop Integrity

The most subtle failure mode (Threat Model §6.10) is feedback-loop drift: agents recommending content that, over time, becomes Codex content, which trains future agents, which produce recommendations subtly biased toward agent preferences.

### 10.1 Agent-Authored Content Distinct

**FEED-001** Content authored or proposed by agents is distinguished in the Codex with `agent` provenance per AI-031.

### 10.2 Agent Proposals Subject to Human Review

**FEED-010** Agent contributions to the Codex go through the proposal-review-merge protocol of Gaia (PRD §6.5) the same as human contributions; agents do not have privileged write access.

### 10.3 Training Data Discipline

**FEED-020** Agent training data is curated to avoid agent-recommended-then-merged content as the dominant signal. Where agents are trained on Codex content that includes prior agent contributions, the training process accounts for this provenance.

**FEED-021** Training that creates strong feedback loops (agents trained primarily on outputs of prior agents) is refused.

### 10.4 External Ecological Reference

**FEED-030** Agent training and evaluation reference ecological knowledge and outcomes from sources external to the agent feedback chain: peer-reviewed scientific literature, indigenous and community knowledge sources, restoration outcomes from non-Robotanica projects.

### 10.5 Periodic Recalibration

**FEED-040** Recipe and Codex content periodically undergoes calibration against external benchmarks. Drift detected through this calibration triggers review of agent contributions to that content.

### 10.6 Indigenous Knowledge Protection

**FEED-050** Indigenous and traditional ecological knowledge contributed to the Codex is protected from agent processing where the contributing community has not consented to such processing. Sovereignty applies to training data the same as to operational data.

---

## 11. Bias, Fairness, and Sovereignty in Agent Operations

### 11.1 Pre-Deployment Bias Assessment

**BIAS-001** Pre-deployment review (§7) includes specific bias analysis:

- Bias in training data (geographic, cultural, methodological, linguistic).
- Bias in evaluation metrics (proxies favoring some outcomes over others).
- Bias in deployment context (where, with whom, under what default).

### 11.2 Ongoing Fairness Monitoring

**BIAS-010** Deployed agents are monitored for differential outcomes across:

- Bioregion and continent
- Federation member size and origin
- Indigenous-partnered versus non-indigenous-partnered work
- Recipe methodology
- Operator characteristics

Differential outcomes are not categorical violations; they may reflect substantive context. They warrant investigation, not automatic correction.

### 11.3 Sovereignty in Agent Operations

**BIAS-020** Agents operating in indigenous or community contexts:

- Use only data the community has consented to providing.
- Do not generate communication in community contexts without sovereignty-aware review.
- Honor community-determined limits on what agents may and may not do in their work.

**BIAS-021** Where indigenous communities prefer that no agents operate in their context, that preference is honored.

### 11.4 Linguistic and Cultural Adequacy

**BIAS-030** Communication and synthesis agents are evaluated for linguistic and cultural adequacy in the languages and contexts where they operate. Inadequate performance is reason for tier reduction or capability withdrawal.

---

## 12. Worker and Community Impact

### 12.1 Agents Augment, Not Displace

**WORK-001** Agents are designed and deployed to augment human work, not to displace meaningful work. Specifically:

- Tasks delegated to agents are typically tasks that are repetitive, scale-bound, or time-pressured — not the substantive judgment work of restoration practice.
- Where agents take on tasks previously performed by humans, the human role evolves rather than disappears.

### 12.2 Personnel Transition Support

**WORK-010** Where agent capability shifts personnel roles, transition support is provided per the Personnel and Compensation Philosophy: re-skilling, role evolution, time for adjustment.

### 12.3 No Forced Adoption

**WORK-020** Operators, communities, and personnel are not forced to use agent capabilities. Where agent capability and human practice produce comparable outcomes, the choice is supported.

### 12.4 Community Self-Determination

**WORK-030** Indigenous and local communities determine the role of agents in their work. Communities preferring to work without AI assistance, or with limited AI assistance, are supported.

### 12.5 Long-Horizon Work Preservation

**WORK-040** Long-horizon work — sustained relationships with land, communities, and ecosystems — is recognized as fundamentally human. Agent capabilities support but do not substitute for these relationships.

---

## 13. Failure Handling and Accountability

### 13.1 Agent Failure Detection

**FAIL-001** Agent failures are detected through:

- Anomaly detection (§8.3).
- Outcome tracking (§8.2).
- Federation member feedback (§8.5).
- Whistleblower reporting (Personnel Philosophy §11).
- External audit (§8.6).
- Routine cross-verification with expert judgment (§8.4).

### 13.2 Response to Detected Failure

**FAIL-010** When agent failure is detected:

- Affected actions are reviewed and, where warranted, reversed.
- Affected outcomes are reconciled per MRV reconciliation (§14).
- The agent's tier is reduced or its operation suspended pending investigation.
- Underlying cause is investigated by the AIERB.
- Remediation is documented in the public record.

### 13.3 Accountability for Agent Failures

**FAIL-020** Agent failures are accountable to humans:

- The deploying body (Robotanica organization, Federation governance) is responsible for the deployment.
- Personnel responsible for design, training, deployment, and monitoring are accountable for negligence in those roles.
- Agents themselves are not "responsible" in any morally meaningful sense; locating accountability solely in the agent is a refused move.

### 13.4 Affected Parties Made Whole

**FAIL-030** Parties harmed by agent failure (Landowners receiving wrong recommendations, communities affected by inappropriate communication, operators dispatched to inappropriate work) are made whole through reconciliation, compensation, or remediation as appropriate.

### 13.5 Pattern of Failure

**FAIL-040** Recurring failures in a category of agent operation trigger reassessment of whether the capability should continue to be deployed at all. Sustained failure may warrant capability withdrawal.

---

## 14. Decommissioning

### 14.1 When to Decommission

**DECOM-001** Agents are decommissioned when:

- Their capability has been superseded by improved alternatives.
- Their operation no longer serves the mission.
- Their failure rate or risk profile is no longer acceptable.
- The capability has been categorically refused (per §6) due to evolved understanding.

### 14.2 Decommission Process

**DECOM-010** Decommissioning includes:

- Notification to dependent systems and parties.
- Handoff of any in-flight work to alternative agents or human operators.
- Preservation of operational logs per the Data Lifecycle and Preservation Plan.
- Public record documentation of decommissioning and rationale.

### 14.3 Sunset Criteria From Deployment

**DECOM-020** Every agent deployment includes documented sunset criteria from the start. Sunset is planned, not afterthought.

---

## 15. Governance Structure

### 15.1 AI Ethics Review Board (AIERB)

**GOV-001** The AIERB is established within Robotanica governance to:

- Conduct pre-deployment reviews (§7).
- Monitor deployed agent operation.
- Investigate anomalies and failures.
- Recommend categorical-limits updates to governance.
- Liaise with the Science Council on agents affecting recipes, methodology, or verification.

**GOV-002** AIERB composition includes:

- Technical AI specialists with expertise in agent design, evaluation, and safety.
- Ethics specialists with expertise in AI ethics, sociotechnical systems, and applied ethics.
- Representatives of operator, community, and personnel constituencies affected by agent operations.
- At least one member with no Robotanica employment relationship, representing external perspective.

**GOV-003** AIERB members are subject to independence requirements similar to Science Council members (income threshold, conflict-of-interest disclosure, term limits).

### 15.2 Coordination With Other Bodies

**GOV-010** AIERB coordinates with:

- **Science Council** — for agents affecting recipes, MRV, or methodology.
- **Stewardship Office** — for agents affecting Lease relationships or community partnerships.
- **Federation governance** — for agents affecting federation membership or marketplace.
- **Communications Office** — for agents affecting public communication.

### 15.3 Veto Authority

**GOV-020** AIERB has veto authority over agent deployments within its scope. Veto may be:

- **Categorical** — a capability is refused outright.
- **Conditional** — deployment requires specified conditions.
- **Phased** — deployment is bounded in scope or duration.

**GOV-021** AIERB veto over agents affecting recipes, MRV, or methodology is coordinated with the Science Council's veto over those domains.

### 15.4 Annual Report

**GOV-030** AIERB publishes an annual report covering:

- Capabilities reviewed and outcomes
- Deployed agents under monitoring
- Anomalies investigated and outcomes
- Agent failures and remediation
- Categorical limits proposed, adopted, or revised
- External audit findings and responses

The annual report is public.

### 15.5 Review of This Framework

**GOV-040** This Framework is reviewed every three years (more frequent than other documents because AI capability evolution warrants more frequent reassessment) or sooner if material capability shifts warrant.

---

## 16. Open Questions

These are unresolved questions where decisions will have outsized downstream impact:

- **Capability frontier governance.** As AI capability advances, capabilities currently outside Robotanica's deployment may become available. The process for considering whether to deploy new capability classes (and the thresholds for categorical refusal) needs more development.
- **Foundation model dependency.** Most modern agents rely on foundation models (large language models, vision-language models). Robotanica's dependence on external model providers, the implications for capability changes outside Robotanica's control, and exit paths to open alternatives need explicit planning.
- **Agent-to-agent communication.** As agents become more capable, agent-to-agent coordination may emerge (agents in OpenFactory communicating with agents in Gaia). The Framework currently focuses on human-agent and agent-environment interactions; agent-agent dynamics need explicit governance.
- **Verifying long-horizon outcomes for agent decisions.** Year-10 outcome attribution for agent recommendations made today is operationally difficult — the agent that made the recommendation may no longer exist, the underlying model may be deprecated, the training data may be lost. Governance for long-horizon agent accountability needs more design.
- **Agent capabilities at the edge.** Field robots make many decisions per second on bounded data. The boundary between "tool" and "Tier 3 agent" at the edge is contested. Specific guidance for edge AI is needed.
- **Indigenous AI sovereignty.** Some indigenous communities are developing their own AI systems aligned to their knowledge traditions. Robotanica's interaction with indigenous AI (interoperability, respect for sovereignty, joint operation) is not yet specified.
- **Adversarial AI from outside Robotanica.** External actors may use AI agents in adversarial ways (disinformation, market manipulation, surveillance). Robotanica's defensive posture against external AI threats interacts with the Framework's refusal of adversarial capability internally; the boundary needs design.
- **Capability evolution beyond current understanding.** Some emerging AI capabilities may not fit cleanly into current categories. The Framework's revision process must keep pace with capability evolution; concrete mechanism needs development.

---

## Appendix A — Categorical Limits Summary

| Limit | What Is Refused |
|---|---|
| LIMIT-001 | Autonomous Lease decisions |
| LIMIT-002 | Autonomous recipe approval at scale |
| LIMIT-003 | Sovereignty override |
| LIMIT-004 | Autonomous verification sign-off |
| LIMIT-005 | Autonomous personnel decisions |
| LIMIT-006 | Public speech in institutional voice |
| LIMIT-007 | Autonomous genetic or biological release |
| LIMIT-008 | Autonomous compensation disbursement |
| LIMIT-009 | Manipulation design |
| LIMIT-010 | Adversarial capability |
| LIMIT-011 | Surveillance beyond mission need |
| LIMIT-012 | Hidden goals |

---

## Appendix B — Cross-References

- **Robotanica Charter** §2.8 (reversibility), §2.9 (transparent failure), §3.5 (commitments to people)
- **Gaia PRD** §7 (agent architecture)
- **MRV Specification** §7 (verification independence — applies to agent verification)
- **Threat Model** §4.10 (agent failure modes), §6.10 (agent drift scenario)
- **Science Council Charter** (composition and independence as model for AIERB)
- **Personnel and Compensation Philosophy** §3.7 (right of refusal), §11 (whistleblower protection)
- **Public Communication Doctrine** §3.4 (voice discipline)

---

## Appendix C — Glossary (AI-Ethics-Specific)

- **Agent** — A system that makes decisions, generates recommendations, performs actions, or produces content with some autonomy and material effect.
- **AIERB** — AI Ethics Review Board, the governance body within Robotanica responsible for agent ethical review.
- **Categorical limit** — A capability that is refused outright regardless of operational benefit.
- **Edge agent** — An agent operating at the edge on robots and field equipment.
- **Feedback loop integrity** — The discipline preventing agents from progressively biasing the Codex through their own contributions.
- **Pre-deployment review** — The review process before any new agent capability is deployed.
- **Sunset criteria** — Conditions under which an agent will be retired, defined at deployment.
- **Tier** — One of three levels of agent autonomy: advisory, supervised actuation, autonomous operations.
- **Tier transition** — Movement of an agent between tiers, particularly elevation.

---

*AI agents are tools in service of restoration. They are not actors with their own agendas. Their capability evolves; their governance must keep pace. This Framework specifies how Robotanica governs its agents so that the most consequential failure mode — slow drift toward outcomes the agents implicitly favor — is detected and prevented, and so that agent capability advances the mission rather than substituting for it.*
