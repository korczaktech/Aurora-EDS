# Revisão da Fase 0 — Fundação documental

- **Data:** 2026-11-10
- **Estado:** documentação criada; revisão documental inicial concluída
- **Escopo:** consistência entre especificação, ADRs, contratos, políticas e roadmap

## Entregas documentais
- 10 ADRs para arquitetura modular, linguagens/runtime, UI/renderização, bridge, processos Android, armazenamento, segurança de extensões, modelo de texto, builds/cache e migração Nebula.
- Contratos comuns entre módulos.
- Convenções de desenvolvimento.
- Política de versionamento e compatibilidade.
- Estratégia de testes e qualidade.
- Índices atualizados no README e na especificação central.
- Critérios de saída da Fase 0 detalhados no roadmap.

## Revisão de consistência

| Área | Verificação | Resultado |
|---|---|---|
| Camadas e dependências | Core, Runtime, UI Engine, plataforma e módulos mantêm responsabilidades separadas | Coerente |
| Linguagens e runtime | TypeScript é transpilado; Hermes executa JavaScript; UI Engine renderiza | Coerente |
| Android e toolchain | NDK é tratado como toolchain/API nativa, não como compilador Rust | Coerente |
| Bridge | JNI/C ABI ficam atrás de contratos tipados; operações longas são assíncronas | Coerente |
| Arquivos | Recursos são URI/IDs abstratos; SAF e permissões Android são considerados | Coerente |
| Zeus | Não pressupõe shell Linux completo nem root | Coerente |
| Extensões | Permissões e capacidades são mediadas; limitações de isolamento precisam ser explícitas | Coerente |
| Editor | Estrutura de buffer depende de benchmark; unidades de posição são explícitas | Coerente |
| Build | DAG e cache consideram entradas e ambiente relevantes | Coerente |
| Nebula | Migração depende de paridade demonstrada, não apenas de compilação | Coerente |

## Decisões que permanecem condicionadas a evidências

Estas decisões estão registradas como direção arquitetural, mas não autorizam implementação cega:
- Hermes deverá ser confirmado por benchmark em dispositivos-alvo.
- Canvas e Vulkan serão avaliados por capacidade, compatibilidade e medição; Vulkan não é obrigatório.
- Rope, Piece Table e Gap Buffer serão comparados antes da escolha do modelo concreto do editor.
- O modelo de execução de processos depende das restrições reais de cada versão Android e das ferramentas empacotadas.
- O isolamento efetivo de extensões deve ser comprovado antes de habilitar extensões não confiáveis.

## Limites desta revisão
Esta é uma revisão documental. Não representa auditoria de código, validação de build, teste em dispositivo Android, benchmark ou certificação de segurança. O repositório ainda não foi declarado funcional por causa destas entregas.

## Critérios restantes para encerrar formalmente a Fase 0
- [x] ADRs e índice publicados.
- [x] Contratos comuns publicados.
- [x] Convenções de contribuição publicadas.
- [x] Política de versionamento publicada.
- [x] Estratégia de testes publicada.
- [x] README, especificação e roadmap atualizados.
- [x] Revisão de consistência documental inicial registrada.
- [ ] Revisão humana final das decisões arquiteturais.
- [ ] Aprovação explícita do baseline documental para iniciar a Fase 1.

A Fase 0 só deve ser marcada como formalmente concluída após a revisão humana e a aprovação do baseline.