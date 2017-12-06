---
title: Cadastrando cartão
position: 1
menu: gateway
right_code: |
  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
    <soapenv:Header/>
    <soapenv:Body>
        <pag:cadastraPagamentoOneClickV2>
          <dadosOneClick>
              <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
              <emailComprador>suporte@superpay.com.br</emailComprador>
              <formaPagamento>350</formaPagamento>
              <nomeTitularCartaoCredito>Teste</nomeTitularCartaoCredito>
              <numeroCartaoCredito>4444333322221111</numeroCartaoCredito>
              <dataValidadeCartao>10/2018</dataValidadeCartao>
          </dadosOneClick>
          <usuario>superpay</usuario>
          <senha>superpay</senha>
        </pag:cadastraPagamentoOneClickV2>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo cadastro do cartão" }

  ~~~ xml
  <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <ns2:cadastraPagamentoOneClickV2Response xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
          <return>149624974900187da0175-509d-4b01-9158-a96e3ed9ccae</return>
        </ns2:cadastraPagamentoOneClickV2Response>
    </soap:body>
  </soap:envelope>
  ~~~
  {: title="Exemplo retorno cadastro do cartão" }

---

Particulariedades

* Disponível apenas no plano Corporativo;
* Disponível para cartão de crédito e débito.

Esta funcionalidade está disponível em um WebService diferenciado:


 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `https://homologacao.superpay.com.br/checkout/servicosPagamentoOneClickWS.Services?wsdl`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://superpay2.superpay.com.br/checkout/servicosPagamentoOneClickWS.Services?wsdl`
{: .informativoVermelho }

---


Funcionalidade que permite o cadastramento de cartão para utilização nas futuras compras, assim o consumidor precisará incluir apenas o código de segurança para finalizar a compra.


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para criar o token, acione o método `cadastraPagamentoOneClickV2`.
{: .informativo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


_`cadastraPagamentoOneClickV2`_
{: .subtituloAzul }

| Campo                    | Descrição                                                                           | Tipo          | Tamanho            | Obrigatório |
|--------------------------|-------------------------------------------------------------------------------------|---------------|--------------------|-------------|
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)    | Numérico      | 13 dígitos         | Sim         |
| nomeTitularCartaoCredito | Nome do titular do cartão de crédito                                                | Alfa Numérico | Até 25 caracteres  | Sim         |
| numeroCartaoCredito      | Numero do cartão de crédito. Enviar sem espaços e virgúlas                          | Numérico      | Até 22 caracteres  | Sim         |
| dataValidadeCartao       | Data de validade do cartão. Formato mm/yyyy                                         | Alfa Numérico | 7 caracteres       | Sim         |
| emailComprador           | Endereço de e-mail do comprador                                                     | Alfa Numérico | Até 100 caracteres | Não         |
| formaPagamento           | Código da forma de pagamento                                                        | Numérico      | -                  | Sim         |




**RESPOSTA**

O retorno da requisição de cadastro será apenas o Token, este deverá ser armazenado no Ecommerce para as próximas compras



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>