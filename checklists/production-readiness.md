# Production readiness checklist

What must be true before an AI system carries real traffic. Every item states **how it is
verified** — an unverifiable checklist is a wish list.

Mark each: ✅ done · ⚠️ accepted risk, with owner and date · ❌ blocking.

---

## Architecture and design

| # | Item | Verified by |
| --- | --- | --- |
| 1 | Solution design document approved at the required authority | Approval record |
| 2 | Risk tier assigned and confirmed | Design document, section 8 |
| 3 | Significant decisions recorded as ADRs | ADR index exists and is current |
| 4 | Diagrams match what was built | Reviewed against deployed components |
| 5 | Fallback behaviour defined for model unavailability | Documented and tested by fault injection |

## Model and evaluation

| # | Item | Verified by |
| --- | --- | --- |
| 6 | Model certified for this tier and pinned to a version | Registry entry |
| 7 | Evaluation run against a golden dataset | Published results with thresholds |
| 8 | Quality thresholds defined, with an owner for breaches | Named role |
| 9 | Regression suite runs in CI and can block a release | Pipeline configuration |
| 10 | Known failure modes documented and communicated to users | User-facing limitations note |
| 11 | Prompts versioned and promoted through environments | Prompt registry or repository |

## Guardrails

| # | Item | Verified by |
| --- | --- | --- |
| 12 | Baseline controls for the tier implemented | [Guardrails baseline](../governance/guardrails-baseline.md) mapping |
| 13 | Permission filters applied inside the store | Code review plus a cross-tenant test |
| 14 | Red-team suite passes | CI run |
| 15 | Token caps and rate limits enforced | Load test at the limit |
| 16 | Refusal path behaves correctly on out-of-scope questions | Test cases |

## Security and privacy

| # | Item | Verified by |
| --- | --- | --- |
| 17 | Threat model completed, findings resolved or accepted | Signed threat model |
| 18 | Security review passed | [Security checklist](./security-review.md) |
| 19 | Secrets in a managed vault, never in prompts or configuration | Secret scan in CI |
| 20 | Data classification confirmed for everything crossing the provider boundary | Data flow review |
| 21 | Retention configured for prompts, completions, and embeddings | Storage policy |
| 22 | Deletion path reaches derived data, and has been tested | Executed test with evidence |

## Operations

| # | Item | Verified by |
| --- | --- | --- |
| 23 | Tracing spans the full path: request, retrieval, model, response | Trace from a real request |
| 24 | Cost per request measured and attributed to a team | Dashboard |
| 25 | Alerts on latency, error rate, cost, and quality drift | Alert definitions with thresholds |
| 26 | Runbook for the top five failure modes | Runbook reviewed by on-call |
| 27 | On-call ownership agreed and staffed | Rota |
| 28 | Rollback tested, including to a previous prompt version | Rehearsed |
| 29 | Load tested at expected peak, plus headroom | Test report |

## Users and change

| # | Item | Verified by |
| --- | --- | --- |
| 30 | Users know they are interacting with an AI system | Interface review |
| 31 | Limitations communicated in the interface, not only in documentation | Interface review |
| 32 | Feedback mechanism exists and is routed to the owning team | Working end to end |
| 33 | Escalation path to a human is available and staffed | Documented |
| 34 | Baseline metric captured *before* launch | Recorded, with date |

## Governance

| # | Item | Verified by |
| --- | --- | --- |
| 35 | Named accountable owner — a person, not a team | Named in the design document |
| 36 | Re-certification date set | Calendar entry with an owner |
| 37 | Decommissioning criteria defined (Tier 3) | Design document |
| 38 | Incident process covers AI-specific failures | Process document |

---

## Using this in a go/no-go

Blocking items are those where a failure has no compensating control: 6, 13, 17, 19, 22, 23,
28, 35. The rest can carry an accepted risk with an owner and a date.

**Item 34 is the one teams skip and later regret.** Without a pre-launch baseline, the
system cannot demonstrate improvement, and the first budget review becomes an argument about
anecdotes. Capture it before launch or accept that the value claim will be unprovable.
