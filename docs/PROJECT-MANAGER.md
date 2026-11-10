# Project Manager e Workspaces

## Objetivo
Gerenciar projetos e sessões sem impor estrutura universal a todos os ecossistemas.

## Projeto
Um projeto possui identidade estável, nome, localização, metadados, linguagens detectadas, ferramentas, dependências e configurações. Detecção é baseada em arquivos e adaptadores; não executar scripts automaticamente durante a abertura.

## Workspace
Representa uma sessão de trabalho e pode conter vários projetos, arquivos abertos, terminais, painéis, layout, tarefas e estado de navegação. Deve ser possível salvar, restaurar, duplicar e fechar workspaces.

## Operações
Criar, abrir, fechar, importar, exportar, renomear e remover projetos. Operações destrutivas exigem confirmação e apresentam escopo. Importação valida caminhos, tamanho, arquivos especiais e conflitos.

## Configuração
Precedência: padrões do produto, configuração global, workspace, projeto e configuração temporária de sessão. A regra é aplicada por chave e documentada. Segredos não são armazenados em texto simples.

## Recuperação
Estado de sessão é persistido por checkpoints. Após encerramento inesperado, oferecer restauração sem sobrescrever arquivos sem consentimento.

## Aceite
Testar múltiplos projetos, caminhos indisponíveis, importação malformada, conflito de configuração, restauração, permissões Android e encerramento inesperado.
