# Runbook — Backup e restore

Produção é a VM `{{VM_PROD}}`.

## O que precisa de backup

| Dado | Onde vive | Criticidade |
|------|-----------|-------------|
| Banco de dados | container do banco / volume | alta |
| Arquivos / anexos | storage (ex: MinIO/S3) | alta |
| `.env` de produção | host, fora do git | alta (segredos) |

O código está no git. Não precisa de backup separado.

## Backup do banco

```bash
ssh <user>@{{VM_PROD}}
cd <caminho-do-projeto>
# ex: dump lógico
docker compose exec -T <db> pg_dump -U <user> <database> | gzip > backup_$(date +%F).sql.gz
```

Guarde fora da VM, em local seguro. Nunca em pasta servida pela web nem no repositório.

## Backup dos arquivos

Sincronize o storage de objetos para um destino seguro, preservando a estrutura.

## Restore

Operação de risco. Faça em ambiente de teste/homologação `{{VM_HML}}` primeiro.

```bash
gunzip -c backup_AAAA-MM-DD.sql.gz | docker compose exec -T <db> psql -U <user> <database>
```

Em produção, só com GO do owner e janela combinada. Confirme health check e uma amostra de dados.

## Verificação periódica

Backup que nunca foi testado não é backup. Periodicamente, restaure o último dump em `{{VM_HML}}`, suba a aplicação e confira login + uma leitura de cada parte crítica.
