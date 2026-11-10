# Sistema de extensões

## Objetivo
Permitir evolução por módulos sem conceder acesso irrestrito ao núcleo.

## Tipos
Extensões podem fornecer linguagens, temas, componentes, ferramentas, compiladores, depuradores, comandos Zeus, adaptadores de build, integrações e provedores.

## Manifesto
O manifesto contém ID global, nome, versão semântica, versão mínima/máxima da API, plataforma, ponto de entrada, dependências, permissões, arquivos, assinatura e metadados do autor.

## Instalação
Validar origem, integridade, assinatura quando aplicável, compatibilidade, dependências e permissões solicitadas. Atualização preserva a versão anterior até validar a nova, permitindo rollback.

## Lifecycle
Estados: discovered, installed, verified, loaded, active, suspended, failed e disabled. Transições são explícitas e auditáveis. Extensões podem ser desativadas sem remover seus dados, conforme política do usuário.

## Isolamento e compatibilidade
Extensões operam por APIs autorizadas. Código de extensão não recebe ponteiros internos do Core. A arquitetura deve suportar execução isolada, limites de CPU/memória e permissões por capacidade. Extensões nativas confiáveis e extensões não confiáveis têm níveis distintos.

APIs públicas possuem versão. Extensões incompatíveis são bloqueadas ou executadas em modo de compatibilidade explicitamente suportado.

## Aceite
Testar instalação malformada, assinatura inválida, dependência ausente, permissão negada, falha de inicialização, atualização interrompida, rollback e remoção.
