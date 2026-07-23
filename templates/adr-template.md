# ADR template

Copy the block below into `docs/adr/NNNN-short-title.md` in your own repository.

---

```markdown
# ADR-NNNN: Short title stating the decision

- **Status:** Proposed | Accepted | Superseded by ADR-XXXX
- **Date:** YYYY-MM-DD
- **Deciders:** roles, not names

## Context

The forces at play. What requirement or constraint forced a decision here? What options
were considered, and why was each viable or not?

Write this so someone joining in two years understands the situation you were in — not the
situation you are in now.

## Decision

What was decided, in the active voice: "We will use X." State what was deliberately
deferred as well as what was chosen.

## Consequences

**Positive** — what this buys.

**Negative** — what it costs, and what the team will have to live with.

An ADR with no negative consequences has not been thought through. Every real decision
trades something away.
```

---

## Guidance

**What deserves an ADR.** A decision is architecturally significant if reversing it later
would require changing more than one component, or would change the system's cost, latency,
or security profile. Choosing a vector store qualifies. Choosing a logging library does not.

**Immutability.** Accepted ADRs are not edited. A decision that changes gets a new ADR, and
the old one is marked `Superseded by ADR-XXXX`. The history is the point — a reader needs to
see that you once chose differently and why you changed.

**Length.** One page. If an ADR needs three pages of context, the context belongs in a
design document that the ADR links to.

**Timing.** Write it when the decision is made, not when the sprint ends. An ADR written
retroactively documents the outcome and loses the alternatives, which were the valuable part.

## Decisions worth recording in an AI system

Recurring ones, offered as a starting list:

- Model selection, and the policy for changing models
- Embedding model selection and re-embedding strategy on version change
- Chunking strategy
- Vector store selection and the portability boundary around it
- Retrieval strategy: dense, lexical, hybrid, re-ranking
- Prompt versioning and promotion between environments
- Guardrail placement: input, output, or both
- Human-in-the-loop boundaries — which actions require approval
- Data retention for prompts and completions
- Provider fallback behaviour when the primary model is unavailable

## Anti-patterns

**The rubber stamp.** An ADR written after implementation, listing one option. It records
nothing; delete it and save the reader the time.

**The essay.** Six pages of background with the decision buried in the middle. If a reader
cannot find the decision in ten seconds, the format has failed.

**The consequence-free decision.** "Positive: it's better. Negative: none." This is the most
common failure and the clearest signal that alternatives were never seriously weighed.

**The orphan.** An ADR nobody links to from the design document or the code. Reference ADRs
from the architecture overview, and from the module they govern.
