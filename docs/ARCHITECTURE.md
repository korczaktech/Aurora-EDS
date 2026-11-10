# Arquitetura geral

## Objetivo
Definir limites estáveis entre Android, núcleo, runtime, UI Engine e serviços funcionais. A arquitetura prioriza isolamento, testabilidade, portabilidade e migração gradual para Nebula.

## Camadas
1. **Platform Adapter:** ciclo de vida Android, superfícies, permissões, armazenamento, entrada e APIs do sistema.
2. **Aurora Core:** serviços de domínio, estado, tarefas, eventos, processos e ciclo de vida dos módulos.
3. **Language Runtime:** frontend TypeScript executado por Hermes na primeira geração.
4. **UI Engine:** árvore visual, layout, eventos de interface, animações e renderização.
5. **Product Modules:** editor, Zeus, projetos, arquivos, builds, linguagens, Git, depuração e extensões.

Dependências seguem interfaces públicas. Módulos de produto não podem importar estruturas internas de outros módulos.

## Regras
- Core não depende de componentes visuais.
- UI Engine não executa regras de negócio de projetos.
- Frontend não acessa diretamente filesystem, processos ou APIs Android; solicita serviços autorizados.
- Adaptadores de plataforma não contêm regras de domínio.
- Integrações externas ficam atrás de adaptadores.
- Contratos entre camadas são versionados e independentes de linguagem.

## Inicialização e encerramento
A inicialização segue dependências: plataforma, configuração mínima, Core, serviços essenciais, runtime, UI Engine e módulos solicitados. Cada estágio deve ser idempotente ou detectar duplicidade.

O encerramento impede novas tarefas, cancela operações canceláveis, persiste estado necessário, libera recursos gráficos e fecha processos filhos conforme política. Falha de módulo opcional não pode derrubar todo o ambiente.

## Android e portabilidade
ARM64 é o alvo inicial. O NDK fornece toolchain e APIs nativas; Rust/Cargo compila para os targets Android apropriados. O NDK não é compilador Rust. APIs Android exclusivas do SDK podem exigir Kotlin/Java mínimo chamado por JNI.

A camada de plataforma oferece capacidades abstratas. Alvos futuros não devem exigir reescrita do Core.

## ADRs e validação
Backend gráfico, modelo de processos Android, runtime JS, formato de plugin, persistência e protocolo de bridge exigem ADR quando definidos em detalhe. Hermes e backends gráficos são decisões iniciais sujeitas a benchmark.

Testes de arquitetura verificam dependências permitidas, ausência de ciclos, isolamento de plataforma e compatibilidade de contratos.
