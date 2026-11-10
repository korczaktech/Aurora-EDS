# File System Manager

## Objetivo
Fornecer API de arquivos uniforme, segura e compatível com o modelo de armazenamento Android.

## Abstração de recursos
Arquivos são identificados por URI/Resource ID, não necessariamente por caminho POSIX. O provedor pode ser filesystem privado, SAF, volume externo ou provedor remoto. Operações declaram capacidades disponíveis; não presumir rename, seek ou acesso aleatório em todos os provedores.

## Operações
Listagem, leitura, escrita, criação, remoção, movimentação, renomeação, metadados, busca e observação de alterações. Operações em lote reportam resultados por item e permitem cancelamento quando seguro.

## Segurança
Aplicar permissões concedidas pelo Android e políticas internas por projeto. Resolver caminhos sem traversal. Links simbólicos e arquivos especiais são tratados explicitamente. Não seguir links fora da raiz autorizada sem permissão.

## Escrita segura
Quando o provedor permitir, utilizar escrita temporária seguida de substituição atômica. Em provedores sem atomicidade, documentar risco e usar backup/recuperação quando viável. Nunca afirmar atomicidade sem suporte real.

## Observação e cache
Watchers são canceláveis e consolidados para evitar tempestades de eventos. Cache possui invalidação explícita e respeita alterações externas.

## Aceite
Testar arquivos grandes, Unicode, permissões revogadas, SAF, caminhos inválidos, traversal, alterações externas, falhas de escrita e provedores sem suporte POSIX.
