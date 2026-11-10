# Build System

## Objetivo
Orquestrar compilação, empacotamento e tarefas de projeto por adaptadores de ecossistema.

## Grafo de build
Um build é um grafo dirigido de tarefas. Cada nó declara entradas, saídas, dependências, comando/adaptador, ambiente, recursos e política de cache. Ciclos são detectados antes da execução.

## Execução
O executor agenda nós quando dependências terminam. Limites de concorrência consideram CPU, memória, temperatura e configuração do usuário. Tarefas expõem progresso, logs, cancelamento e resultado.

## Incrementalidade e cache
A chave de cache inclui hashes de entradas, opções, versões de ferramentas, ambiente relevante e dependências. Saídas só são reutilizadas após validação de integridade. Cache tem tamanho máximo e política de limpeza.

## Adaptadores
Cada sistema de build é integrado por adaptador versionado. O núcleo não assume que todos os projetos usam Cargo, Gradle ou outro sistema. Scripts arbitrários são código não confiável e exigem consentimento e permissões.

## Artefatos e diagnósticos
Artefatos possuem nome, tipo, localização, hash, tamanho, origem e metadados. Publicação e assinatura são etapas distintas da compilação.

Logs são associados a tarefas e, quando possível, convertidos em diagnósticos com arquivo, intervalo, severidade, código e origem. Saídas não reconhecidas permanecem disponíveis.

## Android
Builds locais dependem de toolchains, espaço, memória e permissões. Detectar limitações antes de tarefas pesadas e permitir execução remota por adaptador futuro.

## Aceite
Testar grafos, ciclos, cache inválido, builds incrementais, cancelamento, falhas de ferramenta, concorrência, pressão de memória e reprodutibilidade.
