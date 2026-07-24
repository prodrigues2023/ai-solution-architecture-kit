# AI Solution Architecture Kit

> The artefacts an enterprise needs before it approves an AI system — decision records,
> design templates, review checklists, and model certification criteria.

[![Phase](https://img.shields.io/badge/phase-1%20foundations-blue)](./ROADMAP.md)
[![Templates](https://img.shields.io/badge/templates-3-green)](./templates)
[![License](https://img.shields.io/badge/license-CC%20BY%204.0-lightgrey)](./LICENSE)

There is no shortage of material on how to build AI features. There is very little on how
an organisation decides whether it is allowed to ship one — who signs off, against which
criteria, and what evidence they need to see.

This kit is that missing half. Everything here is a working document you can copy into your
own organisation, adapt, and put in front of a review board.

**Português:** [README.pt-BR.md](./README.pt-BR.md)

---

## Contents

| Artefact | What it is for |
| --- | --- |
| [ADR template](./templates/adr-template.md) | Recording architecture decisions so the reasoning survives the people |
| [Solution design document](./templates/solution-design-document.md) | The one document a review board actually reads |
| [AI threat model](./templates/threat-model-ai.md) | Threats specific to LLM systems, beyond the usual STRIDE pass |
| [Production readiness checklist](./checklists/production-readiness.md) | What must be true before an AI system carries real traffic |
| [Security review checklist](./checklists/security-review.md) | What a security reviewer asks, so you can answer before they ask |
| [Model certification criteria](./governance/model-certification.md) | How to approve a model for a risk tier, repeatably |
| [Guardrails baseline](./governance/guardrails-baseline.md) | The minimum controls, by risk tier |
| [C4 conventions](./diagrams/c4-conventions.md) | Diagramming AI systems consistently, in Mermaid |
| [Pattern catalogue](./patterns/README.md) | Reference architectures and when each one applies |

## Who this is for

**Architects** proposing an AI system and needing to survive a review board.
**Review boards and AI committees** needing consistent criteria instead of case-by-case
judgement.
**Engineering leads** who have been told to "add guardrails" and need to know what that
means concretely.

## How to use it

Copy what you need. Delete what does not apply. These documents are deliberately opinionated
so that adapting them requires you to disagree explicitly — a template that fits every
organisation constrains none of them.

The one thing worth keeping intact is the **risk tiering** in
[model-certification.md](./governance/model-certification.md). Most of the other documents
key off it, and a tier system everyone recognises is worth more than a perfect one nobody
uses.

## Roadmap

See [ROADMAP.md](./ROADMAP.md). Phase 1 establishes the core artefacts; later phases add
worked examples, an evaluation playbook, and a cost-governance model.

## Related

The kit specifies what evidence a review requires. These repositories are worked examples of
producing it:

- [enterprise-ai-framework](https://github.com/prodrigues2023/enterprise-ai-framework) — the framework that gives the [guardrail baseline](./governance/guardrails-baseline.md) a single place to be enforced across applications
- [rag-reference-architecture](https://github.com/prodrigues2023/rag-reference-architecture) — a reference architecture documented the way the [solution design template](./templates/solution-design-document.md) asks for
- [rag-evaluation-toolkit](https://github.com/prodrigues2023/rag-evaluation-toolkit) — the evaluation evidence that [model certification](./governance/model-certification.md) requires at Tier 2 and above
- [mcp-servers-collection](https://github.com/prodrigues2023/mcp-servers-collection) — designing the tool surfaces that [excessive agency](./templates/threat-model-ai.md) is assessed against
- [event-driven-dotnet-reference](https://github.com/prodrigues2023/event-driven-dotnet-reference) — reliable messaging between services: outbox, idempotent consumers, sagas

## Contributing

Disagreement is the most useful contribution. If a checklist item does not survive contact
with your organisation, open an issue saying why — that is the feedback that makes these
documents real rather than aspirational.

## Author

Paulo Roberto Franco Rodrigues — AI Solutions Architect.
Twenty years in distributed systems and solution architecture; recently designing
cloud-native AI platforms on AWS and Azure, and serving on an enterprise AI architecture
committee defining guardrails, model certification, and framework governance.
[LinkedIn](https://linkedin.com/in/paulo-roberto-franco-rodrigues)

## License

[CC BY 4.0](./LICENSE) — use it commercially, adapt it, just keep the attribution.
