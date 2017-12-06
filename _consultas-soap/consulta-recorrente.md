---
title: Consulta recorrente
position: 4
menu: gateway
right_code: |
  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:rec="http://recorrencia.webservices.superpay.ernet.com.br/">
    <soapenv:Header/>
    <soapenv:Body>
      <rec:consultaTransacaoRecorrenciaWS>
          <recorrenciaConsultaWS>
              <estabelecimento>1000000000000</estabelecimento>
              <numeroRecorrencia>1</numeroRecorrencia>
          </recorrenciaConsultaWS>
          <usuario>
              <senha>superpay</senha>
              <usuario>superpay</usuario>
          </usuario>
        </rec:consultaTransacaoRecorrenciaWS>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo criação transação recorrente" }

  ~~~ xml
  <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <ns2:consultaTransacaoRecorrenciaWSResponse xmlns:ns2="http://recorrencia.webservices.superpay.ernet.com.br/">
          <return>
              <autorizacao>145681</autorizacao>
              <codigoFormapagamento>170</codigoFormapagamento>
              <codigoTransacaoOperadora>0</codigoTransacaoOperadora>
              <dataAprovacaoOperadora>2017-06-02 10:20:30</dataAprovacaoOperadora>
              <estabelecimento>1000000000000</estabelecimento>
              <mensagemVenda>Transação capturada com sucesso</mensagemVenda>
              <numeroCobrancaRestantes>0</numeroCobrancaRestantes>
              <numeroCobrancaTotal>Sem Limite</numeroCobrancaTotal>
              <numeroComprovanteVenda>0602102031041</numeroComprovanteVenda>
              <numeroPedido>1</numeroPedido>
              <numeroRecorrencia>10000001</numeroRecorrencia>
              <statusTransacao>1</statusTransacao>
              <valor>100</valor>
          </return>
        </ns2:consultaTransacaoRecorrenciaWSResponse>
    </soap:Body>
  </soap:Envelope>
  ~~~
  {: title="Exemplo retorno transação recorrente" }

---

Consulta para receber informações da recorrência e da última cobrança realizada.


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para consulta, acione o método `rec:consultaTransacaoRecorrenciaWS`.
{: .informativo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo             | Descrição                                                                           | Tipo     | Tamanho       | Obrigatório |
|-------------------|-------------------------------------------------------------------------------------|----------|---------------|-------------|
| numeroRecorrencia | Número da Recorrência a ser consultado                                              | Numérico | Até 8 dígitos | Sim         |
| estabelecimento   | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway) | Numérico | 3 dígitos     | Sim         |

**RESPOSTA**

| Campo                    | Descrição                                                                                                                                    |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| numeroRecorrencia        | Número da Recorrência                                                                                                                        |
| estabelecimento          | Código do estabelecimento, fornecido pelo SuperPay                                                                                           |
| valor                    | Valor                                                                                                                                        |
| statusTransacao          | Status atual da transação recorrente                                                                                                         |
| numeroPedido             | Número do Pedido                                                                                                                             |
| numeroCobrancaTotal      | Quantidade total de cobranças pedidas no cadastro. Caso não tenha sido pedido um valor limite, este campo retornará a mensagem: “Sem Limite" |
| numeroCobrancaRestantes  | Quantidade restante de cobranças a serem efetuadas.                                                                                          |
| autorizacao              | Código de autorização retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                               |
| codigoTransacaoOperadora | Código de transação retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                                 |
| dataAprovacaoOperadora   | Data de aprovação retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                                   |
| numeroComprovanteVenda   | Número do comprovante de venda retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                      |
| mensagemVenda            | Mensagem de venda retornado pela operadora. Retornado apenas se alguma cobrança já ocorreu                                                   |

Ao lado você pode visualizar um exemplo de retorno da transação.



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>