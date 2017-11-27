---
title: Cartão de Crédito
position: 1
menu: gateway
---

Nas transações que utilizam o pagamento via **Cartão de Crédito**,  você utilizará na nossa API de Transação o método **Criar Transação**, adicionando ao nó `payment` os parâmetros `method`, `processor` e também adicionar o nó `card` que contem os parâmetros do cartão de crédito, veja abaixo os dados necessários para envio:

| Dados de Entrada                              |  Obrig.  | Formato   | Descrição                              |
|-----------------------------------------------|----------|-----------|----------------------------------------|
| transaction[payment][processor]               | Sim      |  Texto    |  Processador do pagamento              |
| transaction[payment][method]                  | Sim      |  Texto    |  Meio de pagamento                     |
| transaction[payment][card][reference]         | Sim      |  Texto    |  Referência do cartão <sup>1</sup>     |
| transaction[payment][card][holder_name]       | Sim      |  Texto    |  Nome impresso no cartão               |
| transaction[payment][card][number]            | Sim      |  Texto    |  Número do cartão                      |
| transaction[payment][card][cvv]               | Sim      |  Texto    |  Código de segurança do cartão         |
| transaction[payment][card][expiration][month] | Sim      |  Texto    |  Mês de vencimento do cartão (mm)      |
| transaction[payment][card][expiration][year]  | Sim      |  Texto    |  Ano de vencimento do cartão (YYYY)    |


<sup>1</sup> Quando você **Cria uma Transação**, a nossa API retorna o `reference`, que é o código de referência do cartão de crédito em nossa base, nas proximas transações você pode utilizar como forma para identificar os dados do pagamento. 
{: .infoRedirect }


Os parâmetros `method` e `processor` são **OBRIGATÓRIOS**.
{: .error }

Ao informar que a forma de pagamento é **Cartão de Crédito**, os campos `holder_name`, `number`, `cvv`, `expiration[month]` e `expiration[year]` se tornão campos **OBRIGATÓRIOS**.
{: .warning }



Para saber mais sobre o método de **Criar Transação**, <a href="/gateway/criar-transacao/#criar-transacao" target="_blank" class="linkPadraoVerde">clique aqui</a>.