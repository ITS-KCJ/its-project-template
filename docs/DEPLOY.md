# Deploy — {{PROJETO}}

Política **HML-first**: nada vai para produção sem passar por homologação. Produção é bloqueada por padrão.

## Ambientes

| Ambiente | Host | Acesso |
|----------|------|--------|
| Homologação | {{VM_HML}} | equipe |
| Produção | {{VM_PROD}} | somente o owner |

## Fluxo de promoção

```
branch + PR → CI verde → merge na main
   → deploy em homologação ({{VM_HML}}) → validação
   → gate da fase PASS
   → GO explícito do owner
   → deploy em produção ({{VM_PROD}})
```

## Deploy em homologação

<!-- Comando/procedimento de deploy na .96 -->

```bash
# ex: git push hml main   (ou docker compose na VM de homologação)
```

## Deploy em produção (somente owner)

As três condições obrigatórias antes de tocar produção:

1. Fase 100% completa
2. Gate validado em homologação ({{VM_HML}})
3. GO explícito do owner

```bash
{{DEPLOY_CMD}}
```

## Rollback

<!-- Como reverter: voltar ao último commit estável e rebuildar. -->

```bash
# ex: git checkout <hash-bom> && {{DEPLOY_CMD}}
```

Confirme o health check antes de considerar resolvido. Ver `docs/runbooks/incidente.md`.
