# Documentação da Delfinance

Este repositório contém a documentação oficial da Delfinance em formato Mintlify.

## Estrutura do projeto

- [docs.json](docs.json): configuração principal do tema, navegação e metadados.
- [index.mdx](index.mdx): página inicial da documentação.
- [iniciacao](iniciacao): conteúdos de introdução, autenticação, ambientes e segurança.
- [api-reference](api-reference): referência técnica dos endpoints.

## Como visualizar localmente

Instale a CLI do Mintlify:

```bash
npm i -g mint
```

Na raiz do projeto, execute:

```bash
mint dev
```

A pré-visualização fica disponível em http://localhost:3000.

## Boas práticas para editar

- mantenha os textos em português;
- use frontmatter com `title` e `description` em todas as páginas;
- prefira links internos para páginas da documentação;
- teste a navegação após alterar a estrutura de páginas ou menus.

