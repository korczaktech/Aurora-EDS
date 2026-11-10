# Architecture Decision Records (ADRs)

ADRs registram decisões arquiteturais duradouras do Aurora-EDS. São parte normativa da especificação.

## Estados
- **Proposta:** em discussão; não é vinculante.
- **Aceita:** decisão vigente.
- **Substituída:** superada por outra ADR, preservada para histórico.
- **Rejeitada:** avaliada e não adotada.

## Convenções
- Identificadores sequenciais: `ADR-NNNN`.
- Uma ADR trata de uma decisão principal.
- ADR aceita não é editada para mudar seu sentido; uma nova ADR a substitui.
- Mudanças devem registrar motivação, alternativas, consequências, riscos, validação e plano de migração.
- A implementação não altera uma decisão aceita implicitamente.

## Índice
| ADR | Decisão | Estado |
|---|---|---|
| [0001](0001-modular-architecture.md) | Arquitetura modular e limites entre camadas | Aceita |
| [0002](0002-language-and-runtime.md) | Linguagens e runtime da primeira geração | Aceita |
| [0003](0003-native-ui-and-rendering.md) | Interface nativa e estratégia de renderização | Aceita |
| [0004](0004-interoperability-and-bridge.md) | Interoperabilidade e bridge | Aceita |
| [0005](0005-android-process-model.md) | Processos e terminal no Android | Aceita |
| [0006](0006-storage-and-project-access.md) | Armazenamento e acesso a projetos | Aceita |
| [0007](0007-extension-security.md) | Segurança e extensões | Aceita |
| [0008](0008-editor-text-model.md) | Modelo de texto do editor | Aceita |
| [0009](0009-build-and-cache.md) | Builds e cache | Aceita |
| [0010](0010-nebula-migration.md) | Migração gradual para Nebula | Aceita |

## Revisão
Uma ADR deve ser reavaliada quando surgirem evidências que contradigam suas premissas, mudança relevante nas restrições Android, risco de segurança, regressão mensurável ou necessidade de quebrar um contrato público.
