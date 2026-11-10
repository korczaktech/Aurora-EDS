# Sistema de linguagens e Language Services

## Objetivo
Oferecer suporte linguístico desacoplado do editor e do compilador. Uma linguagem pode ter destaque e edição básica sem análise semântica ou compilador integrado.

## Manifesto
Cada pacote declara ID, versão, extensões, nomes de arquivo, gramática, tokenizer, parser opcional, serviços disponíveis, comandos de build e dependências.

## Níveis de suporte
1. Identificação de arquivo.
2. Destaque lexical.
3. Parsing e estrutura.
4. Diagnósticos sintáticos.
5. Análise semântica.
6. Autocompletar, hover, definições e referências.
7. Formatação e ações de código.
8. Build, execução e depuração.

A interface indica níveis disponíveis sem sugerir suporte completo quando houver somente destaque.

## Protocolo interno
Definir initialize/capabilities, open/change/close document, diagnostics, completion, hover, definition, references, symbols, formatting, rename, cancellation e shutdown. Toda mensagem de documento inclui URI e versão. Respostas atrasadas de versões antigas são descartadas.

## Incrementalidade e LSP
Parsing e análise trabalham com snapshots e invalidam somente regiões afetadas quando possível. Serviços não bloqueiam digitação. LSP será suportado por adaptador, não como dependência obrigatória do núcleo.

## Segurança e aceite
Servidores e plugins são executáveis potencialmente não confiáveis. Exigem permissões, limites de recursos, diretório controlado e política de rede. Testar documentos grandes, mudanças rápidas, respostas fora de ordem, cancelamento, Unicode e falhas do servidor.
