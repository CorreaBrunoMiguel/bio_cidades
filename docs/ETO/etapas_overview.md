# BioCidades — etapas_overview (Orion v3.7)

## 📖 Resumo

Visão macro do caminho até o deploy. Define etapas, marcos e critérios de
passagem. Documento universal, domínio‑agnóstico, instanciado para esta
aplicação.

## Etapas

- **Etapa 0 — Conceito & Codex**: visão, modelo, arquitetura, ética. **Status:**
  concluída.
- **Etapa 1 — Alinhamento**: cola entre etapas, rastreabilidade do todo.
  **Status:** corrente.
- **Etapa 1.5 — Oficialização**: commit dos docs, `develop` default, configs
  mínimas.
- **Etapa 2 — MVP Fundacional**: Fase 1 · Sprint 1 → **T1: Monorepo &
  Qualidade**; **T2: API Bootstrap**.
- **Etapa 3 — Mapa & Filtros**: clusters, filtros por
  região/bioma/período/eco_status, ofuscação pública aplicada.
- **Etapa 4 — Observabilidade & Release**: OTel, hardening, release.

## Critérios de Passagem

- **0 → 1**: 4 CORE de Etapa 0 aprovados.
- **1 → 1.5**: 3 CORE de Etapa 1 aprovados.
- **1.5 → 2**: repositório vivo (docs em `main`, `develop` default, configs
  mínimas).
- **2 → 3**: API básica pronta (`/status|/healthz|/readyz`), CI mínimo e
  qualidade baseline.
- **3 → 4**: mapa e filtros funcionais com política de ofuscação; prontidão para
  observabilidade e hardening.

---
