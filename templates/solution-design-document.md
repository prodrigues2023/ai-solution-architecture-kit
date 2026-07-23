# Solution design document template

The single document a review board reads. Aim for eight to twelve pages. Anything longer
gets skimmed, and skimming is how bad designs get approved.

---

## 1. Summary

Three paragraphs, maximum. The problem, the proposed solution, and what you are asking the
board to approve. Written so a non-specialist executive understands it.

## 2. Problem and business context

- What problem is being solved, and for whom
- Current process, and what it costs today in time, money, or error rate
- Why now
- What happens if nothing is done

**If you cannot state a measurable current cost, stop here.** An AI system without a
baseline cannot demonstrate value later, and it will be cancelled in the first budget review.

## 3. Scope

- **In scope:** what the system will do
- **Out of scope:** what it will not do, explicitly
- **Non-goals:** things a reader would reasonably assume are included, but are not

## 4. Users and use cases

Who uses it, what they are trying to accomplish, how often, and what they do today instead.
Include the case where the system fails or refuses — that path is part of the design.

## 5. Solution architecture

- C4 context diagram — see [C4 conventions](../diagrams/c4-conventions.md)
- C4 container diagram
- Component responsibilities, one line each
- Data flow, including where data crosses a trust boundary

## 6. AI-specific design

The section a generic design template omits, and the one the board is actually there for.

| Question | Your answer |
| --- | --- |
| Which models, and why those |  |
| Where does the model run, and who operates it |  |
| Grounding strategy — retrieval, tools, fine-tuning, none |  |
| How is output validated before it reaches the user |  |
| What happens when the model is wrong |  |
| What happens when the model is unavailable |  |
| Is there a human in the loop, and for which actions |  |
| How will quality be measured, before and after launch |  |

## 7. Data

- Sources, classification, and residency
- What is sent to the model provider, and under which contractual terms
- Retention for prompts, completions, and embeddings
- How personal data is identified and handled
- How a deletion request propagates to derived data such as embeddings

## 8. Security

Reference the completed [threat model](./threat-model-ai.md) and
[security review checklist](../checklists/security-review.md). In this document, summarise:

- Authentication and authorisation, including how permissions reach retrieval
- Tenant and data isolation
- Guardrails applied, per the [baseline](../governance/guardrails-baseline.md)
- Risk tier and its justification — see [model certification](../governance/model-certification.md)

## 9. Quality attributes

Numbers, not adjectives. "Fast" is not a target; "p95 under 3 seconds" is.

| Attribute | Target | How measured |
| --- | --- | --- |
| Latency (p95) |  |  |
| Throughput |  |  |
| Availability |  |  |
| Answer quality |  |  |
| Cost per 1,000 requests |  |  |

## 10. Alternatives considered

At least two, each with why it was rejected. "We considered doing nothing" is a legitimate
and often instructive entry.

A design document with no rejected alternatives is a proposal, not a design.

## 11. Risks and mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |

Include the risks you would rather not raise. A board that discovers a known risk after
approval will not approve your next proposal.

## 12. Delivery plan

Phases, dependencies, and what each phase proves. Name the point at which the project would
be cancelled if the evidence does not appear.

## 13. Open questions

What is genuinely undecided, and who needs to decide it. Leaving this section empty when it
should not be is the fastest way to lose a board's trust.

## 14. Decision requested

State plainly what approval you are asking for, and what you will do next if it is granted.
