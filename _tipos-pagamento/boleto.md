---
title: Boleto
position: 2
menu: gateway
---

Nas transações que utilizam o pagamento via **Boleto**,  você utilizará na nossa API de Transação o método **Criar Transação** adicionando ao nó `payment` os parâmetros `method`, `processor` e também adicionar o nó `billet` que contem os parâmetros do boleto, veja abaixo os dados necessários para envio:

| Dados de Entrada                              |  Obrig.  | Formato   | Descrição                                   |
|-----------------------------------------------|----------|-----------|---------------------------------------------|
| transaction[payment][processor]               | Sim      |  Texto    |  Processador do pagamento                   |
| transaction[payment][method]                  | Sim      |  Texto    |  Meio de pagamento                          |
| transaction[payment][billet][due_date]	    | Sim      |  Texto    |  Data de vencimento do boleto<sup>1</sup>   |
| transaction[payment][billet][observations][]	| Sim      |  Texto    |  Observações do boleto<sup>1</sup>          |



<sup>1</sup> Ao informar que a forma de pagamento é **Boleto**, os campos `due_date` e `observations` são para facilitar a transação via boleto. Não são campos obrigatórios.
{: .infoRedirect }

Os parâmetros `method` e `processor` são **obrigatórios**.
{: .error }


Para saber mais sobre o método de **Criar Transação**, <a href="/gateway/criar-transacao/#criar-transacao" target="_blank" class="linkPadraoVerde">clique aqui</a>.
