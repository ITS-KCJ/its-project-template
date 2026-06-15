# Onboarding — {{PROJETO}}

Guia do zero ao primeiro PR. Se você vai dar suporte ou desenvolver, comece por aqui.

## 1. O que é

{{DESCRICAO}} Em produção em {{DOMINIO}}. Stack: {{STACK}}.

Visão técnica completa: `docs/ARCHITECTURE.md`.

## 2. Acessos que você precisa pedir

Peça ao owner, por canal seguro (nunca por chat):

- Conta no GitHub com acesso ao repositório `{{REPO}}`
- Valores reais do `.env` (o repositório só traz o `.env.example`)
- Acesso à VM de homologação `{{VM_HML}}`, se for validar deploy

Você não precisa de acesso à VM de produção `{{VM_PROD}}`. Deploy em produção é exclusivo do owner.

## 3. Subir o ambiente local

```bash
git clone https://github.com/{{REPO}}.git
cd {{PROJETO}}
cp .env.example .env        # preencher com os valores recebidos
{{RUN_LOCAL}}
```

Se algum serviço não subir, veja `docs/TROUBLESHOOTING.md`.

## 4. Entender a estrutura antes de codar

<!-- Descreva a organização do código: pastas principais, onde fica o quê,
     o padrão que todo módulo segue. Aponte um módulo de referência. -->

Leia também `CLAUDE.md` (regras do projeto para a IA) e `.planning/STATE.md` (onde o projeto está).

## 5. Seu primeiro PR

1. Branch curta: `feat/nome-curto` ou `fix/nome-curto`. Nunca direto na `main`.
2. Mudança pequena e revisável.
3. Rode as validações locais (ver `CONTRIBUTING.md`).
4. Valide em homologação (`{{VM_HML}}`) quando houver impacto de runtime.
5. Abra o PR para `main`. O template já traz o checklist. CI vermelho não é revisado.
6. O owner revisa e faz o merge.

## 6. Claude Code (GSD)

Escolha o nível pelo risco: `/gsd-fast` (trivial), `/gsd-quick`/`/gsd-debug` (manutenção), ciclo completo (estrutural). Detalhes em `CONTRIBUTING.md`.

## 7. Onde pedir ajuda

- Produto ou prioridade: owner
- Erro em produção: `docs/runbooks/incidente.md`
- Ambiente local: `docs/TROUBLESHOOTING.md`
- Decisão arquitetural: `docs/ADRs/`
