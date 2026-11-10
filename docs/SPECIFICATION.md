# Especificação técnica — Aurora-EDS

**Versão:** 1.0.0 · **Status:** normativa para arquitetura; implementação sujeita a validação.

Este é o índice normativo das especificações. O README apresenta a visão geral; os documentos especializados definem responsabilidades, limites, contratos e critérios verificáveis.

## Linguagem normativa
- **DEVE:** requisito obrigatório.
- **NÃO DEVE:** proibição.
- **DEVERIA:** recomendação forte; exceções exigem justificativa.
- **PODE:** comportamento opcional.

Uma especificação não comprova implementação. Requisitos só são atendidos após implementação, testes e evidências.

## Decisões vigentes

| Tema | Decisão |
|---|---|
| Plataforma | Android, ARM64 prioritário |
| Núcleo inicial | Rust |
| Interface inicial | TypeScript transpilado para JavaScript |
| Runtime inicial | Hermes, isolado por adaptador |
| UI | Engine próprio, nativo, sem WebView/Chromium |
| Gráficos | Backend abstrato; Canvas de compatibilidade e Vulkan quando viável |
| Integração | JNI/C ABI; Kotlin/Java mínimo quando exigido pelo Android SDK |
| Terminal | Zeus, inicialmente Rust |
| Linguagem de destino | Nebula para o código próprio, em migração gradual |

## Fundação documental
- [Índice de ADRs](adr/README.md)
- [Contratos entre módulos](MODULE-CONTRACTS.md)
- [Convenções de desenvolvimento](CONTRIBUTING.md)
- [Versionamento e compatibilidade](VERSIONING.md)
- [Estratégia de testes](TEST-STRATEGY.md)
- [Revisão da Fase 0](PHASE-0-REVIEW.md)

## Documentos especializados
- [Arquitetura geral](ARCHITECTURE.md)
- [Aurora Core](CORE.md)
- [Runtime](RUNTIME.md)
- [UI Engine](UI-ENGINE.md)
- [Renderizador](RENDERER.md)
- [Comunicação interna](COMMUNICATION.md)
- [Editor](EDITOR.md)
- [Terminal Zeus](ZEUS.md)
- [Projetos e workspaces](PROJECT-MANAGER.md)
- [Sistema de arquivos](FILE-SYSTEM.md)
- [Build System](BUILD-SYSTEM.md)
- [Sistema de linguagens](LANGUAGE-SYSTEM.md)
- [Depurador](DEBUGGER.md)
- [Extensões](EXTENSIONS.md)
- [Segurança](SECURITY.md)
- [Memória e recursos](MEMORY.md)
- [Testes e qualidade](TESTING.md)
- [Migração para Nebula](NEBULA-MIGRATION.md)
- [Roadmap](ROADMAP.md)

## Precedência e mudanças
Em caso de conflito, prevalecem ADRs aprovadas, esta especificação e documentos especializados, documentação explicativa e, por último, implementação existente. Código não documentado não altera silenciosamente contratos.

Mudanças incompatíveis exigem ADR com motivação, alternativas, impacto, migração e validação.

## Conformidade
Um subsistema só estará conforme quando tiver escopo e API documentados, implementação funcional, testes relevantes, tratamento de falhas, gestão de recursos, integração validada e evidências de desempenho quando aplicável.
