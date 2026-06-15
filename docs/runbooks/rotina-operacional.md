# Runbook — Rotina operacional

Tarefas recorrentes para manter {{PROJETO}} saudável.

## Diário

- Conferir health check de {{DOMINIO}}.
- Conferir se os alertas/jobs agendados rodaram.

## Semanal

- Procurar erros recorrentes nos logs:
  ```bash
  ssh <user>@{{VM_PROD}}
  cd <caminho-do-projeto>
  docker compose logs --since 168h <serviço> | grep -i error
  ```
- Confirmar que o backup rodou e está guardado fora da VM.
- Checar espaço em disco e crescimento dos volumes.

## Mensal

- Testar restore do banco em homologação `{{VM_HML}}`.
- Revisar dependências com atualização de segurança pendente.

## Jobs agendados

<!-- Liste os jobs do projeto: nome, quando roda, o que faz, como verificar se parou. -->

| Job | Quando | O que faz |
|-----|--------|-----------|
| | | |

## Deploy (resumo)

Deploy de produção segue HML-first e é exclusivo do owner. Procedimento completo em `docs/DEPLOY.md`.
