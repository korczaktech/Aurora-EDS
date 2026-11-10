# Editor de código

## Arquitetura
O modelo de documento e operações de edição ficam no núcleo nativo; a interface visual usa o UI Engine. Integração com serviços de linguagem é assíncrona e versionada por documento.

## Modelo de documento
Cada documento possui URI/identidade, versão monotônica, encoding, estado de salvamento e buffer. O modelo deve permitir inserções e remoções locais sem reconstruir todo o texto. Rope, piece table e gap buffer serão avaliados com cargas reais antes da decisão final.

Posições devem declarar unidade (byte, scalar value ou UTF-16 code unit) em cada API. Conversões entre offsets e linhas/colunas ficam centralizadas para evitar inconsistência Unicode.

## Edição transacional
Uma ação produz transação contendo operações, seleção/cursor antes e depois e metadados para undo/redo. Agrupamento de digitação é configurável. Undo/redo não pode corromper o documento após edição externa.

## Recursos
Múltiplos cursores, seleção, busca, substituição, indentação, folding, diagnósticos, marcadores, navegação, formatação e edição multi-arquivo. Recursos caros devem ser configuráveis.

## Arquivos grandes
Suportar carregamento sob demanda, viewport virtualizado, cálculo incremental de linhas e limites configuráveis para recursos avançados. Arquivos binários não devem ser tratados como texto automaticamente.

## Integração linguística
Lexer/parser e language services não bloqueiam digitação. Cada resposta identifica a versão do documento analisada; respostas antigas são descartadas. Diagnósticos possuem intervalo, severidade, origem e código.

## Entrada e acessibilidade
Suportar teclado físico, IME, composição, atalhos configuráveis, navegação por foco, seleção acessível e escala de texto.

## Aceite
Testes de Unicode, undo/redo, cursores múltiplos, arquivos grandes, alterações externas, latência de digitação, busca e recuperação após encerramento.
