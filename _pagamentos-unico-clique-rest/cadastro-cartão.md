---
title: Cadastro Cartão 
position: 1
menu: gateway
right_code: |
  ~~~ json
  curl
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick
    --header "Content-Type: application/json"
    --curl -u usuario:senha
    --data-binary
    {
    "codigoEstabelecimento": 1000000000000,
    "formaPagamento": 170,
    "nomeTitularCartaoCredito": "Teste OneClick",
    "numeroCartaoCredito": "0000000000000001",
    "dataValidadeCartao": "10/2020",
    "emailComprador": "yapay@yapay.com.br"
    }

  ~~~
  {: title="Exemplo de transação" }

  ~~~ json
  --header "Content-Type: application/json
    { 
    "codigoEstabelecimento": 1000000000000,
    "formaPagamento": 170,
    "oneClick": 1,
    "token": "1514483826864c3149224-67db-4557-8950-6a80f708c1c5",
    "nomeTitularCartaoCredito": "Teste OneClick",
    "numeroCartaoCredito": "000000******0001",
    "dataValidadeCartao": "10/2020",
    "emailComprador": "yapay@yapay.com.br"
    }

  ~~~
  {: title="Exemplo retorno" }

---


Através desta funcionalidade é possível armazenar os dados de cartão do cliente de forma segura (sempre será solicitado seu código de segurança) nos serviços do Gateway e eles não precisarão digitar todos os dados de cartão sempre que efetuarem uma compra.

**Particulariedades**

* Disponível apenas no plano Corporativo;
* Disponível para cartões de crédito e débito.


Funcionalidade que permite o cadastramento de cartão para utilização nas futuras compras, assim o consumidor precisará incluir apenas o código de segurança para finalizar a compra.

 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `https://sandbox.gateway.yapay.com.br/checkout/api/v3/oneclick/`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://gateway.yapay.com.br/checkout/api/v3/oneclick/`
{: .informativoVermelho }


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para criar o token, acione o método <span class="post">POST</span>.
{: .informativo }

 Para autenticação, enviar `usuario` e `senha` seguindo os padrões Basic Authentication:

| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |



| Campo                 | Descrição                                                                           | Tipo          | Tamanho           | Obrigatório |
|-----------------------|-------------------------------------------------------------------------------------|---------------|-------------------|-------------|
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico      | 13 dígitos        | Sim         |
| formaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                        | Numérico      | Até 3 dígitos     | Sim         |
| nomeTitularCartaoCredito     | Nome titular do cartão de crédito/débito                                            | Alfa Numérico | Até 16 caracteres | Sim         |
| numeroCartaoCredito   | Numero do cartão de crédito/débito, sem espaços ou traços                           | Numérico      | Até 22 dígitos    | Sim         |
| dataValidadeCartao    | Data de validade do cartão. Formato mm/yyyy                                         | Alfa Numérico | 7 caracteres      | Sim         |
| emailComprador        | Email do comprador                                                                  | Alfa Numérico | 20 caracteres     | Não         |


**RESPOSTA**


| Campo                 | Descrição                                                                           | Tipo          | Tamanho           |
|-----------------------|-------------------------------------------------------------------------------------|---------------|-------------------|
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico      | 13 dígitos        |
| formaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                        | Numérico      | Até 3 dígitos     |
| oneClick              | Retornará 1 para cadastro criado                                                    | Numérico      | 1 dígito          |
| token                 | Token criado                                                                        | Alfa Numérico | Até 60 caracteres |
| nomeTitularCartaoCredito     | Nome titular do cartão de crédito/débito                                            | Alfa Numérico | Até 16 caracteres |
| numeroCartaoCredito   | Numero do cartão de crédito/débito, sem espaços ou traços                           | Numérico      | Até 22 dígitos    |
| dataValidadeCartao    | Data de validade do cartão. Formato mm/yyyy                                         | Alfa Numérico | 7 caracteres      |
| emailComprador        | Email do comprador                                                                  | Alfa Numérico | 20 caracteres     |




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>