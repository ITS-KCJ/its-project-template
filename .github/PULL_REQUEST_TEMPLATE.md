<!--
Preencha o resumo e marque o checklist. PR com CI vermelho não é revisado.
Deploy em produção é exclusivo do owner e segue a política HML-first (ver docs/DEPLOY.md).
-->

## Resumo

<!-- O que muda e por quê, em 2-4 linhas. -->

## Tipo

- [ ] Correção (fix)
- [ ] Funcionalidade (feat)
- [ ] Documentação
- [ ] Refatoração / manutenção
- [ ] Migração de banco — atenção redobrada

## Riscos e impacto

<!-- O que pode quebrar. Partes afetadas. Impacto em dados, permissões ou operação. -->

## Como foi testado

<!-- Comandos rodados e resultado. Se não rodou algo, justifique. -->

## Checklist do PR

- [ ] Mudança pequena e focada
- [ ] Branch própria, nunca `main`
- [ ] Sem credenciais reais no diff
- [ ] Validações (testes / lint / build) executadas ou justificativa registrada
- [ ] Documentação atualizada quando muda comportamento, variáveis ou operação
- [ ] Validado em homologação ({{VM_HML}}) quando há impacto de runtime

## Se este PR mexe no banco

- [ ] É fase GSD nível 3 (não foi "ajuste rápido")
- [ ] Impacto, rollback e validação em banco limpo documentados
- [ ] Nenhuma outra migração em paralelo

---

> Gate de produção (preenchido pelo owner, não pelo autor): fase 100% completa · gate validado em {{VM_HML}} · GO explícito. Sem as três condições, não vai para produção.
