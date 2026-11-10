# Memória e gerenciamento de recursos

## Objetivo
Controlar memória nativa, runtime JavaScript, buffers, recursos gráficos, caches e processos para manter estabilidade em dispositivos móveis.

## Propriedade
Toda alocação e recurso externo possui proprietário e regra de liberação. Handles FFI têm lifecycle explícito. Recursos compartilhados definem referência, empréstimo ou transferência de propriedade. Ponteiros sem contrato são proibidos em APIs públicas.

## Orçamento
Cada subsistema expõe métricas e limites configuráveis. Valores concretos serão definidos por perfil de dispositivo e medição; não há um limite universal presumido.

## Caches
Caches possuem tamanho máximo, expiração e invalidação. Dados regeneráveis têm prioridade de descarte. Cache não é armazenamento durável.

## Pressão de memória
Ao receber sinal de pressão, liberar caches, reduzir buffers, suspender tarefas não essenciais e persistir estado recuperável. Evitar descartar dados não salvos.

## Recursos gráficos
Texturas, fontes, buffers e superfícies são liberados em encerramento, troca de contexto e perda de superfície. Reconstrução deve ser possível a partir de fontes ou dados persistentes.

## Diagnóstico e aceite
Separar métricas de heap Rust, heap JS, memória gráfica, buffers e processos quando possível. Testar ciclos de abrir/fechar projeto, arquivos grandes, reload, perda de superfície, pressão de memória e vazamentos.
