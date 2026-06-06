# Luri Financeiro 🤖

Agente de IA financeiro criado com Make, Google Sheets e Groq — sem nenhuma linha de código.

## O que é?

A Luri Financeiro é um agente conversacional que simula o que ferramentas como o Microsoft Copilot Studio fazem em grandes empresas. Ela recebe uma pergunta sobre um pedido de compra, consulta uma base de dados e responde em linguagem natural.

Projeto desenvolvido como atividade prática do curso **Copilot Studio: fundamentos e automação** da Alura, reproduzindo a lógica do agente no Make como alternativa ao Copilot Studio.

## Como funciona

Webhook → Google Sheets → Groq (Llama 3.3-70b) → Webhook Response

1. **Webhook** — recebe a pergunta do usuário em formato JSON
2. **Google Sheets** — busca o pedido na planilha pelo número informado
3. **Groq** — gera uma resposta em linguagem natural com os dados encontrados
4. **Webhook Response** — devolve a resposta para quem fez a pergunta

## Ferramentas utilizadas

- [Make](https://make.com) — plataforma de automação no-code
- [Google Sheets](https://sheets.google.com) — base de dados dos pedidos
- [Groq](https://groq.com) — modelo Llama 3.3-70b-versatile para geração de respostas
- [Hoppscotch](https://hoppscotch.io) — para testar as requisições

## Exemplo de uso

**Entrada:**
```json
{
  "pergunta": "1001"
}
```

**Resposta da Luri:**

Consegui encontrar os detalhes do seu pedido!
Aqui estão as informações do pedido 1001:

Número do pedido: 1001
Objeto: Notebook Dell
Valor unitário: R$ 3.500,00
Quantidade: 2 unidades
Valor total: R$ 7.000,00
Status: Entregue

Se você tiver alguma outra pergunta ou precisar de mais informações, sinta-se à vontade para perguntar!

## Autor

Higor Figueredo — em transição para a área de IA e tecnologia.

[LinkedIn](https://www.linkedin.com/in/seu-perfil) • [YouTube](https://www.youtube.com/@HigorFigueredo)

## Screenshots

### Cenário no Make
![Cenário no Make](Make%20-%20Luri%20Financeiro.png)

### Resposta no Hoppscotch
![Resposta no Hoppscotch](hoppscotch%20-%20Luri%20Financeiro.png)
