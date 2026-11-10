# Runtime de interface

## Objetivo
A primeira geração executará frontend TypeScript após transpilação para JavaScript, utilizando Hermes. TypeScript não é executado diretamente pelo Android. Hermes é runtime JavaScript, não renderizador gráfico.

O runtime permanece atrás de uma interface Aurora Runtime para permitir substituição sem alterar módulos de produto.

## Pipeline
1. Fontes TypeScript.
2. Verificação de tipos e transpilação.
3. Bundling e resolução de módulos.
4. Validação de metadados e permissões.
5. Geração/empacotamento de bytecode quando suportado.
6. Carregamento no runtime.
7. Registro de módulos e conexão com UI Engine e serviços permitidos.

Builds de produção identificam versão do runtime, configuração e hash do bundle.

## Limites
Runtime é responsável por apresentação, estado visual, composição e interações. Filesystem, processos, rede privilegiada e gerenciamento de projetos são serviços do Core, acessados por APIs explícitas.

Código de UI não bloqueia thread de renderização. Tarefas pesadas são delegadas a serviços ou workers, com cancelamento e limites.

## Bridge
Objetos nativos não são expostos sem controle ao JavaScript. A bridge oferece handles opacos, métodos tipados, ciclo de vida definido e conversão explícita de erros. Referências JS não podem impedir indefinidamente a liberação de recursos nativos.

Transferências grandes usam buffers ou handles com propriedade clara.

## Erros e recuperação
Exceções JS são capturadas na fronteira do módulo e registradas como diagnósticos. Módulo visual com falha pode ser recarregado quando seguro, sem reiniciar serviços críticos.

## Segurança e aceite
Bundles declaram capacidades; runtime não concede acesso ao sistema por padrão. Validar carregamento, módulos, erros, limites de memória, latência da bridge e recuperação. Hermes será mantido se benchmarks em aparelhos-alvo demonstrarem compatibilidade e consumo aceitável.
