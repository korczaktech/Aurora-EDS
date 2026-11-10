# Aurora-EDS

## Estação de Desenvolvimento de Sistemas

**Categoria:** Estação de Desenvolvimento de Sistemas (EDS)  
**Plataforma inicial:** Android  
**Arquitetura:** Nativa, modular, orientada a eventos e extensível  
**Linguagens iniciais:** Rust e TypeScript  
**Linguagem de destino:** Nebula  
**Terminal integrado:** Zeus  
**Versão da especificação:** 1.0.0  
**Status:** Especificação arquitetural inicial normativa

---

# 1. Definição do produto

O Aurora-EDS é uma Estação de Desenvolvimento de Sistemas destinada à criação, edição, execução, compilação, depuração, gerenciamento e distribuição de projetos de software.

Uma EDS não deve ser limitada ao conceito tradicional de editor de código. O Aurora-EDS deverá reunir, em um único ambiente, ferramentas que normalmente são distribuídas entre diferentes aplicativos:

- Edição de código e gerenciamento de arquivos.
- Gerenciamento de projetos e workspaces.
- Terminais e execução de processos.
- Compiladores, interpretadores e depuradores.
- Sistemas de build e gerenciamento de dependências.
- Controle de versão e integração com Git.
- Testes automatizados e análise estática.
- Inspeção de processos e recursos.
- Integração com ferramentas externas.
- Extensões, módulos e ambientes de execução.

O sistema deverá administrar o ciclo de desenvolvimento de software, desde a criação do projeto até sua compilação e distribuição.

## 1.1. Princípios fundamentais

1. Arquitetura nativa.
2. Separação rigorosa entre interface e núcleo.
3. Baixo consumo de memória e recursos.
4. Processamento paralelo e execução assíncrona.
5. Modularidade e extensibilidade.
6. Segurança por isolamento e permissões.
7. Independência de uma linguagem específica.
8. Interfaces internas estáveis e versionadas.
9. Compatibilidade com ferramentas e ecossistemas externos.
10. Evolução progressiva sem reconstrução integral do sistema.

# 2. Plataformas e tecnologias

## 2.1. Plataforma inicial

O primeiro alvo será Android. A arquitetura deverá considerar:

- Android SDK e Android NDK.
- ARM64 como ABI prioritária.
- ARM32 quando tecnicamente viável.
- Integração com armazenamento e permissões Android.
- Ciclo de vida de aplicativos e gerenciamento de janelas.
- Teclado físico e virtual, toque e acessibilidade.
- Serviços em segundo plano conforme as restrições do Android.

O núcleo deverá evitar dependências desnecessárias da plataforma. APIs específicas deverão ficar em adaptadores, permitindo futuros alvos como Linux e Windows.

## 2.2. Rust

Rust será responsável inicialmente pelo núcleo e pelos serviços de sistema:

- Gerenciamento de projetos, arquivos e sessões.
- Processamento, tarefas, concorrência e eventos.
- Gerenciamento de processos e recursos.
- Comunicação entre módulos.
- Segurança e persistência.
- Sistemas de build e dependências.
- Infraestrutura do terminal Zeus.
- Núcleo do editor e serviços linguísticos quando apropriado.

## 2.3. TypeScript

TypeScript será responsável pela camada de apresentação:

- Componentes visuais e composição de telas.
- Navegação, interações e estados visuais.
- Animações e personalização.
- Representação de informações e painéis.

O TypeScript não deverá assumir responsabilidades de negócio que pertencem ao núcleo.

O código TypeScript será transpilado e empacotado para execução em um runtime JavaScript embarcado.

## 2.4. Runtime JavaScript

O runtime inicial escolhido é **Hermes**.

Hermes executará JavaScript; não será responsável pelo desenho ou pela renderização da interface. A integração deverá ficar isolada por uma API própria para permitir substituição futura caso benchmarks demonstrem que outro runtime atende melhor aos requisitos.

## 2.5. Nebula

Nebula será a linguagem de destino do código próprio do Aurora-EDS.

A arquitetura deverá permitir a substituição progressiva das implementações próprias em Rust e TypeScript por implementações Nebula, preservando contratos, APIs e formatos de comunicação.

A migração não será abrupta. Ela dependerá de suporte comprovado de Nebula a compilação Android, interoperabilidade nativa, módulos, memória, concorrência, operações assíncronas e integração com o UI Engine.

# 3. Arquitetura geral

O Aurora-EDS será dividido em camadas independentes.

## 3.1. Plataforma nativa

Responsável pela comunicação com o sistema operacional:

- Inicialização Android e ciclo de vida.
- Janelas, superfícies e entrada de dispositivos.
- Permissões e armazenamento.
- Integração com APIs Android.
- Serviços e notificações.

Será permitida uma camada mínima de integração Kotlin/Java quando uma API estiver disponível exclusivamente pelo Android SDK. Essa camada não conterá regras de negócio do Aurora-EDS.

## 3.2. Aurora Core

Núcleo principal, inicialmente em Rust. Responsável por:

- Inicialização e coordenação dos subsistemas.
- Estado, eventos, tarefas e processos.
- Projetos, arquivos, ferramentas e extensões.
- Segurança, configurações e persistência.
- Ciclo de vida dos módulos.

Operações importantes não deverão depender diretamente da interface.

## 3.3. Runtime

Responsável pela execução da interface TypeScript:

- Transpilação e bundling.
- Carregamento de módulos.
- Execução JavaScript por Hermes.
- Gerenciamento de contexto.
- Comunicação com o núcleo.
- Controle de erros e recursos do runtime.

## 3.4. UI Engine

Sistema próprio de interface nativa, responsável por:

- Árvore de componentes.
- Layout e renderização.
- Atualizações incrementais.
- Eventos visuais e entrada.
- Animações e acessibilidade.
- Gerenciamento de superfícies.

Não será utilizado WebView, Chromium ou DOM de navegador como base da interface.

## 3.5. Sistemas funcionais

Subsistemas independentes:

- Editor.
- Explorador e sistema de arquivos.
- Terminal Zeus.
- Gerenciador de projetos e workspaces.
- Compiladores e depuradores.
- Sistema de extensões.
- Controle de versão.
- Gerenciador de dependências.
- Build System e Test Manager.

# 4. Renderização nativa

## 4.1. Estratégia

Será adotada uma arquitetura de renderização nativa com renderizador próprio e integração seletiva com componentes Android nativos.

O sistema utilizará:

1. Superfície nativa para a interface principal.
2. Renderizador próprio para componentes visuais de alta densidade.
3. Componentes Android nativos quando houver vantagem funcional, de acessibilidade ou integração.
4. CPU para layout e preparação de cenas.
5. GPU para operações gráficas compatíveis.

## 4.2. Backends gráficos

A arquitetura gráfica será independente do backend.

- **Android Canvas:** backend inicial de compatibilidade.
- **Vulkan:** backend acelerado prioritário quando disponível e vantajoso.
- Outros backends poderão ser adicionados sem alterar os componentes públicos.

A seleção deverá considerar capacidades reais do dispositivo e possuir fallback seguro.

## 4.3. Capacidades do renderizador

Deverá suportar texto, ícones, formas, bordas, sombras, gradientes, imagens, recortes, transformações, opacidade, camadas, clipping, scroll e composição de elementos.

## 4.4. Layout Engine

O mecanismo de layout será independente do runtime TypeScript e deverá suportar:

- Layout em linha e coluna.
- Posicionamento relativo e absoluto.
- Dimensionamento e restrições.
- Alinhamento e distribuição.
- Margens e espaçamentos.
- Redimensionamento e layout responsivo.
- Scroll e medição de texto.

O cálculo deverá ser incremental, evitando recalcular toda a interface quando somente um componente mudar.

## 4.5. Árvore de interface

Cada componente deverá possuir identificador estável, tipo, propriedades, estado visual, relações hierárquicas, eventos, restrições de layout e informações de acessibilidade.

O UI Engine deverá implementar diff de árvore e atualizar somente os elementos afetados.

# 5. Comunicação interna

## 5.1. Bridge

A comunicação inicial entre Rust, runtime JavaScript e plataforma nativa utilizará JNI e interfaces C ABI, encapsuladas por uma bridge pequena, tipada e independente dos módulos funcionais.

## 5.2. Protocolo de mensagens

Cada mensagem deverá definir:

- Identificador da operação.
- Origem e destino.
- Tipo da mensagem.
- Payload tipado.
- Identificador de correlação.
- Informações de erro quando aplicáveis.

O protocolo deverá suportar chamadas síncronas restritas, chamadas assíncronas, eventos, respostas, cancelamento, notificações e transferência de dados em lote.

## 5.3. Regras de desempenho

A comunicação deverá minimizar serializações, cópias de memória, chamadas repetitivas e bloqueios de thread.

Atualizações visuais deverão ser agrupadas. Animações não poderão depender de chamadas Rust por frame: deverão executar no runtime ou no subsistema nativo de animação.

## 5.4. Independência de linguagem

A bridge e os contratos não deverão expor detalhes internos de Rust ou TypeScript. Essa independência será obrigatória para a migração futura para Nebula.

# 6. Aurora Core

## 6.1. Estado

O núcleo deverá administrar estado global e estados por domínio: projetos, sessões, módulos, processos, tarefas e configurações. O estado será dividido por responsabilidade, evitando acoplamento em uma estrutura global única.

## 6.2. Event Bus

Será implementado um sistema interno de eventos tipados, com assinaturas, cancelamento, filtragem, prioridades e entrega assíncrona.

Eventos não deverão substituir indiscriminadamente chamadas diretas entre serviços.

## 6.3. Task Manager

Deverá executar tarefas assíncronas com filas, prioridades, cancelamento, dependências, limites de concorrência, tratamento de falhas e monitoramento.

Tarefas longas nunca poderão bloquear a thread da interface.

## 6.4. Process Manager

Cada processo gerenciado deverá possuir identificador, estado, origem, recursos utilizados, entrada, saída, erros, código de encerramento e possibilidade de cancelamento.

O sistema deverá distinguir processos internos, comandos do Zeus e processos externos.

# 7. Editor de código

O editor será um componente próprio, independente da interface geral. Seu núcleo de edição será inicialmente implementado em Rust; a camada TypeScript cuidará da apresentação e das interações.

## 7.1. Recursos obrigatórios

- Edição de texto, cursor e seleção.
- Múltiplos cursores e seleção múltipla.
- Desfazer e refazer.
- Busca e substituição, inclusive no projeto.
- Indentação e autoindentação.
- Numeração e guias de linhas.
- Destaque de sintaxe.
- Diagnósticos e marcadores.
- Code folding.
- Edição de múltiplos arquivos.
- Navegação por símbolos e definições.
- Autocompletar e formatação.
- Referências e histórico de alterações.

## 7.2. Modelo de texto

O editor deverá utilizar estrutura otimizada para edição incremental. A implementação deverá avaliar rope, piece table e gap buffer por benchmarks.

O modelo deverá considerar buffers, linhas, índices, intervalos, inserções, remoções, transações e histórico. Uma alteração de caractere não poderá reconstruir integralmente o documento.

## 7.3. Linguagens iniciais

Rust, TypeScript, JavaScript, JSON, HTML, CSS, Markdown e Nebula. Novas linguagens poderão ser adicionadas por módulos.

# 8. Sistema de linguagens

A infraestrutura de linguagens deverá ser independente de uma linguagem específica.

Cada integração poderá registrar:

- Identificação e extensões.
- Gramática, lexer e parser.
- Análise semântica.
- Destaque e temas.
- Diagnósticos.
- Autocompletar e formatação.
- Navegação e símbolos.
- Compilador, interpretador e depurador.

O sistema deverá permitir suporte de edição mesmo quando não houver compilador integrado.

## 8.1. Language Services

Será criado um protocolo interno para diagnósticos, autocompletar, hover, definições, referências, símbolos, formatação, ações de código e renomeação.

Deverá existir compatibilidade futura com LSP por meio de adaptadores, sem obrigar o núcleo a depender diretamente dele.

# 9. Terminal Zeus

## 9.1. Definição

Zeus será o terminal nativo oficial do Aurora-EDS, desenvolvido em Rust inicialmente.

Não será apenas uma janela que executa comandos: será um subsistema de interpretação, execução e gerenciamento de processos integrado ao núcleo.

## 9.2. Responsabilidades

- Interpretar comandos.
- Executar programas e ferramentas.
- Gerenciar sessões e processos.
- Controlar entrada, saída e erros.
- Gerenciar variáveis de ambiente e diretórios.
- Suportar pipelines e redirecionamento.
- Controlar sinais e interrupções.
- Exibir resultados e logs.
- Manter histórico.
- Integrar comandos próprios da EDS.

## 9.3. Componentes

- **Zeus Core:** interpretação e gerenciamento das sessões.
- **Zeus Shell:** sintaxe e avaliação dos comandos.
- **Zeus Process Manager:** processos, sinais, entrada, saída e encerramento.
- **Zeus I/O:** comunicação com processos.
- **Zeus Interface:** apresentação visual integrada ao Aurora-EDS.

## 9.4. Funcionalidades

Múltiplas sessões, histórico persistente, autocompletar, comandos internos e externos, variáveis de ambiente, redirecionamento, pipelines, execução em segundo plano quando suportada, interrupção de processos, estilos, links detectáveis, saída estruturada e integração com projetos.

Os comandos próprios serão definidos em uma especificação específica do Zeus, com categorias para projetos, builds, testes, compilação, dependências, extensões, configurações, diagnósticos e processos.

## 9.5. Compatibilidade

Zeus deverá respeitar as limitações de permissões e execução do Android. Não deverá presumir que o Android oferece um ambiente Linux completo. Compatibilidade com shells externos será modular.

# 10. Gerenciamento de projetos e workspaces

O Project Manager deverá criar, abrir, fechar, importar e exportar projetos; detectar estruturas; gerenciar configurações, linguagens, dependências, scripts e tarefas; e integrar editor e Zeus.

Cada projeto poderá conter identificação, nome, descrição, diretório, linguagens, dependências, configurações, ferramentas e metadados.

O sistema deverá suportar múltiplos projetos por sessão. O workspace controlará projetos, arquivos abertos, painéis, terminais, configurações, layout e estado de edição. O estado recuperável deverá ser persistido após encerramentos inesperados.

# 11. Sistema de arquivos

O File System Manager deverá oferecer leitura, escrita, criação, remoção, renomeação, movimentação, listagem, monitoramento de alterações, busca, filtros, metadados e operações em lote.

Deverá suportar o modelo de armazenamento Android, incluindo Storage Access Framework quando necessário. O acesso será controlado por permissões explícitas; não se presumirá acesso irrestrito ao armazenamento.

# 12. Build System

O Aurora-EDS terá um gerenciador central de builds, responsável por identificar sistemas de build, executar compiladores, resolver dependências, gerenciar configurações e etapas, registrar logs, gerar artefatos, detectar falhas e controlar tarefas.

Componentes:

- Build Manager.
- Build Graph.
- Dependency Resolver.
- Build Executor.
- Cache Manager.
- Artifact Manager.
- Diagnostics Processor.

Builds incrementais deverão reconstruir somente partes afetadas, considerando dependências, entradas, saídas, configurações, versões de compiladores, hashes e cache.

Etapas independentes poderão executar paralelamente, respeitando limites de recursos do dispositivo.

# 13. Gerenciador de dependências

O Dependency Manager deverá oferecer instalação, remoção, atualização, resolução e bloqueio de versões, verificação de integridade, cache, detecção de conflitos, inventário e auditoria.

Diferentes ecossistemas serão suportados por adaptadores. O Aurora-EDS não imporá um único formato de dependências a todos os projetos.

# 14. Depuração

O Debugger Manager deverá integrar depuradores e ferramentas de inspeção.

Recursos previstos:

- Breakpoints e breakpoints condicionais.
- Execução passo a passo.
- Inspeção de variáveis e pilha de chamadas.
- Inspeção de threads e processos.
- Exceções e logs.
- Inspeção de memória quando suportada.
- Avaliação de expressões e controle de execução.

Uma API interna comum deverá abstrair diferenças entre depuradores externos e ferramentas específicas de cada linguagem.

# 15. Sistema de extensões

O Aurora-EDS deverá permitir extensões para linguagens, temas, componentes visuais, ferramentas, compiladores, depuradores, integrações, comandos Zeus, adaptadores de build e gerenciadores de dependências.

## 15.1. Manifesto

Cada extensão deverá declarar identificador, nome, versão, autor, descrição, compatibilidade, dependências, permissões, pontos de integração, arquivos e entradas.

## 15.2. Segurança e isolamento

Extensões não terão acesso irrestrito ao núcleo. O sistema deverá implementar permissões explícitas, APIs controladas, isolamento de execução, limites de recursos, controle de arquivos e processos e registro de atividades.

## 15.3. Ciclo de vida

Estados possíveis: não instalada, instalada, carregada, ativa, suspensa, com falha e desativada.

Deverá ser possível instalar, atualizar, desativar e remover extensões.

# 16. Interface, animações e acessibilidade

## 16.1. Composição

A interface deverá possuir área principal, navegação, explorador, editor, terminal, painéis auxiliares, barra de status, gerenciador de tarefas, diagnósticos e notificações.

A composição será modular. O usuário poderá reorganizar painéis e salvar layouts.

## 16.2. Componentes reutilizáveis

O UI Engine deverá oferecer botões, campos, menus, listas, árvores, abas, painéis, modais, popovers, tooltips, barras, indicadores, seletores, navegação e componentes de editor.

## 16.3. Animações

O subsistema de animações deverá suportar transições, interpolação, curvas de aceleração, transformações, opacidade, movimento, redimensionamento e animações compostas.

As animações deverão executar independentemente do processamento de negócio. Deverá ser possível reduzir ou desativar animações.

## 16.4. Acessibilidade

Deverá oferecer compatibilidade com leitores de tela, descrições semânticas, navegação por teclado, foco visível, escala de texto, contraste, alvos de toque adequados e respeito às configurações de acessibilidade Android.

# 17. Memória e recursos

O Aurora-EDS deverá possuir políticas explícitas de gerenciamento de recursos:

- Evitar cópias desnecessárias.
- Liberar recursos de sessões encerradas.
- Limitar caches e buffers.
- Evitar manter arquivos desnecessariamente na memória.
- Suspender módulos inativos quando possível.
- Monitorar consumo e vazamentos.
- Administrar recursos gráficos.

O sistema deverá reagir à pressão de memória do Android, reduzindo caches, suspendendo tarefas não essenciais, liberando recursos temporários e persistindo estado recuperável. Componentes não críticos poderão ser encerrados quando necessário.

# 18. Concorrência

O núcleo deverá possuir thread principal, threads de processamento, filas de tarefas, operações assíncronas, sincronização, cancelamento, prioridades e limites de concorrência.

A thread da interface nunca deverá executar operações longas. A implementação deverá prevenir deadlocks, starvation e bloqueios circulares. A quantidade de threads deverá considerar os recursos disponíveis no dispositivo.

# 19. Segurança

A segurança será uma propriedade arquitetural.

## 19.1. Permissões

Módulos deverão declarar permissões, como leitura e escrita de arquivos, execução de processos, rede, armazenamento, acesso a dispositivos e instalação de extensões.

## 19.2. Isolamento

O sistema deverá separar núcleo, interface, extensões, ferramentas, processos externos e projetos. Executar código de um projeto não deverá conceder automaticamente acesso aos dados internos da EDS.

## 19.3. Integridade e auditoria

Extensões, dependências, artefatos, atualizações e pacotes deverão ter verificações de integridade. Operações sensíveis deverão produzir registros auditáveis.

# 20. Controle de versão

O sistema deverá integrar Git, incluindo inicialização, clonagem, commit, branches, merge, pull, push, diff, histórico, staging, resolução de conflitos, arquivos ignorados e autenticação.

A integração deverá utilizar ferramentas ou bibliotecas adequadas ao ambiente e não deverá obrigar o usuário a utilizar um único provedor.

# 21. Testes

O Test Manager deverá descobrir, organizar e executar testes, capturar resultados, exibir falhas, registrar duração, executar testes paralelos e integrar ferramentas externas.

Categorias obrigatórias da infraestrutura:

- Testes unitários.
- Testes de integração.
- Testes funcionais.
- Testes de interface.
- Testes de desempenho.
- Testes de regressão.

A infraestrutura deverá permitir testar o próprio Aurora-EDS.

# 22. Observabilidade e diagnósticos

O sistema deverá expor métricas internas:

- Uso de memória e CPU.
- Tempo de inicialização e resposta.
- Duração de builds.
- Quantidade de tarefas e processos.
- Tempo de renderização.
- Falhas e consumo de caches.

Diagnósticos deverão estar disponíveis por interface própria e APIs internas. Logs terão níveis, categorias, timestamps e identificadores de origem.

# 23. Atualizações

O Aurora-EDS deverá possuir sistema de atualização modular, com verificação de versão, download, verificação de integridade, instalação, recuperação de falhas, compatibilidade e histórico.

Atualizações de extensões deverão ser independentes das atualizações do núcleo. Assinaturas e integridade de pacotes deverão ser validadas quando aplicável.

# 24. Configurações

O Configuration Manager administrará configurações globais, por projeto, workspace e módulo, além de preferências de interface, editor, terminal, build e ferramentas.

Deverá existir hierarquia de precedência documentada entre configurações globais, do workspace e do projeto.

# 25. Persistência

O Aurora-EDS deverá utilizar mecanismos de persistência adequados a cada categoria:

- Configurações.
- Metadados.
- Estado de sessão.
- Histórico.
- Índices.
- Cache.
- Dados de extensões.
- Registros de execução.

A persistência deverá ser transacional quando necessário e permitir recuperação após encerramentos inesperados.

# 26. Arquitetura de módulos

Cada módulo deverá declarar identidade, versão, responsabilidades, dependências, APIs públicas, eventos, recursos, permissões e ciclo de vida.

Módulos não poderão acessar estruturas internas de outros módulos sem API autorizada. O núcleo controlará carregamento, descarregamento e dependências.

# 27. Interoperabilidade

O Aurora-EDS deverá integrar compiladores externos, interpretadores, ferramentas de linha de comando, sistemas de build, servidores de linguagem, depuradores, gerenciadores de dependências e serviços remotos.

As integrações ocorrerão por adaptadores. O núcleo não deverá possuir dependências rígidas de ferramentas específicas.

# 28. Migração para Nebula

A migração será progressiva e não poderá depender de substituição abrupta de Rust e TypeScript.

## 28.1. Geração inicial

- Núcleo em Rust.
- Interface em TypeScript.
- Runtime Hermes.
- Bridge independente.
- Contratos documentados e versionados.

## 28.2. Geração intermediária

- Implementar suporte Nebula necessário ao projeto.
- Implementar bindings e interoperabilidade.
- Integrar Nebula ao núcleo e ao UI Engine.
- Migrar módulos independentes.
- Executar testes de equivalência entre implementações.

## 28.3. Geração de destino

Substituir progressivamente as implementações próprias em Rust e TypeScript por implementações Nebula, mantendo os contratos estáveis.

Antes de migrar um componente, Nebula deverá oferecer suporte comprovado às capacidades exigidas por ele: compilação Android, memória, concorrência, operações assíncronas, módulos, interoperabilidade nativa e integração gráfica.

A meta de utilizar Nebula no código próprio não elimina a necessidade de interoperabilidade com APIs Android, bibliotecas nativas e ferramentas externas.

# 29. Build e distribuição

O próprio Aurora-EDS deverá possuir processo de build reproduzível, contemplando:

- Compilação Rust.
- Transpilação TypeScript.
- Empacotamento Hermes.
- Integração Android NDK e SDK.
- Geração de APK e AAB.
- Assinatura e verificação de artefatos.
- Builds de desenvolvimento e produção.

O pipeline deverá permitir builds incrementais e automatizados.

# 30. Requisitos de qualidade

## 30.1. Desempenho

- Nenhuma operação pesada na thread da interface.
- Atualizações incrementais de componentes.
- Processamento assíncrono.
- Cache controlado.
- Paralelismo com limites.
- Redução de cópias entre linguagens.
- Renderização independente do processamento de negócio.

## 30.2. Confiabilidade

- Recuperação de sessões.
- Tratamento e isolamento de falhas.
- Logs estruturados.
- Persistência segura.
- Testes automatizados.
- Verificação de integridade.

## 30.3. Manutenibilidade

- APIs documentadas.
- Módulos independentes.
- Contratos versionados.
- Testes por módulo.
- Separação entre implementação e interface pública.
- Ausência de dependências circulares.

## 30.4. Portabilidade

O núcleo deverá evitar dependências desnecessárias do Android. APIs específicas da plataforma deverão permanecer em adaptadores.

# 31. Estrutura oficial do repositório

Estrutura arquitetural pretendida:

```text
Aurora-EDS/
├── docs/
│   ├── SPECIFICATION.md
│   ├── ARCHITECTURE.md
│   ├── CORE.md
│   ├── RUNTIME.md
│   ├── UI-ENGINE.md
│   ├── RENDERER.md
│   ├── COMMUNICATION.md
│   ├── EDITOR.md
│   ├── ZEUS.md
│   ├── PROJECT-MANAGER.md
│   ├── FILE-SYSTEM.md
│   ├── BUILD-SYSTEM.md
│   ├── LANGUAGE-SYSTEM.md
│   ├── DEBUGGER.md
│   ├── EXTENSIONS.md
│   ├── SECURITY.md
│   ├── MEMORY.md
│   ├── TESTING.md
│   ├── NEBULA-MIGRATION.md
│   └── ROADMAP.md
├── core/
├── runtime/
├── frontend/
├── ui-engine/
├── native/
├── zeus/
├── modules/
├── tests/
├── tools/
├── scripts/
└── README.md
```

Essa é a estrutura pretendida. Os diretórios e arquivos deverão ser criados conforme os módulos forem implementados; sua listagem não significa que já estejam presentes no repositório.

# 32. Fases de desenvolvimento

## Fase 0 — Fundação documental

- Especificação.
- Arquitetura.
- Contratos.
- Convenções.
- Estrutura de módulos.
- Estratégia de testes.

## Fase 1 — Núcleo

- Inicialização.
- Aurora Core.
- Event Bus.
- Task Manager.
- Persistência.
- Bridge.
- Integração Android.

## Fase 2 — UI Engine

- Runtime Hermes.
- Carregamento TypeScript.
- Árvore de componentes.
- Layout Engine.
- Renderizador.
- Eventos.
- Animações.

## Fase 3 — Infraestrutura de desenvolvimento

- File System Manager.
- Project Manager.
- Workspace.
- Editor inicial.
- Zeus.
- Configuration Manager.

## Fase 4 — Ferramentas profissionais

- Build System.
- Language Services.
- Diagnósticos.
- Autocompletar.
- Git.
- Depurador.
- Dependências.
- Testes.

## Fase 5 — Extensibilidade

- Sistema de extensões.
- APIs públicas.
- Permissões.
- Isolamento.
- Adaptadores.
- Integrações externas.

## Fase 6 — Otimização

- Profiling.
- Otimização de memória.
- Otimização de renderização.
- Builds incrementais.
- Redução do tempo de inicialização.
- Testes em diferentes dispositivos.

## Fase 7 — Nebula

- Compilação Nebula para Android.
- Bindings.
- Migração do núcleo.
- Migração da interface.
- Migração dos módulos.
- Remoção gradual das implementações próprias em Rust e TypeScript.

# 33. Critérios de conclusão

Um módulo somente será considerado concluído quando:

1. Sua responsabilidade estiver definida.
2. Sua API estiver documentada.
3. Sua implementação estiver funcional.
4. Seus testes unitários estiverem aprovados.
5. Seus testes de integração estiverem aprovados quando aplicáveis.
6. Os erros estiverem tratados.
7. O gerenciamento de recursos estiver implementado.
8. A integração com os demais módulos estiver validada.
9. Seu comportamento estiver documentado.
10. Não houver dependências arquiteturais não justificadas.

Um módulo não será considerado concluído apenas porque sua interface visual está pronta.

# 34. Diretriz arquitetural definitiva

O Aurora-EDS será construído como uma plataforma de desenvolvimento modular, nativa e independente de linguagem.

Rust e TypeScript serão tecnologias de implementação da primeira geração. Nebula será a linguagem de destino do código próprio da plataforma. Zeus será o terminal oficial. Aurora Core será responsável pelo processamento e coordenação dos subsistemas. UI Engine será responsável pela apresentação nativa.

Os módulos funcionais deverão ser independentes e comunicar-se por contratos documentados. Nenhum subsistema deverá depender de detalhes internos de outro quando uma API estável puder ser utilizada.

A arquitetura deverá permitir que o Aurora-EDS evolua sem perder compatibilidade interna, sem depender de tecnologias de navegador e sem ficar limitado a um único ecossistema de desenvolvimento.

---

**Fim da especificação arquitetural 1.0.0.**
