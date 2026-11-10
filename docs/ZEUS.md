# Terminal Zeus

## Definição
Zeus é o terminal nativo integrado ao Aurora-EDS, inicialmente em Rust. É um ambiente de comandos e gerenciamento de processos, não apenas um painel visual.

## Componentes
- **Zeus Core:** coordena sessões, comandos e políticas.
- **Zeus Shell:** analisa e avalia a sintaxe.
- **Process Manager:** inicia, acompanha, interrompe e finaliza processos.
- **I/O Engine:** encaminha stdin, stdout e stderr.
- **History:** mantém histórico conforme política de privacidade.
- **Command Registry:** registra comandos internos e extensões autorizadas.
- **Terminal View:** apresenta saída, entrada, seleção e acessibilidade.

## Sessão
Uma sessão possui ID, diretório atual, ambiente permitido, shell selecionado, histórico, processos filhos e estado. Encerrá-la aplica política explícita aos processos filhos, sem deixar processos órfãos.

## Sintaxe e execução
O parser distingue palavras, aspas, escapes, operadores, redirecionamento e pipelines. A análise precede a execução; erros sintáticos não iniciam parcialmente uma cadeia de comandos.

Comandos internos usam APIs Aurora. Comandos externos dependem de executáveis disponíveis e permissões. Zeus não presume presença de bash, coreutils, package managers ou filesystem Linux completo no Android.

## I/O e processos
Saída é transmitida em blocos limitados, com backpressure para impedir crescimento ilimitado de memória. stdout e stderr mantêm identificação separada. Entrada interativa suporta cancelamento e encerramento.

No Android, execução está sujeita a sandbox, permissões, ABI e disponibilidade de binários. A interface comunica quando uma operação não é permitida ou disponível.

## Segurança
Comandos podem ser destrutivos. Zeus não executa comandos privilegiados sem capacidade explícita. Extensões de comando declaram permissões. Histórico pode conter dados sensíveis e deve ser local e controlável pelo usuário.

## Comandos e aceite
Comandos Aurora para projetos, build, testes, dependências, extensões, diagnósticos e processos serão registrados em catálogo versionado. Testar parser, quoting, pipelines, redirecionamento, saída grande, backpressure, cancelamento, encerramento e restrições reais Android.
