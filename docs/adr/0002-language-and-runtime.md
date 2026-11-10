# ADR-0002 — Linguagens e runtime da primeira geração

- **Estado:** Aceita, sujeita a benchmark
- **Data:** 2026-11-10
- **Escopo:** Core e apresentação

## Contexto
A primeira geração precisa de uma linguagem de sistemas e de uma camada produtiva para compor a interface, sem misturar regras de domínio e apresentação.

## Decisão
Rust será a implementação inicial do Core e dos serviços de sistema. TypeScript será a linguagem de autoria da apresentação e será transpilado para JavaScript. Hermes será o runtime JavaScript inicial, encapsulado por uma interface substituível.

Hermes executa JavaScript; não renderiza UI. TypeScript não é executado diretamente. Nenhuma API específica de Hermes pode vazar para os contratos de módulos.

## Alternativas consideradas
- JavaScript sem TypeScript: rejeitada como linguagem de autoria inicial por reduzir garantias estáticas.
- Runtime acoplado ao Core: rejeitado por impedir substituição independente.
- Implementar toda a UI em Rust: não adotado para a primeira geração; pode ser reavaliado com evidência.

## Consequências
- O pipeline de build deve transpilar e empacotar TypeScript.
- O runtime precisa de isolamento, limites e gestão de erros.
- A escolha de Hermes deverá ser confirmada por benchmarks de inicialização, memória, throughput e integração Android.

## Revisão
Reavaliar se Hermes não atender aos limites de memória, inicialização, compatibilidade ou manutenção definidos antes do release.
