---
title: Cancelando uma recorrência
position: 2
menu: gateway
right_code: |
  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:rec="http://recorrencia.webservices.superpay.ernet.com.br/">
    <soapenv:Header/>
    <soapenv:Body>
        <rec:cancelarRecorrenciaWS>
          <recorrenciaCancelarWS>
              <estabelecimento>1000000000000</estabelecimento>
              <numeroRecorrencia>1</numeroRecorrencia>
          </recorrenciaCancelarWS>
          <usuario>
              <senha>superpay</senha>
              <usuario>superpay</usuario>
          </usuario>
        </rec:cancelarRecorrenciaWS>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo cancelamento transação recorrente" }

  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:rec="http://recorrencia.webservices.superpay.ernet.com.br/">
    <soapenv:Body>
      <ns2:cancelarRecorrenciaWSResponse xmlns:ns2="http://recorrencia.webservices.superpay.ernet.com.br/">
          <return>
              <estabelecimento>1000000000000</estabelecimento>
              <numeroRecorrencia>1</numeroRecorrencia>
              <status>false</status>
              <valor>100</valor>
          </return>
        </ns2:ccancelarRecorrenciaWSResponse>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo retorno cancelamento transação recorrente" }

---

**REQUISIÇÃO**
{: .subtitulo }

Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo             | Descrição                                                                           | Obrigatório |
|-------------------|-------------------------------------------------------------------------------------|-------------|
| numeroRecorrencia | Número da Recorrência a ser cancelada                                               | Sim         |
| estabelecimento   | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)    | Sim         |

**RESPOSTA**

| Campo             | Descrição                                              |
|-------------------|--------------------------------------------------------|
| numeroRecorrencia | Número da Recorrência                                  |
| estabelecimento   | Código do estabelecimento, fornecido pelo Yapay        |
| valor             | Valor                                                  |
| status            | Status da Recorrência ( True - Ativo, False - Inativo) |