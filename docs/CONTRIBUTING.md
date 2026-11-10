# Convenções de desenvolvimento

Este documento define o fluxo de contribuição e implementação do Aurora-EDS.

## Princípios
- Priorizar correção, segurança e clareza sobre atalhos.
- Manter módulos pequenos, com responsabilidade e ownership definidos.
- Não introduzir dependência sem justificar escopo, manutenção, licença e impacto.
- Não afirmar que algo funciona sem evidência reproduzível.
- Atualizar documentação e testes junto com mudanças de contrato.

## Organização
- Código deve permanecer dentro do módulo responsável.
- APIs públicas devem ser separadas de implementações internas.
- Adaptadores externos devem ficar identificados e isolados.
- Evitar dependências cíclicas.
- Configurações, segredos e dados do usuário não devem ser commitados.

## Estilo
- Seguir formatter e linter oficiais de cada linguagem.
- Usar nomes explícitos e consistentes; evitar abreviações não convencionais.
- Documentar APIs públicas, invariantes, ownership, erros e concorrência.
- Tratar erros explicitamente; não ocultar falhas com valores padrão silenciosos.
- Comentários explicam intenção e invariantes, não repetem o código.

## Mudanças
Toda mudança deve indicar problema, escopo, módulos afetados, riscos, testes executados e limitações conhecidas. Mudanças incompatíveis exigem ADR aceita antes da implementação.

## Revisão
Verificar segurança, ciclo de vida, cancelamento, memória, acessibilidade, desempenho e compatibilidade Android conforme o escopo. Não misturar refatorações não relacionadas com correções funcionais.
