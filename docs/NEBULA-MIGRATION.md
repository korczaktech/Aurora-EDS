# Estratégia de migração para Nebula

## Objetivo
Migrar progressivamente o código próprio do Aurora-EDS para Nebula sem interromper o produto nem quebrar contratos entre subsistemas.

## Princípio
A migração é meta arquitetural, não suposição de que Nebula já possui todas as capacidades. Nenhum componente será migrado até que linguagem, compilador e runtime suportem seus requisitos e existam testes equivalentes.

## Pré-requisitos
- Compilação confiável para Android/ARM64.
- ABI e interoperabilidade nativa.
- Modelo de memória adequado.
- Concorrência e operações assíncronas.
- Módulos e linking.
- Acesso controlado às APIs Android.
- Integração com UI Engine e renderização.
- Diagnóstico, testes e profiling.

## Fases
1. **Preparação:** contratos independentes de linguagem e inventário de módulos.
2. **Toolchain:** validar compilação e interoperabilidade Nebula em projeto mínimo Android.
3. **Piloto:** migrar serviço isolado e comparar comportamento.
4. **Core:** migrar serviços por fronteiras estáveis.
5. **UI:** definir como Nebula substituirá lógica TypeScript; não presumir que Hermes permanecerá na arquitetura final.
6. **Ferramentas:** migrar Zeus e outros subsistemas individualmente.
7. **Desativação:** remover implementações antigas somente após paridade, cobertura e rollback comprovados.

## Paridade
Cada migração possui testes de equivalência, benchmark comparável, rollback e critério objetivo. Durante coexistência, uma única implementação é autoridade para cada operação; evitar dupla escrita.

## Interoperabilidade
Mesmo com código próprio migrado, o produto continuará interoperando com Android SDK, bibliotecas nativas, toolchains e ferramentas externas.

## Runtime
A substituição de TypeScript implica reavaliar Hermes. O runtime JS pode ser removido quando nenhum módulo depender dele. Exigir ADR e validação.
