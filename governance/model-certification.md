# Model certification criteria

The purpose of certification is to make approval **repeatable**. Without it, every AI
proposal is judged on the persuasiveness of whoever presents it, and the organisation
cannot explain to a regulator, an auditor, or itself why one system was approved and
another was not.

Certification answers one question: *is this model approved for this use, at this risk
level, with this evidence?*

---

## Risk tiers

Tier is a property of the **use case**, not the model. The same model can be Tier 1 in one
application and Tier 3 in another.

| Tier | Definition | Examples |
| --- | --- | --- |
| **Tier 1 — Low** | Output is reviewed by a human before any effect. No personal or confidential data. Errors are inconvenient. | Draft generation, internal summarisation, code suggestions |
| **Tier 2 — Moderate** | Output reaches users directly, or confidential data is processed. Errors cause rework or embarrassment. | Internal knowledge assistant, document classification, customer-facing FAQ |
| **Tier 3 — High** | Output influences a decision about a person, or the system acts autonomously with real effect. Errors cause material harm. | Claims triage, credit pre-assessment, agents with write access to production systems |
| **Tier 4 — Prohibited** | The organisation does not do this, regardless of the safeguards proposed. | Fully automated decisions with legal effect on a person; inference of protected characteristics; anything on the organisation's published prohibited list |

### Assigning a tier

Answer in order. The first "yes" sets the tier.

1. Is it on the prohibited list? → **Tier 4. Stop.**
2. Does it act autonomously with irreversible effect, or influence a decision about a person? → **Tier 3**
3. Does output reach an end user without human review, or is confidential data processed? → **Tier 2**
4. Otherwise → **Tier 1**

Tier is assigned by the proposing architect and confirmed at review. Where there is
disagreement, the higher tier applies until evidence justifies lowering it.

---

## Evidence required by tier

| Requirement | T1 | T2 | T3 |
| --- | --- | --- | --- |
| Solution design document | ● | ● | ● |
| Approved model from the registry | ● | ● | ● |
| Threat model completed | | ● | ● |
| Security review passed | | ● | ● |
| Evaluation results against a golden dataset | | ● | ● |
| Human review protocol, with sampling rate | | | ● |
| Bias and fairness assessment | | | ● |
| Data protection assessment | | ● (if personal data) | ● |
| Documented fallback when the model fails | | ● | ● |
| Named accountable owner | ● | ● | ● |
| Post-launch monitoring plan | | ● | ● |
| Decommissioning criteria | | | ● |

**Approval authority:** Tier 1 — engineering lead. Tier 2 — architecture review. Tier 3 —
AI committee, with security and legal represented.

---

## The model registry

Certification is against a registry entry, not against a vendor name. "We use GPT-class
models" is not a certification.

Each entry records:

| Field | Notes |
| --- | --- |
| Model identifier and version | Pinned. `latest` is not a version |
| Provider and hosting region | Determines residency and contractual terms |
| Approved tiers | The highest tier this model may serve |
| Data handling terms | Whether inputs may be used for training; retention by the provider |
| Known limitations | Documented failure modes and evaluation gaps |
| Evaluation date and results | Against the organisation's own suite, not only public benchmarks |
| Review date | Certification expires; see below |
| Accountable owner | A role |

**Version pinning is the point.** A provider updating a model behind an unpinned alias
changes system behaviour with no change on your side and no re-evaluation. Treat a model
version change as a change requiring re-certification proportionate to the tier.

---

## Re-certification

Certification is not permanent. Re-certify when:

- The model version changes — always, at every tier
- The use case changes tier
- Evaluation metrics degrade past their threshold
- Twelve months pass — annually for Tier 2 and Tier 3
- A serious incident occurs in this system or in another using the same model

## What certification does not do

Worth stating plainly, because it is routinely misread:

- It does not guarantee correct output. It records that the risk was assessed and the
  evidence reviewed.
- It does not transfer accountability to the committee. The named owner remains accountable.
- It does not replace monitoring. Most AI failures appear after launch, in the gap between
  the evaluation set and reality.
