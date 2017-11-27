---
title: Estornando uma transação
position: 6
menu: gateway
right_code: |
    ~~~xml
        <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:est="http://estorno.webservices.superpay.ernet.com.br/">
        <soapenv:Header/>
        <soapenv:Body>
            <est:estornaTransacao>
                <codigoEstabelecimento>1000000000000</codigoEstabelecimento>
                <numeroTransacao>2</numeroTransacao>
                <valorEstorno>1000</valorEstorno>
            </est:estornaTransacao>
        </soapenv:Body>
        </soapenv:Envelope>
    ~~~
    {: title="Exemplo estorno de transação" }

    ~~~xml
        <soap:envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:body>
            <ns2:estornaTransacaoResponse xmlns:ns2="http://estorno.webservices.superpay.ernet.com.br/">
                <return>
                    Solicitacao de Estorno Cadastrada
                </return>
            </ns2:estornaTransacaoResponse>
        </soap:body>
        </soap:envelope>
    ~~~    
    {: title="Exemplo retorno estorno de transação" } 
---

A funcionalidade de estorno possui o mesmo objetivo do cancelamento, retornar o valor do pedido ao consumidor. A única diferença entre elas, é que neste modelo algumas adquirentes permitem a devolução de apenas parte do valor da venda ao consumidor, como é o caso da Cielo.

**Particulariedades**

* Disponível apenas no plano Corporativo;
* Disponível apenas para cartões de crédito.

| Operadora | Prazo para estorno | Particulariedades                                                        |
|-----------|--------------------|--------------------------------------------------------------------------|
| Cielo     | D+300              | Total e parcial. Para a bandeira Amex, disponível apenas o estorno Total |
| Bin       | D+0                | Apenas total                                                             |



Esta funcionalidade está disponível em um WebService diferenciado:


 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `https://homologacao.superpay.com.br/checkout/servicosEstornoWS.Services?wsdl`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://superpay2.superpay.com.br/checkout/servicosEstornoWS.Services?wsdl`
{: .informativoVermelho }

**REQUISIÇÃO**


 <i class="fa fa-info-circle" aria-hidden="true"></i>     Para enviar a transação, acione o método `estornaTransacao`
{: .informativo }

Para autenticação, enviar `usuario` e `senha`:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo                 | Descrição                                                                        | Tipo      | Tamanho        |
|-----------------------|----------------------------------------------------------------------------------|-----------|----------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                | Numérico  | Até 8 dígitos  |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway) | Numérico  | 13 dígitos     |
| valorEstorno          | Valor do estorno                                                                 | Numérico  | Ate 10 dígitos |