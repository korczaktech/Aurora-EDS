# ADR-0010 — Migração gradual para Nebula

- **Estado:** Aceita como objetivo condicionado a critérios
- **Data:** 2026-11-10
- **Escopo:** código próprio do Aurora-EDS

## Contexto
Nebula é a linguagem de destino pretendida para reduzir dependência de implementações próprias em Rust e TypeScript. Uma migração prematura poderia comprometer estabilidade, portabilidade e manutenção.

## Decisão
A migração será incremental, orientada por módulos-piloto e condicionada à maturidade comprovada da toolchain Nebula para Android, interoperabilidade nativa, módulos, concorrência, memória, operações assíncronas, diagnóstico e testes automatizados.

Cada módulo migrado deverá preservar contratos públicos e demonstrar paridade funcional, de segurança e de desempenho dentro de limites previamente definidos. Rust/TypeScript só serão removidos de um módulo após a substituição validada. Dependências externas podem permanecer em suas linguagens originais quando necessário.

## Alternativas consideradas
- Reescrita integral imediata: rejeitada pelo risco e custo.
- Migração baseada apenas em compilação bem-sucedida: rejeitada por não provar paridade.
- Abandonar a meta Nebula: não adotada.

## Consequências
- Contratos devem ser independentes de linguagem desde o início.
- A roadmap deve reservar uma etapa de avaliação de prontidão.
- A migração pode ser adiada se os critérios não forem atingidos.
