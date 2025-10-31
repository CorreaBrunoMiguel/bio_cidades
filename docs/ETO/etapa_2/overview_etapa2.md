# BioCidades — Etapa 2 · Overview (Orion v3.7)

## 📖 Resumo

A Etapa 2 estabelece as fundações executáveis do MVP SOLO. Define **Fases →
Sprints** e os critérios de passagem para encerrar a etapa com qualidade mínima
operacional.

## Objetivos

- Monorepo & qualidade base (pnpm/Turborepo, ESLint, Husky/lint-staged, CI).
- API NestJS com endpoints padrão (`/status|/healthz|/readyz`), headers Orion e
  erros RFC7807.
- Camada de dados: Prisma + PostgreSQL (lat/lon); modelos núcleo.
- Fluxos iniciais do domínio: criar observação (sem mapa avançado), catálogo
  básico por árvore/lista.

## Escopo

- Backend operacional + estrutura web mínima (placeholder).
- Upload assinado S3/MinIO.
- Filtros essenciais (bioma/região/período/eco_status) e paginação/ordenação.

## Fora de Escopo (Etapa 2)

- PostGIS (raio/heatmap/cluster), observabilidade OTel, hardening e release
  (ficam para Etapas 3–4).

## Fases → Sprints

### Fase 1 — Fundações & Qualidade

- **Sprint 1**: Monorepo & Qualidade (pnpm + Turborepo + ESLint + Husky + CI)
- **Sprint 2**: API Bootstrap (NestJS + endpoints padrão + headers + RFC7807)
- **Sprint 3**: Data Layer (Prisma schema + migrações + seeds mínimos)

### Fase 2 — Domínio Básico & Fluxos

- **Sprint 1**: Upload Assinado (S3/MinIO) + serviço de mídia
- **Sprint 2**: Catálogo taxonômico mínimo (CRUD Taxon/Region + autocomplete
  stub)
- **Sprint 3**: Criar Observação (POST + validação Zod compartilhada)

### Fase 3 — Catálogo & Pesquisa (sem mapa)

- **Sprint 1**: Árvore taxonômica & lista (frontend básico)
- **Sprint 2**: Filtros por bioma/região/período/eco_status
- **Sprint 3**: Paginação, ordenação e performance baseline

## Critérios de Passagem

- CI verde (install → lint → build → test).
- API responde `/status|/healthz|/readyz` com headers Orion e RFC7807.
- Prisma migrado; seeds mínimos para Taxon/Region.
- Criar Observação persiste mídia (S3) e metadados (EXIF privado) com ofuscação
  aplicada.
- Catálogo básico funcional com filtros essenciais.

## Riscos & Mitigações

- Conflito ESLint/Prettier → integrar via `plugin:prettier`, respeitando
  `.prettierrc` do projeto.
- Autocomplete raso → stub inicial + fontes especificadas na Etapa 0.
- Volume de mídia → TTL curto de URLs assinadas e compressão.

## Documentos Relacionados

- Etapa 0/1 (congeladas) • `rastreabilidade.md` • ADR quando houver trade‑off
  relevante.
