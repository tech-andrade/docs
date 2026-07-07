# Documentação Delfinance — Nova versão

**Para:** Time de Produto  
**Assunto:** Nova documentação para desenvolvedores — o que mudou e por que importa

---

## Contexto

A documentação técnica da Delfinance passou por uma reformulação. O objetivo principal foi reduzir o tempo entre o desenvolvedor chegar na doc e fazer a primeira chamada de API com sucesso. Isso impacta diretamente a taxa de ativação de novas integrações.

As mudanças cobrem três frentes: **estrutura e navegação**, **conteúdo por produto** e **recursos orientados para IA**.

---

## O que mudou na estrutura

### Navegação por produto no header

Os três produtos principais agora têm abas próprias no topo da documentação: **Pix**, **Boleto** e **Webhooks**. Cada aba abre uma página de apresentação do produto — não uma lista de endpoints, mas uma visão de negócio com capacidades, casos de uso, fluxos e atalhos para a integração.

> 📸 **Sugestão de imagem:** Screenshot do header da documentação mostrando as abas Pix, Boleto e Webhooks, com a aba Pix ativa e a página de produto aberta abaixo.

---

### Menu lateral reorganizado

A navegação lateral (`Como integrar`) segue agora o fluxo natural do desenvolvedor:

1. **Introdução** — primeiros passos, idempotência, ida para produção
2. **Autenticação** — API Key, mTLS, filtros de IP
3. **Receber via Pix** — todos os modelos de QR Code + devolução + simulação
4. **Pagar via Pix** — por chave, por QR Code, por dados bancários
5. **Cobranças via Boleto** — emissão, consulta, gerenciamento, simulação
6. **Webhooks** — eventos Pix, Boleto, MEDs

Antes, a estrutura misturava conceitos e deixava o desenvolvedor sem um ponto de entrada claro.

---

## Pix

A página de Pix (`/guias/pix`) foi reformulada como uma página de produto. Ela mostra o que o produto entrega, quem usa e como começar — sem precisar navegar pelo menu lateral para entender o escopo.

**Capacidades documentadas:**
- QR Code Estático (reutilizável, valor livre ou fixo)
- QR Code Dinâmico (uso único, com expiração — ideal para checkout)
- QR Code com Vencimento (juros, multa, desconto — substituto de boleto)
- Pagar por Chave Pix
- Pagar por QR Code
- Devoluções

> 📸 **Sugestão de imagem:** Screenshot da seção "O que você pode fazer" na página do Pix, mostrando os 6 cards de capacidade com os ícones e descrições.

**Casos de uso presentes na doc:**
SaaS, Gateway de Pagamento, Marketplace, Software House, Automação Financeira, ERPs e Sistemas de Gestão.

> 📸 **Sugestão de imagem:** Screenshot da seção de casos de uso com os 6 blocos de nicho — bom para mostrar que a doc já fala a linguagem do segmento do cliente.

**Fluxos visuais:**  
Dois diagramas de sequência cobrem o fluxo de recebimento (criar QR Code → exibir → pagar → webhook) e o fluxo de envio (validar chave no DICT → inicializar → liquidar → confirmar via webhook).

> 📸 **Sugestão de imagem:** Screenshot de um dos fluxos sequenciais (mermaid diagram) mostrando os participantes: Você, API, Pagador, Webhook.

---

## Boleto

A página de Boleto (`/guias/boleto`) segue o mesmo padrão da página de Pix. Cobre o produto boleto híbrido (Boleto + Pix) e todos os fluxos relacionados.

**Capacidades documentadas:**
- Emissão de Boleto Híbrido (BANKSLIP_PIX)
- Encargos, juros e descontos
- Consulta e conciliação
- Atualização de vencimento
- Download do PDF
- Simulação de pagamento (sandbox)

> 📸 **Sugestão de imagem:** Screenshot da hero section da página de Boleto, mostrando o card de código com o payload de exemplo (`"type": "BANKSLIP_PIX"`, `"status": "pending"`).

**Casos de uso presentes na doc:**
Cobranças B2B, Educação, Saúde e Clínicas, Imobiliárias, E-commerce, ERPs e Sistemas de Gestão.

A documentação técnica de boleto cobre: emissão, consulta, atualização de vencimento, cancelamento, download do PDF e simulação no sandbox — tudo com exemplos de request e response.

---

## Webhooks

A página de Webhooks (`/guias/webhooks`) trata o tema como produto, não como configuração secundária. Webhooks são o mecanismo que elimina polling e garante que o sistema do cliente reaja a pagamentos em tempo real.

**O que está documentado:**
- Todos os 10 tipos de evento com descrição e payload de exemplo:
  - `PIX_RECEIVED`, `PIX_REFUNDED`, `PIX_TRANSFERRED`, `PIX_TRANSFER_FAILED`
  - `CHARGE_PAID`, `CHARGE_OVERDUE`, `CHARGE_CANCELLED`
  - `MED_REQUESTED`, `MED_ACCEPTED`, `MED_REJECTED`
- Esquemas de autenticação do webhook: `NONE`, `BASIC`, `BEARER`, `HEADER`
- Retentativas automáticas
- Gestão via API (cadastrar, listar, remover)

> 📸 **Sugestão de imagem:** Screenshot da seção de tipos de evento — a tabela ou os cards listando os 10 event types com descrição.

A API Reference de webhooks foi corrigida e cobre os três endpoints reais:
- `POST /baas/api/v1/webhooks` — cadastrar
- `GET /baas/api/v1/webhooks` — listar
- `DELETE /baas/api/v1/webhooks/:id` — remover

---

## SDKs

A documentação inclui uma página de SDKs (`/iniciacao/sdks`) que lista as bibliotecas disponíveis para acelerar a integração. Para desenvolvedores que preferem não montar as requisições na mão, as SDKs abstraem autenticação, serialização e tratamento de erros.

> 📸 **Sugestão de imagem:** Screenshot da página de SDKs mostrando as linguagens disponíveis (cards com logo de cada stack).

---

## Documentação orientada para IA

Essa é a parte mais diferencial da nova versão. A documentação foi pensada para ser consumida por assistentes de IA — tanto pelos desenvolvedores que usam ferramentas como Cursor, Copilot e Claude, quanto por quem quer gerar código ou entender a API com ajuda de IA.

### llms.txt e llms-full.txt

Seguindo o padrão [llms.txt](https://llmstxt.org), a documentação disponibiliza dois arquivos otimizados para LLMs:

| Arquivo | Conteúdo | Indicado para |
|---|---|---|
| `llms.txt` | Índice com links para todas as páginas | Assistentes que navegam a doc em tempo real (Cursor, Copilot) |
| `llms-full.txt` | API reference completa em texto puro | Cole direto no contexto do ChatGPT, Claude ou qualquer LLM |

O `llms-full.txt` contém todos os endpoints, parâmetros, exemplos de request/response, tipos de evento e boas práticas — pronto para ser colado como contexto em qualquer conversa com IA.

> 📸 **Sugestão de imagem:** Screenshot do modal "Baixar contexto para IA" na documentação, mostrando as duas opções (llms.txt e llms-full.txt) com os badges "Resumido" e "Completo".

### Assistente de Integração

O `/guias/assistente-integracao` é um wizard guiado que funciona como um chat dentro da própria documentação. O desenvolvedor responde 4 perguntas e recebe um plano de integração personalizado + um prompt completo para usar com qualquer LLM.

**Fluxo do assistente:**
1. Qual produto integrar? (Receber via Pix / Pagar via Pix / Boleto / Webhooks / Ir para produção)
2. Onde a integração vai rodar? (E-commerce / SaaS / Gateway / Marketplace / Software House / ERP)
3. Qual tecnologia de backend? (Node.js / C# / PHP / Python / Java)
4. Já tem API Key sandbox?

**O que o assistente gera:**
- Fluxo sugerido (passos adaptados ao produto e à situação do dev)
- Links diretos para os guias relevantes
- Botões para baixar `llms.txt` e `llms-full.txt`
- Prompt estruturado com: **Papel**, **Contexto**, **Regras**, **Endpoints relevantes** e **O que preciso** — tudo adaptado ao produto e nicho escolhido

> 📸 **Sugestão de imagem:** Screenshot do assistente com a conversa em andamento — um desenvolvedor tendo respondido as 4 perguntas e o card de resultado aberto mostrando o fluxo sugerido e o prompt gerado.

> 📸 **Sugestão de imagem:** Screenshot do prompt gerado em destaque — mostrando as seções "## Papel", "## Contexto", "## Endpoints relevantes" no card escuro ao final do assistente.

---

## Resumo das melhorias

| Área | Antes | Agora |
|---|---|---|
| Navegação por produto | Sem destaque no header | Abas Pix, Boleto e Webhooks |
| Páginas de produto | Listagens técnicas | Páginas de apresentação com capacidades e casos de uso |
| Tipos de evento webhook | Inconsistentes e incorretos | 10 event types padronizados em SCREAMING_SNAKE_CASE |
| API Reference de webhooks | Endpoints e campos incorretos | Corrigida e validada |
| Fluxos de integração | Apenas texto | Diagramas de sequência (Pix receber e pagar) |
| Documentação para IA | Não existia | llms.txt + llms-full.txt + Assistente de Integração |
| Ponto de entrada para IA | Não existia | Modal "Contexto para IA" em páginas de produto |

---

## Links úteis

- Documentação: `https://docs.delfinance.com.br`
- Página do Pix: `/guias/pix`
- Página do Boleto: `/guias/boleto`
- Página de Webhooks: `/guias/webhooks`
- Assistente de Integração: `/guias/assistente-integracao`
- Contexto para IA (llms.txt): `/llms.txt`
- Contexto para IA (completo): `/llms-full.txt`

---

*Documentação mantida pelo time de Engenharia. Dúvidas ou sugestões: abra uma issue no repositório.*
