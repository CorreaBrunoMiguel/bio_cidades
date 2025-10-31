# BioCidades — Modelo Conceitual (MVP)

## 📖 Resumo

Núcleo de entidades para taxonomia, observações e regiões, com privacidade
aplicada a dados sensíveis.

## Entidades

- **User**(id, role=CITIZEN, display_name)
- **Taxon**(id, rank, scientific_name, common_name?, parent_id, slug)
- **TaxonSynonym**(id, taxon_id, name, source)
- **SpeciesMeta**(taxon_id=SPECIES, eco_status, notes)
- **Region**(id, name, city, biome, bounds_bbox?)
- **Occurrence**(id, user_id, taxon_id, observed_at, lat, lon, notes,
  privacy_level)
- **Media**(id, occurrence_id, kind=IMAGE|VIDEO, s3_key, mime,
  exif_json_private)

## Relações

User 1—N Occurrence • Taxon parent_id↔children • Taxon 1—N TaxonSynonym •
SpeciesMeta 1—1 Taxon(SPECIES) • Region 1—N Occurrence • Occurrence 1—N Media

---
