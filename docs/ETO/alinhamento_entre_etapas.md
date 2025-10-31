# BioCidades — alinhamento_entre_etapas

## 📖 Resumo

Dependências, marcos e artefatos que conectam decisões entre etapas para evitar
retrabalho e manter consistência.

## Dependências chave

- **Taxonomia (Etapa 0)** ↔ Autocomplete e catálogo (Etapa 2).
- **Ética & Privacidade (Etapa 0)** ↔ Ofuscação no mapa e políticas de exposição
  (Etapa 3).
- **Arquitetura alvo (Etapa 0)** ↔ CI/Monorepo e serviços base (Etapa 2 ·
  T1/T2).

## Artefatos de entrada/saída

- **Entrada Etapa 2**: docs congelados (0 e 1), `etapas_overview.md` como
  referência, critérios de aceite MVP.
- **Saída Etapa 2**: API básica rodando, checklist de qualidade atendido.
- **Entrada Etapa 3**: API pronta, política de ofuscação definida; dados mínimos
  para clusters.
- **Saída Etapa 3**: mapa/filtros operacionais com ofuscação; prontos para OTel.

## Riscos transversais & mitigação

- Fontes/dados variáveis → versionamento de catálogos e ADR quando necessário.
- Crescimento de mídia → política de retenção/compressão.
- Escopo de filtros → critérios de aceite objetivos e testes de coerência.

---
