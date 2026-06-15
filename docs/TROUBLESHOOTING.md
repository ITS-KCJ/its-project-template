# Troubleshooting — {{PROJETO}}

Problemas comuns e como resolver. Mantenha esta lista crescendo conforme a equipe encontra coisas.

## Ambiente local

| Sintoma | Causa provável | Solução |
|---------|----------------|---------|
| Serviço não sobe | `.env` incompleto | conferir contra `.env.example` |
| Erro de conexão com banco | container do banco não subiu | checar `docker compose ps` e logs |
| Porta em uso | outra instância rodando | parar o processo ou trocar a porta |

## Runtime

| Sintoma | Causa provável | Solução |
|---------|----------------|---------|
| 401 / sessão expira | token / config de auth | conferir variáveis de JWT/sessão |
| 500 em endpoint | erro no backend | ler logs do serviço |

## Onde olhar logs

```bash
# local
{{RUN_LOCAL}}   # e então: docker compose logs --tail=100 <serviço>
```

Incidente em produção é assunto da runbook: `docs/runbooks/incidente.md`.
