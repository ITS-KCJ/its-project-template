# Architecture Decision Records (ADRs)

Decisões de arquitetura registradas, em ordem. Um ADR captura uma decisão relevante, o contexto que levou a ela e as consequências assumidas. Decisão registrada não se apaga: quando muda, cria-se um novo ADR que substitui o anterior (o antigo vira `Status: Substituído por ADR-XXX`).

## Quando escrever um ADR

- Escolha de tecnologia ou padrão estrutural
- Mudança que afeta fronteiras de módulo, banco, autenticação ou permissões
- Qualquer decisão que um futuro mantenedor vá questionar "por que foi feito assim?"

## Como criar

1. Copie `_TEMPLATE.md` para `NNN-titulo-curto.md` (NNN = próximo número).
2. Preencha as seções. Comece em `Status: Proposto`.
3. Ao aceitar, mude para `Status: Aceito`.

## Convenção

- Numeração sequencial com três dígitos: `001`, `002`, ...
- Nome do arquivo em `kebab-case`: `003-cache-de-permissoes.md`
- Português no texto, inglês no código e identificadores.

## Índice

| ADR | Título | Status |
|-----|--------|--------|
| _ainda nenhum_ | | |

> Mantenha este índice atualizado ao adicionar um ADR.
