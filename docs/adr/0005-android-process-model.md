# ADR-0005 — Processos e terminal Zeus no Android

- **Estado:** Aceita, condicionada às capacidades do sistema
- **Data:** 2026-11-10
- **Escopo:** Zeus e Process Manager

## Contexto
Zeus precisa executar ferramentas e comandos, mas Android não equivale a uma distribuição Linux convencional. Aplicativos estão sujeitos a sandbox, permissões, ciclo de vida e restrições de execução em segundo plano.

## Decisão
Zeus será um subsistema de sessões e processos, não uma promessa de shell Linux completo. O Process Manager utilizará APIs de processo disponíveis no ambiente do aplicativo e adaptadores explícitos para ferramentas embarcadas ou ambientes externos autorizados.

Cada execução terá diretório de trabalho, ambiente permitido, stdin/stdout/stderr, estado, código de saída, limites e política de cancelamento. Execução em segundo plano dependerá das regras do Android e de mecanismos apropriados, nunca de uma suposição de processo persistente.

## Alternativas consideradas
- Presumir shell Linux completo: rejeitada por não refletir as garantias do Android.
- Executar todos os comandos dentro do processo principal: rejeitada por isolamento e estabilidade.
- Exigir root: rejeitada.

## Consequências
- Compatibilidade de comandos será declarada por ambiente e capacidade.
- Processos devem ser encerrados ou recuperados conforme política do ciclo de vida.
- Ferramentas nativas precisam ser empacotadas e compiladas para ABI suportada.
- Segurança e limites de recursos são requisitos de primeira classe.
