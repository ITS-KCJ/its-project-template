# Modo de execução — GSD + PR/GitHub

Como trabalhar em {{PROJETO}} do início ao merge. Duas partes que andam juntas: o ciclo GSD (Claude Code) e a ordem de PR no GitHub, sempre sob a política HML-first.

---

## Parte 1 — Escolher o nível pelo risco

Não use o ciclo completo para tudo. Escolha primeiro:

| Nível | Quando | Como executar |
|-------|--------|---------------|
| **1. Trivial** | typo, texto, ajuste de config, 1 arquivo sem risco | `/gsd-fast` ou edição direta |
| **2. Manutenção** | bug, feature pequena, poucos arquivos | `/gsd-quick` ou `/gsd-debug` |
| **3. Estrutural** | banco, RBAC, schema, módulo novo, integração | ciclo completo (Parte 3) |

Regra fixa: migração de banco nunca é nível 1. Em dúvida entre 2 e 3, comece no 2 e escale.

Mesmo nos níveis 1 e 2, a Parte 4 (PR/GitHub) vale igual. O que muda é só quanto de planejamento GSD entra antes.

---

## Parte 2 — Preparar o projeto (uma vez)

| Situação | Comando | O que faz |
|----------|---------|-----------|
| Projeto novo (greenfield) | `/gsd-new-project` | cria roadmap, milestones e fases |
| Projeto que já existe | `/gsd-map-codebase` | mapeia o código e gera o contexto |
| Novo bloco de trabalho | `/gsd-new-milestone` | cria um milestone novo com suas fases |

Depois disso o projeto tem um roadmap em `.planning/`. O trabalho passa a ser feito **fase a fase**.

---

## Parte 3 — Ciclo de uma fase (nível 3)

A ordem é sempre esta. Cada passo só começa quando o anterior fecha.

```
/gsd-discuss-phase N   → alinhar abordagem e decisões antes de planejar
        ↓
/gsd-plan-phase N      → gera o plano executável (tarefas, dependências)
        ↓
/gsd-execute-phase N   → implementa o plano, com commits atômicos
        ↓
/gsd-verify-work       → confere que a fase entregou o que prometeu
```

Passos condicionais, quando a fase pede:

- **Fase com UI:** rode `/gsd-ui-phase` no lugar do plano comum e `/gsd-ui-review` na verificação.
- **Fase com risco de segurança:** rode `/gsd-secure-phase` antes do ship (valida as mitigações).
- **Faltou teste:** `/gsd-add-tests`.

Apoio durante o trabalho:

| Comando | Para quê |
|---------|----------|
| `/gsd-next` | o que fazer agora |
| `/gsd-progress` | onde a fase/milestone está |
| `/gsd-health` | saúde geral do projeto |
| `/gsd-resume-work` | retomar de onde parou |
| `/gsd-pause-work` | pausar registrando o estado |
| `/gsd-workstreams` | trabalho paralelo no mesmo repo (nunca duas sessões na mesma pasta) |

Quando todas as fases do milestone fecham: `/gsd-complete-milestone`.

---

## Parte 4 — Ordem de PR e GitHub (HML-first)

Esta é a ordem obrigatória, vale para qualquer nível. Produção é bloqueada por padrão.

```
1. Branch
   git checkout -b feat/nome-curto        (nunca trabalhar na main)

2. Trabalhar
   o ciclo GSD da Parte 3 roda aqui, com commits atômicos

3. Validar local
   git diff --check
   testes / lint / build da stack

4. Homologação
   deploy em {{VM_HML}} e validação real
   (quando a mudança tem impacto de runtime)

5. Pull Request
   abrir PR para main, preencher o template (.github/PULL_REQUEST_TEMPLATE.md)
   o CI roda sozinho. PR com CI vermelho NÃO é revisado.

6. Review
   /gsd-code-review            review multi-agente do diff
   /gsd-code-review --comment  posta os achados como comentários no PR
   ajustar o que aparecer

7. Merge
   o owner revisa e faz o merge na main
   (o /gsd-ship ajuda a empacotar a fase e abrir o PR)

8. Produção (somente owner, só com GO)
   três condições: fase 100% completa + gate validado em {{VM_HML}} + GO explícito
   {{DEPLOY_CMD}}
```

### Quem pode o quê

| Remote | Destino | Quem |
|--------|---------|------|
| `origin` | GitHub | todos, via branch + PR |
| `hml` | Homologação ({{VM_HML}}) | equipe |
| `vm` | **Produção** ({{VM_PROD}}) | **somente o owner** |

Ninguém além do owner pusha para `vm`. Validou em homologação, abre PR.

---

## Ponta a ponta (resumo visual)

```
preparar projeto (/gsd-new-project ou /gsd-map-codebase)
      │
      ├─ nível 1 ──→ /gsd-fast ───────────────┐
      ├─ nível 2 ──→ /gsd-quick | /gsd-debug ─┤
      └─ nível 3 ──→ discuss → plan → execute → verify ─┤
                                                         │
                          branch → local → homologação ─┘
                                  │
                          PR → CI verde → /gsd-code-review → merge
                                  │
                          (owner) gate + GO → deploy produção
```

A regra de ouro: **nada chega em produção sem passar por homologação e sem GO do owner**.
