# CI / Workflows

Esta pasta guarda os workflows do GitHub Actions. O template **não** traz um CI pronto, porque ele depende da stack do projeto.

## Como habilitar

Crie um arquivo `ci.yml` aqui com os passos da sua stack. Esqueleto:

```yaml
name: CI
on:
  pull_request:
    branches: [main]
  push:
    branches: [main]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      # Backend (exemplo Python)
      # - uses: actions/setup-python@v5
      #   with: { python-version: "3.12" }
      # - run: pip install -r backend/requirements.txt
      # - run: cd backend && pytest
      # Frontend (exemplo Node)
      # - uses: actions/setup-node@v4
      #   with: { node-version: "22" }
      # - run: cd frontend && npm ci && npm run lint && npx vitest run && npm run build
```

Regra do projeto: **PR com CI vermelho não é revisado** (ver `CONTRIBUTING.md`).
