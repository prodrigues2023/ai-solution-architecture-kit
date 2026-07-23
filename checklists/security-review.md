# Security review checklist

The questions a security reviewer will ask about an AI system. Published in advance so
teams can answer them before the review rather than during it.

This covers the AI-specific surface. It assumes your standard application security review —
authentication, dependencies, transport, infrastructure — is run separately and passed.

---

## 1. Trust boundaries

- Where does untrusted content enter? List every source.
- Which of those sources can an external party influence? Uploaded files, shared mailboxes, wikis with broad write access, third-party feeds, and web content all qualify.
- Is retrieved content treated as data, or is it concatenated into the instruction block?
- Can the model reach the network, a shell, a database, or a file system — directly or through a tool?

**Reviewer's real question:** if an attacker can write one document into your index, what is
the worst outcome?

## 2. Access control

- Are permissions resolved at query time from the identity provider, or cached?
- Are filters applied inside the retrieval query, or after ranking?
- Is there a test proving user A cannot retrieve user B's content?
- Do tools execute with the *user's* privileges or the *service's*?
- Is tenant isolation enforced in the data layer, or only in the prompt?

**Instant fail:** isolation implemented only through prompt instructions. "Only answer about
tenant X" is not a security control.

## 3. Data flow to third parties

- What exactly is sent to the model provider? Include system prompts, retrieved passages, and user content.
- Which contractual terms apply — training use, retention, sub-processors?
- Where is inference performed, and does the region satisfy residency requirements?
- Is personal data redacted before the boundary, and how is redaction verified?
- Are prompts and completions logged? Where, for how long, and who can read them?

## 4. Prompt injection resilience

- What controls exist at input, and at retrieved-context level?
- What is the blast radius of a successful injection — is it a wrong answer, or an action?
- Which actions require human confirmation?
- Is there a red-team suite in CI? When did it last find something?

**Reviewer's real question:** you cannot prevent injection, so show me that succeeding at it
does not matter much.

## 5. Output handling

- Is structured output schema-validated before use?
- Is output encoded before rendering? Can it introduce script into a page?
- Can output reach a shell, a query engine, or a template renderer?
- Can output contain a URL that a client fetches automatically? (A rendered image is an exfiltration channel.)
- Is output scanned for secrets and classified data before it reaches the user?

## 6. Agency and actions

- Enumerate every tool and every write path.
- For each: reversible or not? Blast radius? Rate-limited?
- Is there an iteration cap on agent loops, with a terminal state?
- Is every tool invocation audited with the originating prompt and user?
- Can a tool call be triggered by content the model retrieved rather than by the user?

## 7. Secrets and configuration

- Are any credentials, keys, or endpoints present in a system prompt? (Assume every prompt is recoverable.)
- Are provider API keys in a managed vault, rotated, and scoped?
- Does CI scan for secrets in prompts and prompt templates, not only in code?

## 8. Availability and cost abuse

- Hard token cap per request? Per user, per period?
- What does the most expensive possible single request cost?
- Can a user trigger unbounded retrieval or recursion?
- Is there a circuit breaker on budget, and who is alerted?

## 9. Supply chain

- Are model versions pinned?
- Are third-party prompts, agents, plugins, or MCP servers in the request path? Who reviewed them?
- What changes if the provider silently updates the model?

## 10. Monitoring and response

- Is there a trace covering the full request path, including retrieved sources?
- Would you detect a successful data exfiltration attempt? How?
- Does the incident process cover a wrong-answer incident and a prompt-injection incident?
- Can you answer "where did this answer come from?" for a request from three weeks ago?

---

## Review outcome

| Finding | Severity | Decision | Owner | Due |
| --- | --- | --- | --- | --- |

**Approval conditions.** State any control required before launch, and any accepted risk
with its owner and review date. An accepted risk without both is not accepted — it is
forgotten.
