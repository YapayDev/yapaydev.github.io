---
title: Consultando uma Transação
position: 1
menu: gateway
right_code: |
  ~~~ xml
  <soapenv:envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:pag="http://pagamentos.webservices.superpay.ernet.com.br/">
    <soapenv:header></soapenv:header>
    <soapenv:body>
        <pag:consultaTransacao>
          <consultaTransacaoWS>
              <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
              <numeroTransacao>1</numeroTransacao>
          </consultaTransacaoWS>
          <usuario>superpay</usuario>
          <senha>superpay</senha>
        </pag:consultaTransacao>
    </soapenv:body>
  </soapenv:envelope>
  ~~~
  {: title="Exemplo de consulta" }

  ~~~ xml
  <soap:envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:body>
        <ns2:consultaTransacaoResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
          <return>
              <autorizacao>123456</autorizacao>
              <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
              <codigoFormaPagamento>120</codigoFormaPagamento>
              <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
              <dataAprovacaoOperadora>24/05/2017</dataAprovacaOperadora>
              <mensagemVenda>Transacao cancelada com sucesso</mensagemVenda>
              <numeroComprovanteVenda>1006993069181F841001</numeroComprovanteVenda>
              <numeroTransacao>1</numeroTransacao>
              <parcelas>1</parcelas>
              <statusTransacao>13</statusTransacao>
              <taxaEmbarque>0</taxaEmbarque>
              <urlPagamento>14132971582229c00506d-e84d-4526-b902-92190d5aa808<urlpagamento></urlpagamento>
              <valor>200</valor>
              <valorDesconto>0</valorDesconto>
          </return>
        </ns2:consultaTransacaoResponse>
    </soap:body>
  </soap:envelope>
  ~~~
  {: title="Exemplo retorno de consulta" }

---

Para receber novamente os dados de retorno de uma venda, realize uma consulta.

REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para consultas, acione o método `consultaTransacao`.
{: .informativo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo                 | Descrição                                                                           | Tipo     | Tamanho       | Obrigatório |
|-----------------------|-------------------------------------------------------------------------------------|----------|---------------|-------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                   | Numérico | Até 8 dígitos | Sim         |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico | 13 dígitos    | Sim         |


**RESPOSTA**

| Campo                    | Descrição                                                  | Tipo          | Tamanho            |
|--------------------------|------------------------------------------------------------|---------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do SuperPay       | Numérico      | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do SuperPay | Numérico      | 13 dígitos         |
| codigoFormaPagamento     | Código da forma de pagamento                               | Numérico      | Até 3 dígitos      |
| valor                    | Valor da transação.                                        | Numérico      | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                             | Numérico      | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                        | Numérico      | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                        | Numérico      | Até 2 dígitos      |
| urlPagamento             | Url para autenticação em caso de cartão de débito          | Alfa Numérico | Até 500 caracteres |
| statusTransacao          | Status atual da transação                                  | Numérico      | Até 2 dígitos      |
| autorizacao              | Número de autorização da adquirente                        | Numérico      | Até 20 dígitos     |
| codigoTransacaoOperadora | Código de retorno da adquirente                            | Numérico      | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data aprovação                                             | Alfa Numérico | Até 10 dígitos     |
| numeroComprovanteVenda   | Número Comprovante de venda                                | Alfa Numérico | Até 20 dígitos     |
| mensagemVenda            | Mensagem de venda                                          | Alfa Numérico | Até 50 dígitos     |