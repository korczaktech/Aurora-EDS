# ADR-0008 — Modelo de texto do editor

- **Estado:** Aceita como direção; estrutura final depende de benchmark
- **Data:** 2026-11-10
- **Escopo:** editor

## Contexto
Arquivos grandes, edição frequente, múltiplos cursores e operações de desfazer/refazer exigem uma representação que evite reconstrução integral do documento.

## Decisão
O modelo de documento será independente da UI e baseado em operações incrementais/transacionais. A implementação avaliará Rope, Piece Table e Gap Buffer com cargas representativas antes de escolher a estrutura concreta.

Offsets e posições terão unidade explicitamente definida. A implementação deverá tratar UTF-8, Unicode, graphemes e conversões de posição sem assumir equivalência entre bytes, pontos de código e colunas visuais. Histórico será baseado em transações reversíveis.

## Alternativas consideradas
- String única reconstruída a cada edição: rejeitada para documentos gerais.
- Escolher uma estrutura sem benchmark: rejeitada.
- Usar offsets sem unidade definida: rejeitada por ambiguidade e bugs Unicode.

## Consequências
- O contrato do editor deve declarar unidade de posição.
- Benchmarks devem cobrir arquivos pequenos, grandes, edição local, edição distante, múltiplos cursores e memória.
- A UI não será dona do conteúdo canônico do documento.
