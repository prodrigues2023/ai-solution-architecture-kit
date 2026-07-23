# AI threat model template

A standard STRIDE pass over an AI system finds the API threats and misses everything that
makes the system an AI system. This template covers the difference. Run it *in addition to*
your existing threat modelling, not instead of it.

---

## Scope

- System under review:
- Risk tier ([criteria](../governance/model-certification.md)):
- Trust boundaries — mark every point where untrusted content enters
- Date and participants:

## The core insight

**Retrieved content is untrusted input.** A document in your own knowledge base, indexed by
your own pipeline, is attacker-controlled the moment an attacker can influence that document.
The model cannot distinguish instructions you wrote from instructions embedded in a page it
retrieved. Every threat below follows from this.

---

## 1. Prompt injection

| | |
| --- | --- |
| **Direct** | A user instructs the model to ignore its instructions, reveal its prompt, or act outside its role |
| **Indirect** | Instructions hidden in retrieved content — a document, a web page, an email, a code comment |

Indirect injection is the dangerous one, because it needs no access to your interface.

**Assess:**
- Which content sources can an attacker influence? Consider uploaded files, shared inboxes, wikis anyone can edit, and third-party feeds
- What is the worst action the model can take on the attacker's behalf?
- Are there tools or write actions reachable through a successful injection?

**Controls to consider:**
- Treat retrieved content as data: delimit it clearly and never concatenate it into the instruction block
- Constrain tool access by the *user's* permissions, never the model's
- Require human confirmation for irreversible or outward-facing actions
- Validate outputs against a schema before acting on them
- Detection on retrieved content — imperfect, and never the only control

## 2. Data exfiltration

The model has access to more data than the user does, and an attacker uses the model as the
retrieval mechanism.

**Assess:**
- Are permissions applied *before* retrieval, or filtered out afterwards?
- Can a user reach another tenant's data through a crafted query?
- Can the model emit data through a side channel — a rendered image URL, a link, a tool call to an external endpoint?
- Is training or fine-tuning data reachable through extraction prompts?

**Controls to consider:**
- Permission filters applied inside the store, at query time — a post-filter that shrinks results silently is a vulnerability, not an inconvenience
- Egress restrictions on tools and on rendered content
- Output scanning for identifiers and classified data patterns
- Never place secrets in a system prompt; assume every prompt is recoverable

## 3. Excessive agency

The model can do more than the use case requires, so a single failure becomes a large one.

**Assess:**
- Enumerate every tool, every write path, and every external call the model can trigger
- For each: what is the blast radius of a wrong invocation?
- Which are reversible? Which are not?

**Controls to consider:**
- Least privilege per tool, scoped to the acting user
- Human approval gates on irreversible actions — deletion, payment, sending, publishing
- Rate limits per user and per session, not only globally
- Full audit trail of tool invocations with the originating prompt

## 4. Output integrity

The model is confidently wrong, and a downstream system or a person acts on it.

**Assess:**
- What decisions are made from the output, and by whom?
- Is the output parsed by another system? What happens on malformed output?
- Can the output reach a browser, a shell, or a query engine? (XSS, command injection, SQL injection — through the model)
- What is the cost of a plausible-but-wrong answer that nobody catches?

**Controls to consider:**
- Schema validation on every structured output
- Encode and sanitise before rendering; never execute model output
- Citations, so users can verify rather than trust
- Refuse rather than guess when grounding is weak

## 5. Availability and cost

Denial of wallet is the AI-specific availability threat, and it is cheap to mount.

**Assess:**
- What does a single request cost at the maximum context size?
- Can a user trigger unbounded retrieval, unbounded generation, or a recursive agent loop?
- What happens when the provider rate-limits or goes down?

**Controls to consider:**
- Hard token caps per request and per user per period
- Iteration limits on agent loops, with a terminal state
- Budget alerts with an automatic circuit breaker
- Documented degraded mode and provider fallback

## 6. Supply chain

**Assess:**
- Model provenance — who published the weights or operates the endpoint?
- Third-party prompts, agents, plugins, or MCP servers in the path
- Contractual terms on training with your data
- Model version changes: are they pinned, or does behaviour shift silently underneath you?

**Controls to consider:**
- Pin model versions; treat an upgrade as a change requiring re-evaluation
- Review third-party components in the prompt or tool path as you would a dependency
- Confirm the provider's data-use terms in writing, per environment

## 7. Privacy and compliance

**Assess:**
- Does personal data reach the model provider? Under which legal basis?
- Where is it processed, and does that satisfy residency requirements?
- How does a deletion request reach embeddings, caches, and logs?
- Are prompts and completions logged? Who can read those logs?

**Controls to consider:**
- Redaction before the provider boundary
- Retention limits on prompt and completion logs, enforced automatically
- A documented, tested deletion path covering derived data
- Data protection assessment where the risk tier requires one

---

## Findings

| # | Threat | Likelihood | Impact | Decision | Owner | Due |
| --- | --- | --- | --- | --- | --- | --- |
| 1 |  |  |  | Mitigate / Accept / Transfer / Avoid |  |  |

Accepted risks need a named owner and a review date. An accepted risk with neither is an
ignored risk wearing a better name.
