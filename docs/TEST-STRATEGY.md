# Estratégia de testes e qualidade

## Pirâmide
1. **Unitários:** lógica isolada, invariantes e tratamento de erros.
2. **Contrato:** compatibilidade entre módulos, bridge e formatos persistidos.
3. **Integração:** adaptadores, filesystem, runtime, processos e serviços.
4. **Sistema:** fluxos completos no Android e em dispositivos representativos.
5. **Performance:** inicialização, latência, memória, CPU, GPU e I/O.
6. **Segurança:** permissões, validação, isolamento, armazenamento e extensões.

## Regras
- Cada bug corrigido deve ter teste de regressão quando viável.
- Testes devem ser determinísticos, isolados e reproduzíveis.
- Testes que dependem de Android real devem ser identificados como instrumentados.
- Benchmarks devem registrar dispositivo, versão do sistema, build, carga e método.
- Não usar benchmark isolado como prova de desempenho geral.
- Falhas e testes ignorados devem ser reportados; não podem ser contabilizados como aprovados.

## Critérios de qualidade
Uma entrega só pode ser marcada como concluída quando os testes relevantes forem executados e os resultados registrados. Se o ambiente não permitir executar um teste, declarar explicitamente a limitação e não declarar conformidade total.
