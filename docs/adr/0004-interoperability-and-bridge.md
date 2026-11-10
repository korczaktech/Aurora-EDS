# ADR-0004 — Interoperabilidade e bridge

- **Estado:** Aceita
- **Data:** 2026-11-10
- **Escopo:** Rust, runtime JavaScript e Android

## Contexto
Os subsistemas precisam trocar comandos, eventos e dados sem expor detalhes internos das linguagens ou criar dependências diretas.

## Decisão
JNI será usado na fronteira com APIs Android/JVM quando necessário. C ABI será usada para interoperabilidade nativa controlada. Ambas serão encapsuladas por uma bridge tipada, com contratos versionados e handles opacos.

Operações potencialmente demoradas serão assíncronas, identificáveis, canceláveis quando possível e correlacionadas por IDs. Payloads terão limites explícitos. Ownership, validade e liberação de memória serão definidos em cada contrato. Nenhum ponteiro Rust ou objeto interno do runtime será exposto como API pública.

## Alternativas consideradas
- JSON em toda chamada: rejeitado como formato universal por custo de serialização e cópia.
- Chamadas síncronas irrestritas: rejeitadas por risco de deadlock e bloqueio da UI.
- API específica de Rust/JS exposta a todos os módulos: rejeitada por acoplamento.

## Consequências
- A bridge exige documentação de erros, cancelamento, concorrência e ciclo de vida.
- Dados grandes devem usar transferência em lote ou buffers com ownership definido.
- Chamadas síncronas ficam restritas a operações pequenas e comprovadamente seguras.
