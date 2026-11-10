# ADR-0006 — Armazenamento e acesso a projetos

- **Estado:** Aceita
- **Data:** 2026-11-10
- **Escopo:** File System Manager e Project Manager

## Contexto
Android oferece armazenamento privado do aplicativo e acesso mediado a documentos e diretórios externos. Um caminho de arquivo não implica, por si só, permissão permanente.

## Decisão
O File System Manager será a única camada de domínio autorizada a realizar operações de arquivo. Usará adaptadores para armazenamento privado e Storage Access Framework (SAF), preservando permissões concedidas pelo usuário quando o Android permitir.

Projetos manterão identificadores e referências de localização abstratas, sem assumir que todo recurso é um caminho POSIX. Operações de escrita serão transacionais quando possível, com tratamento de falhas e recuperação. Acesso externo será mediado por capacidades explícitas.

## Alternativas consideradas
- Acesso irrestrito ao filesystem: rejeitado por incompatibilidade com sandbox Android.
- Armazenar todos os projetos em diretório privado: rejeitado como única opção por limitar interoperabilidade.
- Expor caminhos físicos como contrato universal: rejeitado.

## Consequências
- Módulos não devem manipular arquivos fora do File System Manager.
- SAF pode impor diferenças de desempenho e semântica; adaptadores devem documentá-las.
- Watchers e operações atômicas dependem da origem do recurso e devem oferecer fallback.
