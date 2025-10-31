# BioCidades — rastreabilidade

## 📖 Resumo

Regras de governança para garantir rastreamento entre docs, tarefas e código, do
início ao deploy.

## Branching

- `main` para releases; **`develop` default** após a 1.5.
- Features: `feature/e<etapa>-f<fase>-s<sprint>-t<tarefa>-<slug>`.
- Merges `--no-ff`; PR checklist com: testes básicos, docs atualizados quando
  aplicável, headers Orion e erros RFC7807.

## Commits (emoji)

`✨ feat`, `🐛 fix`, `🛠️ refactor`, `🧪 test`, `📝 docs`, `🔧 build`,
`🚀 release`, `🧹 chore`, `🔭 perf/otel`, `🛡️ security`.

## Tags & versões

Semânticas; changelog referenciado por Fase/Sprint/Tarefa.

## Índices e vínculos

- Vínculo bidirecional doc↔tarefa (cada `eto_faseY.md` referencia e é
  referenciado).
- `overview.md` da etapa ativa lista Fases/Sprints/Tarefas e aponta para seus
  `eto_faseY.md`.

## Qualidade mínima

- Lint e testes básicos obrigatórios.
- API sempre com headers Orion e erros `application/problem+json` (RFC7807).
