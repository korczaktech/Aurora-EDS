# ADR-0007 — Segurança e extensões

- **Estado:** Aceita
- **Data:** 2026-11-10
- **Escopo:** extensões, scripts e integrações

## Contexto
Extensões aumentam a capacidade do Aurora-EDS, mas código de terceiros não pode herdar automaticamente acesso a arquivos, processos, rede ou segredos.

## Decisão
Adotar privilégio mínimo, permissões declaradas e concedidas explicitamente, validação de manifestos, identidade e versão de extensão, e APIs mediadas pelo Core. Extensões não recebem acesso direto a ponteiros internos, armazenamento privado ou processos privilegiados.

O isolamento será aplicado por capacidades e limites de API. Quando isolamento de processo não for tecnicamente disponível, a limitação deverá ser documentada e a execução restrita. Segredos não serão incluídos em logs. Atualizações devem suportar verificação de integridade e recuperação/rollback quando aplicável.

## Alternativas consideradas
- Confiança total em extensões instaladas: rejeitada.
- Sandbox apenas documental: rejeitada como controle suficiente.
- Permissões globais permanentes: rejeitadas.

## Consequências
- APIs públicas precisam declarar capacidades exigidas.
- Instalação, atualização e execução devem ser auditáveis.
- O modelo de ameaça e as limitações de isolamento precisam ser revistos antes de habilitar extensões de terceiros.
