# ADR-0009 — Build System e cache

- **Estado:** Aceita
- **Data:** 2026-11-10
- **Escopo:** builds, testes e ferramentas

## Contexto
Builds devem ser reproduzíveis, canceláveis e eficientes, sem acoplar o Core a um compilador específico.

## Decisão
O Build System representará cada execução como um grafo direcionado acíclico (DAG) de tarefas com entradas, saídas, dependências, ambiente e estado declarados. Ferramentas externas serão integradas por adaptadores. Cache será baseado em hash de entradas relevantes, versão da ferramenta, configuração e ambiente declarado.

Uma saída só poderá ser reutilizada quando a chave de cache representar todas as entradas que influenciam o resultado. Tarefas devem expor progresso, logs, cancelamento e falhas estruturadas.

## Alternativas consideradas
- Scripts opacos como única representação: rejeitados por dificultarem análise e cache.
- Cache por nome de arquivo/data de modificação apenas: rejeitado por risco de falsos acertos.
- Build System acoplado a Cargo: rejeitado para manter suporte multilíngue.

## Consequências
- Adaptadores precisam declarar entradas e saídas.
- Cache incorreto é pior que ausência de cache; integridade prevalece sobre velocidade.
- Execução deverá respeitar limites de CPU, memória, armazenamento e concorrência.
