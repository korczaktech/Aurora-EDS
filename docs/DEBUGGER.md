# Debugger Manager

## Objetivo
Unificar experiência de depuração sem exigir que todas as linguagens usem o mesmo depurador.

## Sessão
Uma sessão possui ID, adaptador, alvo, processo, estado, breakpoints, threads, stack frames e capacidades negociadas. Estados mínimos: starting, running, paused, terminated e failed.

## Capacidades
Breakpoints, breakpoints condicionais quando suportados, continuar, pausar, step over/into/out, stack trace, variáveis, scopes, avaliação de expressão, exceções e inspeção de threads. Cada recurso anuncia suporte; a UI não exibe ação indisponível como funcional.

## Adaptadores
Adaptadores convertem protocolo interno para ferramentas específicas. A comunicação com adaptadores externos é isolada e validada. DAP pode ser suportado por adaptador, sem acoplar modelo interno a um único protocolo.

## Segurança e estabilidade
Avaliação de expressões pode executar código no processo depurado e deve ser tratada como operação de risco. Encerramento do projeto ou processo limpa breakpoints temporários e recursos da sessão.

## Aceite
Testar lifecycle, breakpoints, threads, frames, variáveis, processo encerrado, adaptador desconectado, capacidades parciais e sessões concorrentes.
