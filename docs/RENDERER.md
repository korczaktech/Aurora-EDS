# Renderizador nativo

## Objetivo
Renderizar a cena do UI Engine em superfícies Android, sem navegador embarcado. Backend gráfico é detalhe de implementação e não deve vazar para componentes.

## Backends
A arquitetura oferece interface de backend. Android Canvas será o caminho inicial de compatibilidade; Vulkan será habilitado quando capacidade do dispositivo, drivers e custo justificarem. Não se promete Vulkan em todos os aparelhos. Fallback deve ser automático e testado.

## Modelo de cena
A cena contém primitivas de texto, imagem, forma, borda, gradiente, clipping, transformação e camada. Cada comando possui limites, ordem, estado de composição e referência a recursos. Agrupar comandos compatíveis reduz mudanças de estado da GPU.

## Recursos gráficos
Texturas, fontes, buffers e superfícies possuem proprietário, duração e política de descarte. Perda de contexto ou recriação da superfície deve permitir reconstrução. Recursos não usados são liberados sob pressão de memória.

## Sincronização
Produção de cena e apresentação respeitam o ciclo de frames da plataforma. Não bloquear thread de UI esperando GPU. Buffers em uso não podem ser reutilizados antes da conclusão da submissão.

## Texto
Considerar shaping, fontes, fallback, direção, seleção, cursor, composição IME e escala de acessibilidade. Métricas de layout e desenho devem ser consistentes.

## Animações
Animações atualizam propriedades visuais no pipeline de frame sem chamadas FFI por frame. Propriedades simples podem ser compostas no backend. Respeitar redução de movimento.

## Validação
Medir tempo CPU/GPU, jank, memória gráfica, energia e comportamento em diferentes densidades e drivers. Comparações usam cenas equivalentes e aparelhos identificados.
