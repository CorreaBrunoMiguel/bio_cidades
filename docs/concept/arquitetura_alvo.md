# BioCidades — Arquitetura Alvo (PERN)

## 📖 Resumo

Monorepo com Next.js (web), NestJS (API), Prisma (ORM), PostgreSQL e S3/MinIO
para mídia; schemas compartilhados (Zod). Evolução futura: PostGIS.

## Componentes

- **Web (Next.js)** — app pública/privada; Zod para validações/contratos
  compartilhados.
- **API (NestJS)** — serviços REST; headers Orion; erros RFC7807.
- **ORM (Prisma)** — modelos, enums PostgreSQL e migrações.
- **DB (PostgreSQL)** — lat/lon no MVP; PostGIS (POINT 4326 + GIST) depois.
- **Storage (S3/MinIO)** — upload assinado; TTL curto; least privilege.

## Padrões

Endpoints `/status|/healthz|/readyz` • Headers: `X-Correlation-Id`,
`X-API-Version`, `X-Idempotency-Key` (POST) • Erros `application/problem+json`
(RFC7807).

## Evolução

Ativar PostGIS para raio/heatmap; observabilidade (OTel) em etapa posterior.

---
