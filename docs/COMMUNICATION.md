# Comunicação interna e bridge

## Objetivo
Definir comunicação estável entre Rust, runtime JavaScript e adaptadores Android, preservando a migração para Nebula.

## Fronteiras
- JNI conecta código nativo às APIs Java/Kotlin do Android.
- C ABI fornece fronteira nativa estável.
- Bridge Aurora apresenta operações tipadas aos consumidores.
- Módulos de produto não chamam JNI diretamente.

## Envelope lógico
Toda operação contém versão do protocolo, operation_id, request_id, origem, destino, tipo, payload e contexto de cancelamento. Respostas referenciam request_id e contêm resultado ou erro estruturado. Eventos têm event_id e sequência quando ordenação é necessária.

O formato físico (binário ou estruturado) será selecionado por benchmark e documentado em ADR. Não serializar dados grandes sem necessidade.

## Semântica
Chamadas síncronas são permitidas apenas para operações curtas e sem I/O. Operações longas são assíncronas e retornam ID de tarefa. Toda operação longa define cancelamento, timeout quando aplicável e comportamento após encerramento do consumidor.

## Memória e propriedade
Todo buffer transferido declara quem aloca, quem libera, se há cópia e por quanto tempo o dado é válido. Handles são opacos e possuem operação de liberação. Ponteiros crus não podem ser retidos pelo JavaScript sem mecanismo de vida útil.

## Erros e compatibilidade
Erros incluem código estável, categoria, mensagem segura, origem e detalhes opcionais. Segredos não aparecem em logs. Mudanças incompatíveis exigem nova versão ou negociação de capacidades.

## Testes
Cobrir round-trip, cancelamento, timeouts, concorrência, buffers, handles, falhas de runtime, incompatibilidade de versão e ausência de deadlocks.
