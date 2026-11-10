# Roadmap do Aurora-EDS

## Princípios
As fases representam dependências técnicas, não datas prometidas. Uma fase só avança quando critérios de aceite são atendidos. Uma tela ou protótipo não comprova conclusão funcional.

## Fase 0 — Fundação documental
- Especificação central e documentos especializados.
- ADRs para decisões de alto impacto.
- Convenções de código, versionamento e testes.
- Contratos de módulos e comunicação.

**Saída:** arquitetura revisada, dependências definidas e validação aprovada.

## Fase 1 — Fundação nativa e Core
- Projeto Android mínimo.
- Toolchain Rust/NDK para ARM64.
- Adaptador de plataforma.
- Core, lifecycle, eventos e tarefas.
- Persistência, diagnósticos e bridge.

**Saída:** aplicação inicia, encerra e executa testes do Core sem UI completa.

## Fase 2 — Runtime e UI Engine
- Integração Hermes isolada.
- Pipeline TypeScript.
- Árvore de componentes e layout.
- Backend gráfico inicial.
- Entrada, acessibilidade e animações.

**Saída:** interface demonstrativa nativa com atualizações incrementais e métricas.

## Fase 3 — Fluxo básico
- File System Manager.
- Project Manager e workspace.
- Editor inicial.
- Zeus e processos.
- Configurações e recuperação de sessão.

**Saída:** abrir projeto, editar, salvar e executar comando suportado.

## Fase 4 — Ferramentas profissionais
- Sistema de linguagens e diagnósticos.
- Autocompletar.
- Build System e dependências.
- Git, depurador e Test Manager.

**Saída:** fluxo de build, diagnóstico e teste validado em projetos de referência.

## Fase 5 — Extensibilidade
- Manifestos e APIs públicas.
- Permissões e isolamento.
- Instalação, atualização e rollback.
- Adaptadores externos.

**Saída:** extensão de referência executada sob permissões controladas.

## Fase 6 — Estabilização
- Profiling em dispositivos reais.
- Otimização de memória, CPU, GPU e I/O.
- Resiliência e recuperação.
- Testes de segurança e compatibilidade.
- Builds reproduzíveis.

**Saída:** critérios de release documentados e atendidos.

## Fase 7 — Migração Nebula
- Toolchain Nebula Android.
- Módulo piloto.
- Migração progressiva do Core, UI e ferramentas.
- Remoção de Rust/TypeScript próprios quando houver paridade.

**Saída:** código próprio migrado conforme escopo aprovado, sem regressões de contrato.

## Gestão
Cada entrega registra escopo, dependências, critérios de aceite, testes, riscos e estado real. Datas e metas de desempenho só serão definidas após estimativas e baselines medidos.
