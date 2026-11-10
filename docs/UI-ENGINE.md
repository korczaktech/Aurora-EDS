# UI Engine

## Escopo
O UI Engine transforma descrições de interface em árvore visual nativa. Não é navegador, não implementa DOM e não utiliza WebView ou Chromium.

## Modelo de componentes
Cada nó possui ID estável, tipo registrado, propriedades validadas, estado visual, filhos ordenados, eventos e metadados de acessibilidade. Tipos desconhecidos geram diagnóstico controlado.

Propriedades são aplicadas como transações e publicadas no próximo ciclo seguro de renderização.

## Pipeline
1. Receber alterações visuais.
2. Validar propriedades e referências.
3. Calcular diff da árvore.
4. Marcar nós e regiões afetadas.
5. Executar layout incremental.
6. Gerar comandos de desenho.
7. Submeter ao backend.
8. Compor e apresentar a superfície.

## Layout
Suportar eixo horizontal/vertical, constraints, tamanho intrínseco, limites mínimo/máximo, alinhamento, espaçamento, posicionamento absoluto controlado, scroll e medição de texto. Resolução de conflitos deve ser determinística.

## Eventos
Toque, teclado, foco, ponteiro e acessibilidade são normalizados. Roteamento considera hit testing, captura, propagação e cancelamento. Eventos não são entregues a nós destruídos.

## Lifecycle
Nós possuem criação, montagem, atualização, suspensão e destruição. Remoção libera listeners, animações, handles e recursos associados.

## Acessibilidade
A árvore visual produz representação semântica acessível à plataforma. Texto, papel, estado, ações, foco e ordem de navegação devem ser declarados; acessibilidade não depende apenas de pixels.

## Aceite
Testes de diff, layout, hit testing, lifecycle, foco, acessibilidade e consistência sob atualizações rápidas. Evitar reconstrução total, alocações por frame e layout repetido.
