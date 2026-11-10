# Versionamento e compatibilidade

## Versões de produto
O Aurora-EDS usará Semantic Versioning (MAJOR.MINOR.PATCH) quando houver uma versão pública estável:
- MAJOR: quebra incompatível de contratos públicos.
- MINOR: funcionalidade compatível.
- PATCH: correção compatível.

Antes da primeira versão estável, versões 0.y.z indicam evolução; contratos ainda podem mudar, mas mudanças devem ser registradas.

## Contratos
Cada API/protocolo público deve possuir versão própria quando puder evoluir independentemente do produto. A versão deve identificar formato, semântica e capacidades, não apenas a versão da implementação.

- Mudanças aditivas compatíveis incrementam a versão minor do contrato.
- Correções sem mudança semântica incrementam patch.
- Remoção, alteração de significado ou mudança incompatível incrementa major.
- Consumidores devem rejeitar versões não suportadas com erro explícito.
- Compatibilidade deve ser testada com fixtures e testes de contrato.

## Depreciação
Uma API só pode ser removida após aviso documentado, alternativa disponível e política de migração. Exceções por segurança devem registrar justificativa e impacto.
