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

[LinkedIn](https://www.linkedin.com/in/higor-figueredo-b031911a6/) • [YouTube](https://www.youtube.com/@higorfigueredo1996)

## Screenshots

### Cenário no Make
![Cenário no Make](Make%20-%20Luri%20Financeiro.png)

### Resposta no Hoppscotch
![Resposta no Hoppscotch](hoppscotch%20-%20Luri%20Financeiro.png)

## Evolução: Fluxo Conversacional com Router

Na segunda versão, o agente ganhou um fluxo conversacional com 3 etapas, simulando o comportamento do Microsoft Copilot Studio:

Webhook → Router → [3 rotas condicionais]
├── Etapa: inicio  → Webhook Response (pergunta o nome)
├── Etapa: nome    → Webhook Response (pergunta sobre o pedido)
└── Etapa: pergunta → Groq (extrai número) → Google Sheets → Groq (resposta) → Webhook Response

### Como funciona

1. **Etapa inicio** — usuário envia `{"etapa": "inicio", "mensagem": "pedido de compras"}` e a Luri se apresenta e pede o nome
2. **Etapa nome** — usuário envia seu nome e a Luri agradece e pede a pergunta
3. **Etapa pergunta** — usuário faz a pergunta, o primeiro Groq extrai o número do pedido, o Google Sheets busca os dados e o segundo Groq gera a resposta

### Screenshots da conversa

![Etapa inicio](Etapa%201%20-%20Inicio.png)
![Etapa 1 Make](Etapa%201%20(Make)%20-%20Inicio.png)
![Etapa nome](Etapa%202%20-%20Nome.png)
![Etapa 2 Make](Etapa%202%20(Make)%20-%20Nome.png)
![Etapa pergunta](Etapa%203%20-%20Pergunta.png)
![Etapa 3 Make](Etapa%203%20(Make)%20-%20Pergunta.png)

## Versão 3 — Fluxos Condicionais

Na terceira versão, o agente ganhou dois novos fluxos condicionais:

### Fluxo de Continuidade
Após responder sobre um pedido, a Luri pergunta se o usuário tem mais dúvidas:
- **Sim** → volta a perguntar sobre pedidos
- **Não** → agradece e encerra a conversa

### Fluxo de Requisição de Compra
O usuário informa o valor estimado da compra e a Luri direciona:
- **Acima de R$5.000** → orienta abrir no sistema de gestão da empresa
- **Abaixo de R$5.000** → registra no Planner para a equipe de compras

### Como testar

**Continuidade:**
```json
{"etapa": "retorno", "mensagem": "sim"}
{"etapa": "retorno", "mensagem": "não"}
```

**Requisição:**
```json
{"etapa": "requisicao", "mensagem": "8000"}
{"etapa": "requisicao", "mensagem": "2000"}
```

### Screenshots

![Cenário completo](Captura%20de%20Tela%20(1112).png)
![Teste retorno sim](Captura%20de%20Tela%20(1113).png)
![Teste retorno não](Captura%20de%20Tela%20(1114).png)
![Teste requisição acima](Captura%20de%20Tela%20(1115).png)
![Teste requisição abaixo](Captura%20de%20Tela%20(1116).png)

## Versão 4 — Geração de Escopo com IA

Na quarta versão, o fluxo de requisição de compra foi expandido com coleta de dados e geração de escopo técnico com IA.

### Fluxo completo de requisição

1. **requisicao_inicio** — apresenta o agente e pede o nome
2. **requisicao_email** — agradece pelo nome e pede o e-mail
3. **requisicao_descricao** — solicita descrição detalhada do produto ou serviço
4. **requisicao_escopo** — Groq gera o escopo técnico e direciona pelo valor:
   - **Acima de R$5.000** → orienta abrir no sistema de gestão com o escopo gerado
   - **Abaixo de R$5.000** → registra no Planner com o escopo gerado

### Screenshots

![Captura 1143](Captura%20de%20Tela%20(1143).png)
![Captura 1144](Captura%20de%20Tela%20(1144).png)
![Captura 1145](Captura%20de%20Tela%20(1145).png)
![Captura 1146](Captura%20de%20Tela%20(1146).png)
![Captura 1147](Captura%20de%20Tela%20(1147).png)
![Captura 1148](Captura%20de%20Tela%20(1148).png)
![Captura 1149](Captura%20de%20Tela%20(1149).png)
![Captura 1150](Captura%20de%20Tela%20(1150).png)
