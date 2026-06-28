# E-commerce Diagramas

Repositorio de apoio para o artigo e para a geracao do sistema a partir dos requisitos do e-commerce.

## Estrutura

- `diagrams/artigo/`: diagrama limpo para o texto do artigo.
- `diagrams/ia/`: diagrama completo para enviar a IA.
- `docs/requisitos/`: PDF com os requisitos base.
- `docs/texto/`: descricao textual complementar usada junto com os diagramas.
- `docs/publish-github.md`: comando para publicar o repositorio quando o `gh` estiver autenticado.
- `archive/`: versoes antigas ou de apoio.

## Arquivos principais

- `diagrams/artigo/diagrama-classes-ecommerce-limpo.puml`
- `diagrams/artigo/diagrama_classes_ecommerce_limpo.png`
- `diagrams/ia/diagrama-classes-ecommerce-ia.puml`
- `diagrams/ia/diagrama_classes_ecommerce_ia.png`
- `diagrams/ia/diagrama-servicos-ecommerce-ia.puml`
- `diagrams/ia/diagrama_servicos_ecommerce_ia.png`
- `docs/texto/descricao-diagrama-ecommerce-ia.md`
- `docs/requisitos/requisitos-ecommerce.pdf`

## Como renderizar

Se o `plantuml` estiver instalado:

```bash
JAVA_TOOL_OPTIONS=-Djava.awt.headless=true plantuml diagrams/artigo/diagrama-classes-ecommerce-limpo.puml
JAVA_TOOL_OPTIONS=-Djava.awt.headless=true plantuml diagrams/ia/diagrama-classes-ecommerce-ia.puml
JAVA_TOOL_OPTIONS=-Djava.awt.headless=true plantuml diagrams/ia/diagrama-servicos-ecommerce-ia.puml
```

## Observacoes

- A versao do artigo deve permanecer limpa e legivel.
- A versao para IA inclui metodos, regras e servicos de aplicacao.
- O repositorio pode ser usado como base compartilhada ate o projeto final do Overleaf ficar pronto.
