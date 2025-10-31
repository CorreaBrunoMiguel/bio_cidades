# BioCidades — SOLO · Manifesto & Visão

## 📖 Resumo

Catálogo pessoal de biodiversidade por cidade. Registro de observações (foto,
localização, data/hora, taxonomia), navegação por táxons/biomas/regiões e mapa
com clusters. SOLO agora, expansível para escolas depois.

## Problema

Registros dispersos e pouco estruturados; falta um acervo pessoal acessível e
ético para exploração local.

## Objetivo

Construir um acervo vivo e pesquisável da biodiversidade urbana/local.

## Escopo (MVP)

- Criar Observação: foto(s), lat/lon (GPS/EXIF), data/hora, notas, Táxon via
  autocomplete.
- Taxonomia canônica (Reino→Filo→Classe→Ordem→Família→Gênero→Espécie) +
  sinônimos.
- Regiões & Biomas: cadastro simples, filtros por
  bioma/região/período/eco_status.
- Catálogo & Mapa: árvore taxonômica + lista/cluster.
- Upload via URL assinada (S3/MinIO).
- Privacidade: ofuscação pública para espécies sensíveis; EXIF privado.

## Fora de Escopo (agora)

Gamificação; multiusuário amplo; PostGIS avançado; análises espaciais complexas.

## Princípios

Simplicidade auditável • Ética por padrão • Padrões Orion (headers/RFC7807) •
Evolução incremental • Portas para ensino.

## Métricas de Sucesso (exemplos)

- T90 de criação de observação ≤ 45s.
- Autocomplete com ≥ 95% de acerto no top‑5 para termos comuns.
- 100% dos erros em `application/problem+json` com `correlation_id`.

## Riscos & Mitigações (alto nível)

Ambiguidade taxonômica → sinônimos e fonte canônica. Sensibilidade de
localização → ofuscação e atraso opcional de publicação. Custos de storage →
compressão e TTL curto para URLs assinadas.

---
