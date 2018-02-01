---
title: Consultando Token
position: 3
menu: gateway
right_code: |
  ~~~ xml
  curl
    --request GET https://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick/1514483826864c3149224-67db-4557-8950-6a80f708c1c5
    --header "Content-Type: application/json"
    --curl -u usuario:senha
    --data-binary
  ~~~
  {: title="Exemplo criação transação" }

  ~~~ xml
  --header "Content-Type: application/json
    { 
    "codigoEstabelecimento": 1000000000000,
    "codigoFormaPagamento": 170,
    "oneClick": 1,
    "token": "1514483826864c3149224-67db-4557-8950-6a80f708c1c5",
    "nomeTitularCartaoCredito": "Teste OneClick",
    "numeroCartaoCredito": "000000******0002",
    "dataValidadeCartao": "10/2021",
    "emailComprador": "yapay@yapay.com.br"
    }

  ~~~
  {: title="Exemplo retorno transação" }

---

Funcionalidade disponível para visualizar os dados cadastrados em um Token.



 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `ttps://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick/<<`token`>>`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://gateway.yapay.com.br/checkout/api/v3/oneclick/<<`token`>>`
{: .informativoVermelho }


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para consultas, acione o método <span class="get">GET</span>.
{: .informativo }


**RESPOSTA**

| Campo                 | Descrição                                                                           | Tipo          | Tamanho           |
|-----------------------|-------------------------------------------------------------------------------------|---------------|-------------------|
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico      | 13 dígitos        |
| codigoFormaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                        | Numérico      | Até 3 dígitos     |
| oneClick              | Retornará 1 para cadastro criado                                                    | Numérico      | 1 dígito          |
| token                 | Token                                                                               | Alfa Numérico | Até 60 caracteres |
| nomeTitularCartao     | Nome titular do cartão de crédito/débito                                            | Alfa Numérico | Até 16 caracteres |
| numeroCartaoCredito   | Numero do cartão de crédito/débito, sem espaços ou traços                           | Numérico      | Até 22 dígitos    |
| dataValidadeCartao    | Data de validade do cartão. Formato mm/yyyy                                         | Alfa Numérico | 7 caracteres      |
| emailComprador        | Email do comprador                                                                  | Alfa Numérico | 20 caracteres     |



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>