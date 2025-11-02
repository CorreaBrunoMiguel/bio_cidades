# Fase 1 — Fundações & Qualidade

## 📖 Resumo

A Fase 1 estabelece o trilho de execução do MVP: monorepo operante, qualidade
mínima (lint/format/hooks/CI), API viva com contratos base e camada de dados
inicial. Com isso, as próximas fases podem crescer com segurança e
rastreabilidade.

## 🧭 Introdução

**Sprints desta Fase:**

- **Sprint 1 — Monorepo & Qualidade**: root `package.json`
  (orquestração/workspaces), pnpm/Turborepo, ESLint integrado ao `.prettierrc`
  do projeto (sem sobrescrever), Husky/lint-staged, CI mínimo.
- **Sprint 2 — API Bootstrap**: NestJS com `/status|/healthz|/readyz`, headers
  Orion obrigatórios, erros RFC7807 (Problem+JSON).
- **Sprint 3 — Data Layer**: Prisma + PostgreSQL; modelos núcleo (Taxon,
  SpeciesMeta, Region, Occurrence, Media, User) e migrações/seed mínimos.

**Como será detalhado:**

- Cada Sprint inicia com a **lista de Tarefas/Subtarefas (Registro Orion —
  Pt.1)** adicionada a este arquivo.
- Cada Tarefa/Subtarefa será registrada com subtítulos terminando em `:`: `ID:`,
  `Branch base:`, `Branch de trabalho:`, `Objetivo (one-liner):`, `Escopo:`,
  `Critérios de Aceite (verificáveis):`, `Artefatos/Interfaces:`,
  `Diretórios/Arquivos (root):`, `Comandos de verificação:`, `Commit sugerido:`,
  `Riscos & rollback:`, `Documentos relacionados:`.
- Em seguida, a **Implementação Operacional (Pt.2)** é executada e anexada,
  mantendo o histórico orgânico desta Fase.

> Próxima interação nesta aba: **Sprint 1 — Lista de Tarefas/Subtarefas
> (Registro Orion — Pt.1)**.

## Sprint 1 — Monorepo & Qualidade (Registro Orion · Pt.1)

### Tarefa 1 — Monorepo & Workspace Baseline

**Resumo:** Preparar o esqueleto do monorepo com pnpm, Turborepo e workspaces,
sem tocar no `.prettierrc` do projeto.

**ID:** E2-F1-S1-T1 **Branch base:** develop **Branch de trabalho:**
feature/e2-f1-s1-t1-monorepo-workspace **Objetivo (one-liner):** Criar o
workspace raiz (pnpm + turbo) e a estrutura inicial de apps/pacotes. **Escopo:**
package.json (root, workspaces/scripts/engines), pnpm-workspace.yaml,
turbo.json, tsconfig.base.json, diretórios `apps/web`, `apps/api`,
`packages/config` (placeholders). **Critérios de Aceite (verificáveis):**

- `corepack enable` + `pnpm -v` + `turbo --version` funcionam.
- `pnpm install` executa sem erros no workspace.
- Arquivos `package.json`, `pnpm-workspace.yaml`, `turbo.json`,
  `tsconfig.base.json` existem e são válidos.
- Estrutura de diretórios criada conforme planejado. **Artefatos/Interfaces:**
  package.json, pnpm-workspace.yaml, turbo.json, tsconfig.base.json.
  **Diretórios/Arquivos (root):** ver Escopo. **Comandos de verificação:**
  `corepack enable && corepack prepare pnpm@latest --activate`; `pnpm -v`;
  `turbo --version`; `pnpm install`. **Commit sugerido:** 🔧 build: baseline
  monorepo (pnpm+turbo, workspaces, tsconfig.base) **Riscos & rollback:** versão
  do Node incompatível → usar LTS ≥ 20; se falhar, remover arquivos e reverter
  commit. **Documentos relacionados:** overview_etapa2.md; este `eto_fase1.md`;
  rastreabilidade.md.

### Tarefa 2 — ESLint integrado ao Prettier do projeto

**Resumo:** Configurar ESLint no root, integrando ao `.prettierrc` existente
(sem sobrescrever).

**ID:** E2-F1-S1-T2 **Branch base:** develop **Branch de trabalho:**
feature/e2-f1-s1-t2-eslint-prettier **Objetivo (one-liner):** Habilitar lint
unificado para o monorepo, respeitando o Prettier do usuário. **Escopo:**
`.eslintrc.cjs` no root (extends recomendados + `plugin:prettier/recommended`),
`.eslintignore` (se necessário), scripts `lint` e `format` no package.json.
**Critérios de Aceite (verificáveis):**

- `pnpm -w run lint` executa sem erros num repo limpo.
- Código inválido faz o lint falhar (prova negativa). **Artefatos/Interfaces:**
  `.eslintrc.cjs`, `.eslintignore`, scripts no package.json.
  **Diretórios/Arquivos (root):** ver Escopo. **Comandos de verificação:**
  `pnpm -w run lint`; inserir arquivo de teste inválido e confirmar falha;
  remover/ajustar e confirmar sucesso. **Commit sugerido:** 🔧 build: ESLint
  base integrado ao Prettier (sem alterar .prettierrc) **Riscos & rollback:**
  conflitos de regras → desabilitar regras conflitantes via
  `eslint-config-prettier`; rollback removendo config e dependências.
  **Documentos relacionados:** etica_privacidade.md (padrões),
  rastreabilidade.md.

### Tarefa 3 — Husky + lint-staged e CI mínimo

**Resumo:** Proteger a árvore com pre-commit e garantir pipeline mínimo no
GitHub Actions.

**ID:** E2-F1-S1-T3 **Branch base:** develop **Branch de trabalho:**
feature/e2-f1-s1-t3-husky-ci **Objetivo (one-liner):** Impedir commits quebrados
e validar lint/build no CI. **Escopo:** Husky (`pre-commit` executando
`lint-staged`), `lint-staged.config.cjs` (format + lint em arquivos staged),
workflow `.github/workflows/ci.yml` (Node LTS 20 + pnpm + turbo cache +
install + lint + build). **Critérios de Aceite (verificáveis):**

- Commit com arquivo JS/TS inválido é barrado pelo hook.
- Workflow `ci.yml` finaliza com **success** em install/lint/build.
  **Artefatos/Interfaces:** `.husky/pre-commit`, `lint-staged.config.cjs`,
  `.github/workflows/ci.yml`. **Diretórios/Arquivos (root):** ver Escopo.
  **Comandos de verificação:** criar arquivo simples inválido, `git add` e
  `git commit -m "🧪 test: hook"` (deve falhar); ajustar e tentar novamente
  (deve passar). **Commit sugerido:** 🧪 test/🔧 build: hooks Husky +
  lint-staged e CI mínimo (install/lint/build) **Riscos & rollback:** hook
  excessivamente rígido → ajustar globs do lint-staged; pipeline lento →
  adicionar cache; rollback removendo `.husky/` e workflow. **Documentos
  relacionados:** rastreabilidade.md; overview_etapa2.md; este `eto_fase1.md`.

## Sprint 2 — API Bootstrap (Registro Orion · Pt.1)

### Tarefa 1 — API Scaffolding & Workspace Wiring

**Resumo:** Criar o app **NestJS** em `apps/api` e integrá-lo ao monorepo
(pnpm/Turbo), preparando scripts e configuração base.

**ID:** E2-F1-S2-T1 **Branch base:** develop **Branch de trabalho:**
feature/e2-f1-s2-t1-api-bootstrap **Objetivo (one-liner):** Subir a API NestJS
(apps/api) integrada ao workspace e pronta para evolução. **Escopo:** gerar app
NestJS; `package.json` do pacote (`name: "@bc/api"`), scripts
(`dev/build/lint/test`), `tsconfig` local (herdando do `tsconfig.base.json`),
`main.ts` com CORS e `globalPrefix 'api/v1'`, `.env.example`. **Critérios de
Aceite (verificáveis):**

- `pnpm --filter @bc/api dev` inicia servidor (porta 3000 por padrão,
  configurável por `PORT`).
- Prefixo global `api/v1` ativo.
- Scripts do pacote executam via Turbo (`pnpm -w run dev`).
  **Artefatos/Interfaces:** `apps/api/package.json`, `apps/api/src/main.ts`,
  `apps/api/src/app.module.ts`, `apps/api/tsconfig.json`, `.env.example`.
  **Diretórios/Arquivos (root):** `apps/api/**`. **Comandos de verificação:**
  `pnpm --filter @bc/api dev`; `curl -i http://localhost:3000/` (404 esperado
  até endpoints); `curl -i http://localhost:3000/api/v1` (404 com prefixo).
  **Commit sugerido:** 🔧 build: bootstrap NestJS em apps/api (workspace &
  scripts) **Riscos & rollback:** conflito de porta → ajustar `.env`; rollback
  removendo `apps/api` e lockfile relacionado. **Documentos relacionados:**
  overview_etapa2.md; rastreabilidade.md; este `eto_fase1.md`.

### Tarefa 2 — Headers Orion & Problem+JSON

**Resumo:** Implementar **headers obrigatórios** e **filtro de exceções** para
**RFC7807** (`application/problem+json`).

**ID:** E2-F1-S2-T2 **Branch base:** develop **Branch de trabalho:**
feature/e2-f1-s2-t2-headers-problemjson **Objetivo (one-liner):** Garantir
`X-Correlation-Id` e `X-API-Version` em todas as respostas; aceitar
`X-Idempotency-Key` em POST; padronizar erros em Problem+JSON. **Escopo:**
middleware para `X-Correlation-Id` (gera se ausente), interceptor
`X-API-Version` (ler de `package.json`/const), aceitação/eco de
`X-Idempotency-Key` em POST, **ExceptionFilter** global retornando Problem+JSON
com `type`, `title`, `status`, `detail`, `instance`, `correlation_id`.
**Critérios de Aceite (verificáveis):**

- Qualquer erro (`HttpException`) retorna `application/problem+json` com os
  campos exigidos e `correlation_id`.
- Todas as respostas possuem `X-Correlation-Id` e `X-API-Version`.
- Requisições POST com `X-Idempotency-Key` veem o header ecoado.
  **Artefatos/Interfaces:**
  `apps/api/src/common/middleware/correlation-id.middleware.ts`,
  `.../interceptors/version.interceptor.ts`,
  `.../filters/problem-json.filter.ts`, `main.ts` (registro global).
  **Diretórios/Arquivos (root):** `apps/api/src/common/**`,
  `apps/api/src/main.ts`. **Comandos de verificação:**
  `curl -i http://localhost:3000/naoexiste`;
  `curl -i -X POST http://localhost:3000/dev/echo -H 'X-Idempotency-Key: abc'`
  (rota stub para teste). **Commit sugerido:** 🛡️ security/🛠️ refactor: headers
  Orion + Problem+JSON (global) **Riscos & rollback:** incompatibilidades de
  libs → isolar configuração no `main.ts`; rollback removendo registros globais.
  **Documentos relacionados:** etica_privacidade.md; rastreabilidade.md.

### Tarefa 3 — Endpoints /status | /healthz | /readyz

**Resumo:** Implementar endpoints padrão com payload mínimo e integração aos
headers Orion.

**ID:** E2-F1-S2-T3 **Branch base:** develop **Branch de trabalho:**
feature/e2-f1-s2-t3-status-health-ready **Objetivo (one-liner):** Expor
`GET /api/v1/status`, `GET /healthz`, `GET /readyz` com checks simples.
**Escopo:** controller de status (`/api/v1/status` com `version`, `timestamp`,
`uptime`); `healthz` (process up); `readyz` (checks mínimos — ex.: acesso a env;
DB opcional stub). **Critérios de Aceite (verificáveis):**

- `curl -i /api/v1/status` retorna 200 com `version/timestamp/uptime` e headers
  Orion.
- `curl -i /healthz` e `/readyz` retornam 200 (`readyz` pode iniciar com
  `checks: []`).
- Em erro forçado, resposta é Problem+JSON com `correlation_id`.
  **Artefatos/Interfaces:** `apps/api/src/status/status.controller.ts`,
  `status.service.ts`, `readyz.controller.ts`, `healthz.controller.ts` (ou
  módulo único). **Diretórios/Arquivos (root):** `apps/api/src/status/**`,
  `apps/api/src/app.module.ts`. **Comandos de verificação:**
  `curl -i http://localhost:3000/api/v1/status`;
  `curl -i http://localhost:3000/healthz`;
  `curl -i http://localhost:3000/readyz`. **Commit sugerido:** ✨ feat:
  endpoints /status /healthz /readyz com headers Orion **Riscos & rollback:**
  colisão de prefixos de rota → definir `globalPrefix = 'api/v1'` no `main.ts`;
  rollback via revert do módulo de status. **Documentos relacionados:**
  arquitetura_alvo.md; rastreabilidade.md; este `eto_fase1.md`.
