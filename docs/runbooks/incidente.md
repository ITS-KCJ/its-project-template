# Runbook — Incidente em produção

Para quando {{DOMINIO}} está fora, lento ou com erro afetando usuários.

## 0. Antes de tudo

- Produção é a VM `{{VM_PROD}}`. Acesso e deploy são exclusivos do owner.
- Se você não é o owner: registre sintomas, hora de início e impacto, e acione o owner. Não corrija produção por conta própria.

## 1. Detecção

Sinais comuns: usuários relatam erro, alerta automático, health check falhando.

Registre desde já: o que parou, desde quando, quantos/quais usuários, qual parte do sistema.

## 2. Triagem rápida (5 minutos)

```bash
ssh <user>@{{VM_PROD}}
cd <caminho-do-projeto>
docker compose ps                 # algum serviço down/restarting?
docker compose logs --tail=100 <serviço>
```

Checar a borda: tunnel/reverse-proxy ativo? Serviço respondendo no host?

## 3. Contenção

| Sintoma | Primeira ação |
|---------|---------------|
| Container caído | `docker compose up -d <serviço>` |
| Serviço em loop de restart | ler logs, checar `.env` e dependências |
| Erro após deploy recente | rollback (seção 4) |
| Banco inacessível | checar container e volume; não recriar volume |
| Lentidão geral | checar CPU/memória da VM e filas |

Objetivo: restaurar serviço, não achar a causa raiz ainda.

## 4. Rollback de deploy

Se o incidente começou logo após um deploy:

```bash
ssh <user>@{{VM_PROD}}
cd <caminho-do-projeto>
git log --oneline -5
git checkout <hash-bom>
{{DEPLOY_CMD}}
```

Confirme o health check antes de considerar resolvido.

## 5. Comunicação

Avise os afetados ao ter previsão ou normalização. Mantenha registro: início, ações, normalização.

## 6. Pós-incidente

- Resumo: causa, impacto, o que resolveu, como evitar.
- Decisão de arquitetura vira ADR em `docs/ADRs/`.
- Falta de cobertura vira issue de melhoria.
