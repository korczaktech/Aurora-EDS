# ADR-0001 — Arquitetura modular e limites entre camadas

- **Estado:** Aceita
- **Data:** 2026-11-10
- **Escopo:** arquitetura global

## Contexto
O Aurora-EDS reúne editor, terminal, projetos, builds, linguagens e extensões. Sem limites explícitos, os módulos se tornam acoplados à interface, à plataforma e uns aos outros.

## Decisão
Adotar camadas com dependências direcionadas: Platform Adapter, Aurora Core, Language Runtime, UI Engine e Product Modules. Contratos públicos versionados serão a única forma de integração entre camadas e módulos.

O Core não depende da UI. A UI não implementa regras de domínio. Módulos não acessam estruturas privadas de outros módulos. A plataforma não contém regras de produto. Dependências cíclicas entre módulos são proibidas.

## Alternativas consideradas
- Aplicação monolítica: rejeitada por dificultar isolamento, testes e evolução.
- Módulos com dependência livre: rejeitada pelo risco de acoplamento.
- Microserviços locais: rejeitados para a primeira geração pelo custo operacional e de comunicação em dispositivo móvel.

## Consequências
- Interfaces e ownership precisam ser definidos antes da integração.
- O sistema ganha testabilidade e possibilidade de substituição de implementações.
- Há custo inicial de desenho e manutenção dos contratos.

## Validação
Testes arquiteturais devem detectar ciclos, imports privados entre módulos e dependências de UI dentro do Core. Integrações devem usar somente interfaces publicadas.
