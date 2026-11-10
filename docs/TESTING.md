# Testes e qualidade

## Estratégia
Cada módulo possui testes adequados. Testes automatizados não substituem validação em dispositivos Android reais.

## Camadas
- **Unitários:** funções, estruturas, parsers, estados e algoritmos.
- **Integração:** contratos entre módulos, bridge e persistência.
- **Sistema:** inicialização, lifecycle, permissões e fluxos completos.
- **UI:** layout, eventos, foco, acessibilidade e regressão visual.
- **Performance:** latência, frames, CPU, memória, I/O e builds.
- **Segurança:** permissões, entradas malformadas, isolamento e dependências.

## Determinismo
Evitar dependência de rede e relógio real quando não necessário. Relógios, filesystem, processos e serviços externos devem possuir interfaces substituíveis em testes.

## Dispositivos
A matriz inclui versões Android, densidades, tamanhos de tela, RAM, arquiteturas e drivers. ARM64 é obrigatório para o alvo inicial.

## Performance
Benchmarks registram dispositivo, versão do sistema, build, estado relevante, tamanho da entrada, repetições e distribuição dos resultados. Comparações usam cenários equivalentes. Metas numéricas serão definidas após baseline medido.

## CI e release
CI deve formatar, lintar, compilar, executar testes disponíveis, verificar documentação e produzir diagnósticos. Falha de etapa obrigatória bloqueia validação. Release exige testes aprovados, revisão de segurança aplicável, compatibilidade, changelog, artefatos assinados e plano de rollback.
