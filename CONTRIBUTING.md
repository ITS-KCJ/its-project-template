# Como contribuir — {{PROJETO}}

Leia isto antes do primeiro commit. Vale para todo mundo, sem exceção.

## Setup local

```bash
git clone https://github.com/{{REPO}}.git
cd {{PROJETO}}
cp .env.example .env        # pedir os valores reais por canal seguro, nunca por chat
{{RUN_LOCAL}}
```

Setup detalhado e acessos necessários: `docs/ONBOARDING.md`.

## Fluxo de trabalho — branch e PR

1. **Nunca commitar direto na `main`.** Crie uma branch curta: `feat/nome-curto`, `fix/nome-curto`.
2. Mudanças pequenas e revisáveis. Termine, rode as validações, abra o PR para `main` com resumo, riscos e testes.
3. O CI roda no PR. **PR com CI vermelho não é revisado.**
4. O owner revisa e faz o merge.

## Validações locais (obrigatório antes do PR)

<!-- Ajuste para a stack do projeto. -->

```bash
git diff --check
# backend: testes
# frontend: lint + testes + build
```

Quando não der para rodar algo, registre o motivo no PR.

## Deploy e remotes — quem pode o quê

Política **HML-first**: todo trabalho é validado em homologação antes de produção. Produção fica bloqueada por padrão.

| Remote | Destino | Quem usa |
|--------|---------|----------|
| `origin` | GitHub | todos, via branch + PR |
| `hml` | Homologação ({{VM_HML}}) | equipe, para validar antes do PR |
| `vm` | **PRODUÇÃO** ({{VM_PROD}}) | **somente o owner** |

Deploy em produção (`{{DEPLOY_CMD}}`) só com as três condições: fase completa, gate validado na homologação, GO explícito do owner. Detalhes em `docs/DEPLOY.md`.

## Trabalhando com Claude Code (GSD)

Escolha o nível pelo risco:

| Nível | Quando | Comando |
|-------|--------|---------|
| 1. Trivial | typo, texto, 1 arquivo sem risco | edição direta ou `/gsd-fast` |
| 2. Manutenção | bug, feature pequena | `/gsd-quick` ou `/gsd-debug` |
| 3. Estrutural | migração de banco, RBAC, schema, módulo novo | `/gsd-discuss-phase` → plan → execute → verify |

Migração de banco nunca é nível 1. Leia `CLAUDE.md` e `.planning/STATE.md` antes de começar. Não abra duas sessões do Claude na mesma pasta; use `/gsd-workstreams` para trabalho paralelo.

## Segurança

- Nunca commitar `.env`, tokens, senhas, dumps ou chaves. Em exemplos, use placeholders (`example.com`, `change-me`).
- Backend valida tudo: permissão e schema em todo endpoint. Esconder botão no front é UX, não segurança.
- Revise o diff antes de commitar.

## Convenções

- Código (identificadores): **inglês**. Commits, comentários, docstrings e UI: **português**.
- Sem travessão nos textos.
- Siga o padrão do módulo vizinho antes de criar o seu.

## Checklist de PR

O template de PR (`.github/PULL_REQUEST_TEMPLATE.md`) já traz o checklist completo. Em resumo: mudança pequena, branch própria, sem credenciais, validações rodadas, doc atualizada, validado em homologação.
