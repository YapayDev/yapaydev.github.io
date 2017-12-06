---
title: Consultando token
position: 3
menu: gateway
right_code: |
  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
    <soapenv:Header/>
    <soapenv:Body>
        <pag:consultaDadosOneClick>
          <token>1476210884949a25ed2d6-17cf-4ac4-af22-5c67d7907ef5</token>
          <usuario>superpay</usuario>
          <senha>superpay</senha>
        </pag:consultaDadosOneClick>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo consulta" }

  ~~~ xml
  <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <ns2:consultaDadosOneClickResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
          <return>
              <codigoEstabelecimento>1318336765212</codigoEstabelecimento>
              <codigoSeguranca/>
              <dataValidadeCartao>11/2016</dataValidadeCartao>
              <emailComprador>teste@suporte.com.br</emailComprador>
              <formaPagamento>121</formaPagamento>
              <numeroCartaoCredito>555555*****5555</numeroCartaoCredito>
          </return>
        </ns2:consultaDadosOneClickResponse>
    </soap:Body>
  </soap:Envelope>
  ~~~
  {: title="Exemplo retorno consulta" }

---

Para visualizar os dados de cartão cadastrados em um Token, basta acionar o método de consulta dentro do WS de estorno.


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para consulta, acione o método `consultaDadosOneClick`.
{: .informativo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |

| Campo | Descrição              | Tipo          | Tamanho        | Obrigatório |
|-------|------------------------|---------------|----------------|-------------|
| token | Token a ser consultado | Alfa Numérico | 100 caracteres | Sim         |

**RESPOSTA**

Ao lado exemplo de retorno de consulta.


<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>