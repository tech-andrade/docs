> **First-time setup**: Customize this file for your project. Prompt the user to customize this file for their project.
> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP

## Terminology

{/* Add product-specific terms and preferred usage */}
{/* Example: Use "workspace" not "project", "member" not "user" */}

### Split de Pagamentos

Definição oficial em `guias/split-pagamentos/visao-geral.mdx` (seção "Conceitos"). Use os mesmos termos em docs, discussões de fluxo de negócio e specs.

- **Conta de recebimento**: conta Delfinance que recebe o pagamento original e de onde saem os repasses. Não use "conta de origem", "conta pagadora", "conta principal" ou "sua conta". Placeholder em exemplos: `CONTA_DE_RECEBIMENTO`.
- **Beneficiário**: pessoa ou empresa que recebe uma parte do pagamento (vendedor, parceiro, afiliado).
- **Conta do beneficiário**: conta para onde o repasse vai. Não use "conta de destino" nem "conta beneficiária". Placeholder: `CONTA_DO_BENEFICIARIO`.
- **Instrução**: a regra de um repasse (`amount`, `type`, `transferType`, `beneficiary`).
- **Repasse**: a transferência efetiva da conta de recebimento para a conta do beneficiário.
- **Split padrão da conta**: configuração em `/split-payments/configurations`, aplicada a todo Pix recebido na conta. Não use "split por conta".
- **Split por cobrança**: `splitPayment` informado na criação do QR Code dinâmico; substitui o split padrão para aquela cobrança.
- Tipos de conta do beneficiário aceitos para Pix: apenas `PAYMENT`, `CURRENT` e `SAVING` (`SALARY` não é aceito pelo Pix).

## Style preferences

{/* Add any project-specific style rules below */}

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references
- Listagens paginadas da API retornam o próprio array no corpo, sem wrapper (`items`, `data` etc.). A paginação vem no header `Pagination` (JSON com `currentPage`, `pageSize`, `pageCount`, `rowCount` e, opcionalmente, `totalAmount`), e os query params são `page` e `limit`. Documente numa seção "Paginação", como em `guias/boleto/consultar-pagamento.mdx`.
- Escreva valores em reais no texto como `R\$ 200,00`. Dois `$` no mesmo parágrafo viram fórmula LaTeX no Mintlify. Dentro de blocos de código e diagramas Mermaid, use `R$` sem escape.

## Content boundaries

{/* Define what should and shouldn't be documented */}
{/* Example: Don't document internal admin features */}
