# {{PROJETO}}

<!--
Este CLAUDE.md é o contexto do projeto para o Claude Code.
Preencha com a realidade do projeto. Mantenha curto e factual.
-->

## Project

**{{PROJETO}}** — {{DESCRICAO}}

Em produção em {{DOMINIO}}. Stack: {{STACK}}, em {{VM_PROD}} via Docker.

### Constraints

- **Tech stack**: {{STACK}} — não introduzir novas tecnologias sem ADR
- **Deploy**: {{DEPLOY_CMD}} → {{VM_PROD}} (HML-first: validar em {{VM_HML}} antes)
- <!-- outras restrições: schema, multi-tenant, RBAC, integrações -->

## Technology Stack

<!-- Linguagens, frameworks, libs principais, versões. -->

## Conventions

- Código (identificadores) em inglês; comentários, docstrings e commits em português.
- Sem travessão nos textos.
- Cada módulo segue o padrão do vizinho. Olhe um existente antes de criar.
- <!-- padrões de erro, logging, naming específicos do projeto -->

## Architecture

<!-- Padrão arquitetural, camadas, entry points, fluxos principais. Ver docs/ARCHITECTURE.md. -->

## GSD Workflow Policy — 3 níveis

Escolha o nível pelo risco:

| Nível | Quando | Como |
|-------|--------|------|
| 1. Trivial | typo, texto, ajuste de config, 1 arquivo sem risco | edição direta ou `/gsd-fast` |
| 2. Manutenção | bug, feature pequena, poucos arquivos | `/gsd-quick` ou `/gsd-debug` |
| 3. Estrutural | migração de banco, RBAC, schema, módulo novo | ciclo completo: discuss-phase → plan-phase → execute-phase → verify-work |

Migração de banco nunca é nível 1. Em dúvida entre 2 e 3, comece no 2 e escale.

**Deploy e acesso:** deploy em produção é exclusivo do owner e segue a política HML-first (ver CONTRIBUTING.md e docs/DEPLOY.md). Se a sessão não for do owner, nunca executar push para `vm`.

## Developer Profile

> Profile not yet configured. Run `/gsd-profile-user` to generate your developer profile.
> This section is managed by `generate-claude-profile` -- do not edit manually.
