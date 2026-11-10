# Contratos entre módulos

## Objetivo
Definir regras comuns de integração para Platform Adapter, Aurora Core, Runtime, UI Engine e Product Modules. Os contratos específicos serão detalhados por subsistema.

## Regras obrigatórias
- Consumidores dependem de interfaces públicas, nunca de estruturas privadas.
- Cada operação declara entrada, saída, erros, efeitos, permissões e comportamento de cancelamento.
- Cada evento declara produtor, schema, semântica de entrega e política de retenção.
- Toda operação assíncrona possui identificador de correlação e estado observável.
- Recursos têm ownership, ciclo de vida e regra de liberação explícitos.
- Nenhuma chamada longa pode bloquear a thread principal da UI.
- Interfaces devem ser independentes de Rust, TypeScript, Hermes e detalhes Android.
- Dados externos são não confiáveis e devem ser validados na fronteira.
- APIs com acesso a arquivos, processos, rede ou segredos exigem capacidade explícita.
- Erros são tipados e estáveis; mensagens para humanos não substituem códigos de erro.

## Envelope de operação
Uma operação lógica deve definir: versão do contrato, identificador, operação, origem, destino, payload tipado, correlação, prazo opcional e capacidades requeridas. A codificação concreta será definida pela ADR da bridge e pelo contrato do subsistema.

## Ciclo de vida
Módulos devem declarar inicialização, disponibilidade, suspensão, encerramento e recuperação. O encerramento deve impedir novas operações, cancelar as canceláveis e liberar recursos. Chamadas após encerramento retornam erro previsível.

## Evolução
Mudanças incompatíveis exigem nova versão major e plano de migração. Compatibilidade será verificada por testes de contrato e fixtures versionadas.
