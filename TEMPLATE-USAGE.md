# Como usar este template

Este repositório é um **modelo** de projeto ITS. Ele padroniza documentação e governança de GitHub para que qualquer pessoa da equipe consiga desenvolver e dar suporte sem depender de conhecimento na cabeça de alguém.

## Para um projeto novo (recomendado)

No GitHub, com este repositório marcado como **Template repository**:

1. Clique em **Use this template** → **Create a new repository**.
2. Nomeie o repositório do projeto novo.
3. Clone e faça o "preenchimento" (próxima seção).

## Para um projeto que já existe

Copie as pastas `docs/` e `.github/` e os arquivos `CLAUDE.md`, `CONTRIBUTING.md`, `README.md` para o projeto, sem sobrescrever o que já estiver bom. Depois faça o preenchimento.

## Preenchimento: substitua os placeholders

Procure e troque em todos os arquivos:

| Placeholder | O que é | Exemplo |
|-------------|---------|---------|
| `{{PROJETO}}` | Nome do projeto | LUMEN Voice |
| `{{DESCRICAO}}` | Uma linha sobre o que faz | PABX multi-cliente |
| `{{REPO}}` | owner/repo no GitHub | buenojulio/lumen-voice |
| `{{DOMINIO}}` | URL de produção | voice.itscs.net |
| `{{STACK}}` | Stack resumida | FastAPI + Next.js + PostgreSQL |
| `{{VM_PROD}}` | Host de produção | 10.70.1.92 |
| `{{VM_HML}}` | Host de homologação | 10.70.1.96 |
| `{{DEPLOY_CMD}}` | Comando de deploy | docker compose up -d --build |
| `{{OWNER_GH}}` | Handle do owner no GitHub | @buenojulio |
| `{{RUN_LOCAL}}` | Como subir local | docker compose up -d |

Busca rápida pelos placeholders que faltam preencher:

```bash
grep -rn "{{" . --include="*.md" --include="CODEOWNERS" --include="*.yml"
```

## Depois de preencher

1. Apague este arquivo (`TEMPLATE-USAGE.md`) e o bloco de aviso no topo do `README.md`.
2. Ajuste `docs/ARCHITECTURE.md` com a realidade do projeto.
3. Revise `CODEOWNERS` com os responsáveis por área.
4. Habilite o CI: veja `.github/workflows/README.md`.
5. Commit inicial em branch, nunca direto na `main`.

## O que é convenção ITS (não mexer sem motivo)

Estes pontos valem para todos os projetos e já vêm prontos:

- **Deploy HML-first**: homologação (`{{VM_HML}}`) antes de produção; produção bloqueada por padrão.
- **Idioma**: português para doc/comentário/commit; inglês para código.
- **Segurança**: nunca commitar segredos; backend valida tudo.
- **Fluxo GSD** por nível de risco (1/2/3).
- **Sem travessão** nos textos.
