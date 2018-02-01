---
title: Alterar cartão 
position: 3
menu: gateway
right_code: |
  ~~~ json
  curl
    --request PUT https://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick/1514483826864c3149224-67db-4557-8950-6a80f708c1c5/alterar
    --header "Content-Type: application/json"
    --curl -u usuario:senha
    --data-binary
    {
    "codigoEstabelecimento": 1000000000000,
    "formaPagamento": 170,
    "nomeTitularCartaoCredito": "Teste OneClick",
    "numeroCartaoCredito": "0000000000000002",
    "dataValidadeCartao": "10/2021",
    "emailComprador": "yapay@yapay.com.br"
    }

  ~~~
  {: title="Exemplo de transação" }

  ~~~ json
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
  {: title="Exemplo retorno" }
---

Funcionalidade permite a alteração dos dados já cadastrados na base do Gateway.

 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `https://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick/<<`token`>>/alterar`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://gateway.yapay.com.br/checkout/api/v3/oneclick/<<`token`>>/alterar`
{: .informativoVermelho }


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para criar o token, acione o método <span class="put">PUT</span>.
{: .informativo }

Para autenticação, enviar `usuario` e `senha` seguindo os padrões Basic Authentication:


| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |


| Campo                 | Descrição                                                                           | Tipo          | Tamanho           | Obrigatório |
|-----------------------|-------------------------------------------------------------------------------------|---------------|-------------------|-------------|
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico      | 13 dígitos        | Sim         |
| codigoFormaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                        | Numérico      | Até 3 dígitos     | Sim         |
| nomeTitularCartao     | Nome titular do cartão de crédito/débito                                            | Alfa Numérico | Até 16 caracteres | Sim         |
| numeroCartaoCredito   | Numero do cartão de crédito/débito, sem espaços ou traços                           | Numérico      | Até 22 dígitos    | Sim         |
| dataValidadeCartao    | Data de validade do cartão. Formato mm/yyyy                                         | Alfa Numérico | 7 caracteres      | Sim         |
| emailComprador        | Email do comprador                                                                  | Alfa Numérico | 20 caracteres     | Não         |


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