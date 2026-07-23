# Roadmap

Four phases. Each ships artefacts that are usable on their own — this kit is meant to be
useful from the first release, not at the end of the last one.

Track these as GitHub Milestones.

---

## Milestone 1 — Foundations

**Goal:** an architect can take a proposal through a review board using only what is here.

| Issue | Deliverable |
| --- | --- |
| ADR template and guidance | Template, worked guidance, anti-patterns |
| Solution design document template | The document a review board reads |
| AI threat model template | LLM-specific threats beyond a standard STRIDE pass |
| Production readiness checklist | Gate criteria before real traffic |
| Security review checklist | The reviewer's questions, published in advance |
| Model certification criteria | Risk tiers and approval evidence |
| Guardrails baseline | Minimum controls per tier |
| C4 conventions for AI systems | Diagramming conventions and Mermaid starters |
| Pattern catalogue index | Which reference architecture fits which problem |

**Exit criteria:** every checklist item states how it is verified, not only what is required.

---

## Milestone 2 — Worked examples

**Goal:** show the artefacts filled in, not just blank. Templates without an example are
guessed at.

| Issue | Deliverable |
| --- | --- |
| Worked example: enterprise RAG assistant | Full design doc, threat model, tier assessment |
| Worked example: agentic workflow with tool access | Higher tier, tighter controls |
| Worked example: batch document classification | Low tier, showing proportionate review |
| Filled ADR set | Six real decisions with real trade-offs |

**Exit criteria:** a reader can diff a worked example against the blank template and see
exactly what good looks like.

---

## Milestone 3 — Evaluation playbook

**Goal:** turn "the model is good enough" into a defensible, evidenced statement.

| Issue | Deliverable |
| --- | --- |
| Evaluation strategy by use case | What to measure for RAG, agents, classification |
| Golden dataset guidance | Building, sizing, and maintaining one |
| Human review protocol | Sampling, rubric, inter-rater agreement |
| Regression gates | Blocking a release on measured quality |
| Drift monitoring | Detecting degradation after launch |

**Exit criteria:** every metric names its threshold and who owns the decision when it fails.

---

## Milestone 4 — Cost and operating model

**Goal:** the part every AI programme discovers too late.

| Issue | Deliverable |
| --- | --- |
| Cost model template | Per-request accounting: tokens, retrieval, infrastructure |
| Capacity and quota planning | Rate limits, burst behaviour, provider fallback |
| FinOps guardrails | Budget alerts, per-team attribution, kill switches |
| Operating model | Who runs it, who owns quality, escalation paths |
| Decommissioning criteria | When to retire an AI system, and how |

**Exit criteria:** a finance stakeholder can read the cost model without a translator.
