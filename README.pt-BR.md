# AI Solution Architecture Kit

> Os artefatos que uma empresa precisa antes de aprovar um sistema de IA — registros de
> decisão, templates de design, checklists de revisão e critérios de certificação de modelos.

[![Fase](https://img.shields.io/badge/fase-1%20fundamentos-blue)](./ROADMAP.md)
[![Templates](https://img.shields.io/badge/templates-3-green)](./templates)
[![Licença](https://img.shields.io/badge/licen%C3%A7a-CC%20BY%204.0-lightgrey)](./LICENSE)

Não falta material sobre como construir funcionalidades de IA. Falta material sobre como uma
organização decide se pode colocá-las em produção — quem aprova, com quais critérios e quais
evidências precisa ver.

Este kit é essa metade que falta. Tudo aqui é documento de trabalho: copie para a sua
organização, adapte e leve para um comitê de arquitetura.

**English:** [README.md](./README.md)

---

## Conteúdo

| Artefato | Para que serve |
| --- | --- |
| [Template de ADR](./templates/adr-template.md) | Registrar decisões para que o raciocínio sobreviva às pessoas |
| [Documento de design de solução](./templates/solution-design-document.md) | O documento que um comitê realmente lê |
| [Threat model para IA](./templates/threat-model-ai.md) | Ameaças específicas de sistemas com LLM, além do STRIDE tradicional |
| [Checklist de prontidão para produção](./checklists/production-readiness.md) | O que precisa ser verdade antes de receber tráfego real |
| [Checklist de revisão de segurança](./checklists/security-review.md) | As perguntas do revisor, publicadas antes da revisão |
| [Critérios de certificação de modelos](./governance/model-certification.md) | Como aprovar um modelo por nível de risco, de forma repetível |
| [Baseline de guardrails](./governance/guardrails-baseline.md) | Os controles mínimos por nível de risco |
| [Convenções C4](./diagrams/c4-conventions.md) | Diagramar sistemas de IA de forma consistente, em Mermaid |
| [Catálogo de padrões](./patterns/README.md) | Arquiteturas de referência e quando cada uma se aplica |

> Os documentos técnicos são mantidos em inglês para alcançar o público mais amplo possível.
> Este README traz o contexto em português.

## Para quem é

**Arquitetos** propondo um sistema de IA e que precisam passar por um comitê.
**Comitês de IA e boards de arquitetura** que precisam de critérios consistentes em vez de
julgamento caso a caso.
**Líderes técnicos** que receberam a instrução "coloque guardrails" e precisam saber o que
isso significa concretamente.

## Como usar

Copie o que serve, apague o que não se aplica. Os documentos são propositalmente opinativos —
adaptar exige discordar explicitamente, e um template que serve para qualquer organização não
orienta nenhuma.

O que vale manter intacto é o **tiering de risco** em
[model-certification.md](./governance/model-certification.md). A maior parte dos outros
documentos se apoia nele, e um sistema de níveis que todos reconhecem vale mais do que um
sistema perfeito que ninguém usa.

## Roadmap

Veja [ROADMAP.md](./ROADMAP.md). A Fase 1 estabelece os artefatos centrais; as fases
seguintes trazem exemplos preenchidos, um playbook de avaliação e um modelo de custo e
operação.

## Relacionados

O kit especifica quais evidências uma revisão exige. Estes repositórios são exemplos de como
produzi-las:

- [ai-guardrails-toolkit](https://github.com/prodrigues2023/ai-guardrails-toolkit) — a engenharia que implementa os controles que o [baseline de guardrails](./governance/guardrails-baseline.md) exige
- [enterprise-ai-framework](https://github.com/prodrigues2023/enterprise-ai-framework) — o framework que dá ao [baseline de guardrails](./governance/guardrails-baseline.md) um único lugar para ser aplicado entre aplicações
- [rag-reference-architecture](https://github.com/prodrigues2023/rag-reference-architecture) — uma arquitetura de referência documentada do jeito que o [template de design](./templates/solution-design-document.md) pede
- [rag-evaluation-toolkit](https://github.com/prodrigues2023/rag-evaluation-toolkit) — a evidência de avaliação que a [certificação de modelos](./governance/model-certification.md) exige a partir do Tier 2
- [mcp-servers-collection](https://github.com/prodrigues2023/mcp-servers-collection) — design das superfícies de tools contra as quais o [excesso de autonomia](./templates/threat-model-ai.md) é avaliado
- [event-driven-dotnet-reference](https://github.com/prodrigues2023/event-driven-dotnet-reference) — mensageria confiável entre serviços: outbox, consumidores idempotentes, sagas

## Contribuindo

Discordância é a contribuição mais útil. Se um item de checklist não sobreviver ao contato
com a sua organização, abra uma issue explicando por quê — é esse retorno que separa um
documento real de um documento aspiracional.

## Autor

Paulo Roberto Franco Rodrigues — AI Solutions Architect.
Vinte anos em sistemas distribuídos e arquitetura de soluções; recentemente projetando
plataformas de IA cloud-native em AWS e Azure, e atuando em comitê corporativo de arquitetura
de IA na definição de guardrails, certificação de modelos e governança de frameworks.
[LinkedIn](https://linkedin.com/in/paulo-roberto-franco-rodrigues)

## Licença

[CC BY 4.0](./LICENSE) — uso comercial permitido, adaptação permitida, basta manter a atribuição.
