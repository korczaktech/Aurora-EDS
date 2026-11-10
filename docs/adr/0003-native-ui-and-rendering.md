# ADR-0003 — Interface nativa e estratégia de renderização

- **Estado:** Aceita
- **Data:** 2026-11-10
- **Escopo:** UI Engine e Renderer

## Contexto
A EDS exige interface integrada ao Android, responsiva e com controle do pipeline visual. Uma WebView ou navegador embutido adicionaria uma pilha web que não corresponde à arquitetura desejada.

## Decisão
A interface principal será nativa e utilizará um UI Engine próprio, sem WebView, Chromium ou DOM como fundamento. O Engine manterá árvore de componentes, layout, eventos, acessibilidade e atualização incremental independentes do runtime.

O renderer terá backend abstrato. Android Canvas será o caminho inicial de compatibilidade; Vulkan poderá ser usado quando disponível e comprovadamente vantajoso. Componentes Android nativos poderão ser usados seletivamente para integração ou acessibilidade.

## Alternativas consideradas
- WebView/Chromium: rejeitados como base da interface.
- Views Android para absolutamente tudo: não adotadas como única estratégia; podem ser usadas em componentes específicos.
- Vulkan obrigatório: rejeitado por incompatibilidade de disponibilidade e custo de suporte.

## Consequências
- UI Engine e renderer são subsistemas próprios, com custo de implementação significativo.
- Layout e preparação de cena não podem bloquear a thread principal.
- Animações devem ser executadas no subsistema visual, sem chamadas FFI por frame.
- A escolha de backend exige testes em dispositivos reais.
