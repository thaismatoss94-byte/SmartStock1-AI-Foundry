# SmartStock1-AI-Foundry
Agente SmartStock desenvolvido no Azure AI Foundry para Challenge.

## 1. Visão geral do projeto
O **SmartStock** é um agente simples criado no **Azure AI Foundry** para ajudar um mini mercado a acompanhar a validade dos produtos.  
Ele não usa banco de dados nem integração complexa. Toda a lógica fica dentro do próprio agente, em uma lista de produtos de exemplo.

Esse formato foi pensado para:
- Ser **fácil de configurar**;
- Atender aos **requisitos do Challenge**;
- Ser ideal para quem está tendo o **primeiro contato com o Azure**.
  
  
  [Tela inicial do meu agente](Prints/2025-11-19 (15).png)


## 2. Objetivo do agente
O objetivo do SmartStock é:
- Listar produtos que estão **próximos do vencimento**, de acordo com um número de dias informado pelo usuário.

  
[Tela com Prompts de descrição do agente 1](Prints/2025-11-19 (16).png)
[Tela com Prompts de descrição do agente 2](Prints/2025-11-19 (17).png)
[Tela com Prompts de descrição do agente 3](Prints/2025-11-19 (18).png)
[Tela com Prompts de descrição do agente 4](Prints/2025-11-19 (19).png)

Exemplo de cenário:
> “Quais produtos vencem em até 10 dias?”

O agente devolve uma lista com esses produtos.

## 3. Como o agente funciona (lógica simples)
Dentro das instruções do agente (no Azure AI Foundry), é cadastrada uma **lista fixa de produtos** com um campo de “dias para vencer”. Exemplo:
- Leite Integral – vence em 07 dias  
- Queijo Minas Padrão – vence em 05 dias  
- Arroz Branco Tipo 1 – vence em 120 dias  
- Iogurte Natural – vence em 03 dias  
- Presunto – vence em 04 dias
- Feijão -  vence me 45 dias
- Sal -  vence em 280 dias
- Leite desnatado -  vence em 02 dias
- Suco integral de uva - vence em 03 dias

A lógica é simples:
1. O usuário informa um número de dias (por exemplo, 10);
2. O agente compara esse número com a lista interna;
3. O agente retorna apenas os produtos que vencem em **menor ou igual** a esses dias.

Não há banco de dados, nem API externa. Tudo é feito na conversa do agente.

[Testando ação do agente 1](Prints/2025-11-19 (20).png)
[Testando ação do agente 2](Prints/2025-11-19 (21).png)
[Testando ação do agente 3](Prints/2025-11-19 (22).png)

## 4. Ação disponível no agente
O agente possui uma ação conceitual chamada **get_expiring_products**.

### Nome da ação
`get_expiring_products`

### Parâmetro
- `days` (número inteiro): quantidade de dias para verificar a validade.

### O que a ação faz
Filtra a lista de produtos de exemplo e retorna apenas aqueles que vencem em até X dias.


### Exemplo de uso (no chat do agente)
Pergunta do usuário:
> “Liste os produtos que vencem em até 10 dias.”

Resposta esperada (exemplo):
> “Os produtos que vencem em até 10 dias são:  
> - Iogurte Natural – vence em 3 dias  
> - Presunto – vence em 4 dias  
> - Queijo Minas Padrão – vence em 5 dias  
> - Leite Integral – vence em 7 dias.”

[Resposta do agente](Prints/2025-11-19 (20).png) 

## 📌 2. Arquitetura Simplificada do Agente

```text
+----------------------+
|        Usuário       |
+----------------------+
           |
           v
Pergunta no Playground:
"Quais produtos vencem
em até X dias?"
           |
           v
+---------------------------+
|    Agente SmartStock      |
|  (Azure AI Foundry)       |
+---------------------------+
           |
           v
Lê as instruções e aplica a lógica:
- Usa a lista interna de produtos
- Compara dias informados
- Filtra produtos com vencimento <= X dias
           |
           v
+---------------------------+
|     Resposta ao usuário   |
+---------------------------+
           |
           v
Exemplo:
- Iogurte Natural – vence em 3 dias
- Presunto – vence em 4 dias
- Queijo Minas – vence em 5 dias

> ---

## 5. Estrutura do repositório no GitHub
Sugestão de estrutura:
- `README.md` → este arquivo, com a explicação do agente.
- `prints/` → pasta contendo prints de tela do Azure AI Foundry.
  - `prints/agente_criado.png`
  - `prints/teste_acao.png`
  - `prints/fluxo_execucao.png`

## 6. Prints recomendados para o Challenge
Para cumprir bem o item de documentação do Challenge, inclua no README (ou pasta `prints/`) imagens como:
1. **Tela do agente no Azure AI Foundry** (nome SmartStock visível);
2. **Tela do chat do agente** mostrando uma pergunta do tipo “produtos que vencem em até 10 dias” e a resposta;
3. (Opcional) Um pequeno **diagrama simples** mostrando:
   - Usuário → Agente SmartStock → Lista interna de produtos → Resposta.

## 7. Como esse projeto atende ao Challenge
De acordo com as regras do “Build Your First Copilot Challenge (Foundry Edition)”, este projeto atende aos requisitos mínimos porque:
- Está em um **repositório público no GitHub**;
- Possui um **README completo**, com descrição do projeto, objetivo do agente, fluxo e prints;
- Possui um **agente funcional no Azure AI Foundry**, com pelo menos **uma ação simples** (filtrar produtos por dias para o vencimento);
- A solução é **simples, clara e reproduzível**, ideal para quem está começando.

## 8. Referências
- Azure AI Foundry – Documentação oficial  
- Material do Challenge – Build Your First Copilot Challenge (Foundry Edition)
