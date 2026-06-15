<!--
==================================================================
ESTE É UM PROJETO CRIADO A PARTIR DO TEMPLATE ITS.
Antes de entregar: preencha os placeholders {{...}}, leia TEMPLATE-USAGE.md
e apague este bloco de aviso.
==================================================================
-->

# {{PROJETO}}

{{DESCRICAO}}

Em produção em **{{DOMINIO}}**. Stack: {{STACK}}.

## Rodar local

```bash
git clone https://github.com/{{REPO}}.git
cd {{PROJETO}}
cp .env.example .env        # pedir os valores reais por canal seguro, nunca por chat
{{RUN_LOCAL}}
```

Detalhes e acessos: `docs/ONBOARDING.md`.

## Documentação

| Documento | Para quê |
|-----------|----------|
| `docs/ONBOARDING.md` | Do zero ao primeiro PR |
| `docs/ARCHITECTURE.md` | Visão técnica e decisões |
| `docs/DEPLOY.md` | Como subir (HML antes de produção) |
| `docs/TROUBLESHOOTING.md` | Problemas comuns |
| `docs/runbooks/` | Operação: incidente, backup, rotina |
| `docs/ADRs/` | Decisões de arquitetura |
| `CONTRIBUTING.md` | Como contribuir |
| `CLAUDE.md` | Regras do projeto para a IA (Claude Code) |

## Ambientes

| Ambiente | Host | Quem acessa |
|----------|------|-------------|
| Homologação | {{VM_HML}} | equipe, para validar antes do PR |
| Produção | {{VM_PROD}} | deploy exclusivo do owner |
