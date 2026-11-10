# Segurança

## Princípios
Privilégio mínimo, consentimento explícito, isolamento, validação de entradas, proteção de segredos, auditabilidade e falha segura.

## Fronteiras de confiança
Separar Core, frontend, módulos internos, extensões, projetos do usuário, ferramentas externas e serviços remotos. Código de projeto não é confiável por padrão. Abrir projeto não executa scripts automaticamente.

## Permissões
Capacidades são específicas: filesystem por escopo, execução de processos, rede, dispositivos, instalação de extensão e acesso a dados sensíveis. Permissões possuem finalidade, origem, duração e possibilidade de revogação.

## Processos e terminal
Comandos destrutivos, scripts e executáveis externos respeitam política de execução. Variáveis de ambiente e argumentos não são montados por concatenação insegura. Segredos não entram em histórico ou logs.

## Armazenamento e rede
Usar APIs Android de armazenamento e permissões. Validar certificados e integridade de pacotes. Tokens devem ser armazenados em mecanismo seguro da plataforma quando disponível, nunca em texto simples no repositório ou logs.

## Atualizações e extensões
Verificar hash e assinatura quando aplicável. Atualização deve ser atômica quando o mecanismo permitir e possuir rollback. Extensões declaram permissões antes da ativação.

## Auditoria e validação
Registrar operações sensíveis sem coletar conteúdo privado desnecessário. Logs evitam tokens, senhas, chaves e conteúdo de arquivos. Aplicar threat modeling, testes de permissões, fuzzing de parsers/protocolos, análise de dependências e testes de traversal.
