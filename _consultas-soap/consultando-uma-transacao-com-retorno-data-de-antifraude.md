---
title: Consultando uma transação de Antifraude
position: 2
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
  {: title="Exemplo consulta" }

  ~~~ xml
  <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <ns2:consultaDataAntifraudeResponse xmlns:ns2="http://pagamentos.webservices.superpay.ernet.com.br/">
          <return>
              <numeroTransacao>6903</numeroTransacao>
              <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
              <codigoFormaPagamento>170</codigoFormaPagamento>
              <valor>200</valor>
              <valorDesconto>0</valorDesconto>
              <taxaEmbarque>0</taxaEmbarque>
              <parcelas>1</parcelas>
              <urlPagamento>1495797252959508629a6-16f2-4311-a79b-e290b4d64237</urlPagamento>
              <statusTransacao>1</statusTransacao>
              <autorizacao>345051</autorizacao>
              <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
              <dataAprovacaoOperadora>2017-05-26 08:14:17</dataAprovacaoOperadora>
              <dataRetornoAntifraude>26/05/2017 17:36:41</dataRetornoAntifraude>
              <numeroComprovanteVenda>0526081417585</numeroComprovanteVenda>
              <mensagemVenda>Transação capturada com sucesso</mensagemVenda>
          </return>
        </ns2:consultaDataAntifraudeResponse>
    </soap:Body>
  </soap:Envelope>
  ~~~
  {: title="Exemplo retorno consulta" }

---

Método de consulta com estrutura parecida ao método comum, porém com um novo campo informando a data e horário do retorno da antifraude ao Gateway.

**Particularidades**

* Disponível apenas para estabelecimentos que possuem contrato com a Clear Sale nas modalidades Total/Total Garantido e Application;
* Para utilização solicitar ativação ao Suporte SuperPay.

**REQUISIÇÃO**

<i class="fa fa-info-circle" aria-hidden="true"></i> Para consultas, acione o método `consultaDataAntifraude`.
{: .informativo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo                 | Descrição                                                                           | Tipo     | Tamanho       | Obrigatório |
|-----------------------|-------------------------------------------------------------------------------------|----------|---------------|-------------|
| numeroTransacao       | Código que identifica a transação dentro do SuperPay                                | Numérico | Até 8 dígitos | Sim         |
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