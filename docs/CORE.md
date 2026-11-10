# Aurora Core

## Responsabilidade
O Aurora Core coordena serviços de domínio. Na primeira geração será Rust e não conterá código de apresentação. Deve funcionar em testes sem inicializar o UI Engine.

## Subsistemas
- **Lifecycle Manager:** inicialização, execução, suspensão e encerramento.
- **Service Registry:** registro e descoberta explícita de serviços.
- **Event Bus:** eventos tipados.
- **Task Manager:** filas, prioridades, cancelamento e limites.
- **Process Manager:** processos supervisionados pela EDS.
- **Configuration Manager:** configuração validada e hierárquica.
- **Persistence Service:** armazenamento transacional quando necessário.
- **Diagnostics:** logs, métricas, erros e rastreamento.

## Contratos
Cada serviço expõe interface pública pequena e versionada. Tipos públicos não vazam detalhes internos. Operações longas são assíncronas e nunca bloqueiam a thread da interface.

Eventos incluem versão de schema, identificador, timestamp, origem e payload tipado. Eventos notificam; comandos que exigem resposta usam chamadas de serviço.

## Tarefas
Uma tarefa possui ID, tipo, origem, prioridade, estado, progresso opcional, timestamps, política de cancelamento e resultado/erro. Estados mínimos: queued, running, succeeded, failed e cancelled. Transições inválidas são rejeitadas.

O escalonador limita concorrência por classe de tarefa e considera pressão de memória e lifecycle Android quando disponível. I/O e compilação não executam na thread de UI.

## Falhas
Erros são tipados e seguros para diagnóstico. Falhas recuperáveis de serviços opcionais não encerram o Core. Panics não atravessam FFI; fronteiras FFI convertem falhas em resultados explícitos.

## Aceite
Testes unitários de estados, filas, cancelamento, ordenação e concorrência; integração de inicialização/encerramento; estresse de tarefas simultâneas; execução do Core sem UI.
