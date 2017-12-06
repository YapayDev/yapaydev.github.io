---
title: Criando uma transação
position: 1
menu: gateway
right_code: |
  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:rec="http://recorrencia.webservices.superpay.ernet.com.br/">
    <soapenv:Header/>
    <soapenv:Body>
        <rec:cadastrarRecorrenciaWS>
            <recorrenciaWS>
              <dadosCartao>
                <codigoSeguranca>123</codigoSeguranca>
                <dataValidade>05/2018</dataValidade>
                <nomePortador>Teste</nomePortador>
                <numeroCartao>4444333322221111</numeroCartao>
              </dadosCartao>
              <dadosCobranca>
                <nomeComprador>Nome do Comprador</nomeComprador>
                  <telefone>
                  </telefone>
              </dadosCobranca>
              <diaCobranca>23</diaCobranca>
              <mesCobranca>10</mesCobranca>
              <estabelecimento>1000000000000</estabelecimento>
              <formaPagamento>170</formaPagamento>
              <numeroRecorrencia>1</numeroRecorrencia>
              <periodicidade>3</periodicidade>
              <primeiraCobranca>1</primeiraCobranca>
              <processarImediatamente>1</processarImediatamente>
              <quantidadeCobrancas>0</quantidadeCobrancas>
              <urlNotificacao></urlNotificacao>
              <valor>100</valor>
          </recorrenciaWS>
          <usuario>
              <senha>superpay</senha>
              <usuario>superpay</usuario>
          </usuario>
        </rec:cadastrarRecorrenciaWS>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo criação transação recorrente" }

  ~~~ xml
  <soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:rec="http://recorrencia.webservices.superpay.ernet.com.br/">
    <soapenv:Body>
      <ns2:cadastrarRecorrenciaWSResponse xmlns:ns2="http://recorrencia.webservices.superpay.ernet.com.br/">
          <return>
              <estabelecimento>1000000000000</estabelecimento>
              <numeroRecorrencia>1</numeroRecorrencia>
              <status>true</status>
              <valor>100</valor>
          </return>
        </ns2:cadastrarRecorrenciaWSResponse>
    </soapenv:Body>
  </soapenv:Envelope>
  ~~~
  {: title="Exemplo retorno transação recorrente" }

---


Esta funcionalidade está disponível em um WebService diferenciado:


 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `https://homologacao.superpay.com.br/checkout/servicosRecorrenciaWS.Services?wsdl`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://superpay2.superpay.com.br/checkout/servicosRecorrenciaWS.Services?wsdl`
{: .informativoVermelho }

---

Neste modelo, o Yapay controla os pagamentos que foram cadastrados pelo estabelecimento, de acordo com sua periodicidade, valor e dia de cobrança.

O gateway possui um processo que verifica todos os dias se existem recorrências a serem processadas. Se sim, elas são agendadas para processamento na madrugada e assim que finalizadas, o Yapay notifica o estabelecimento através do acionamento da campainha, enviada no cadastro da recorrência.

**Particulariedades**

* Disponível apenas para cartão de crédito no modelo WebService;
* Renova Fácil com a operadora Cielo;
* Importante a utilização do recurso de Campainha, para atualização dos pedidos no Ecommerce;


REQUISIÇÃO
{: .subtitulo }


Para autenticação, enviar usuario e senha:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


_`cadastrarRecorrenciaWS`_
{: .subtituloAzul }


| Campo                  | Descrição                                                                                             | Tipo     | Tamanho        | Obrigatório |
|------------------------|-------------------------------------------------------------------------------------------------------|----------|----------------|-------------|
| numeroRecorrencia      | Número da Recorrência deve ser único                                                                  | Numérico | Até 15 dígitos | Sim |
| estabelecimento        | Código que identifica o estabelecimento dentro do SuperPay (fornecido pelo gateway)                   | Numérico | 13 dígitos     | Sim |
| valor                  | Valor da recorrência. Não devem ser utilizados virgulas nem pontos                                    | Numérico | Até 10 dígitos | Sim |
| formaPagamento         | Código da forma de pagamento                                                                          | Numérico | Até 3 dígitos  | Sim |
| dadosCartao            | Array descrito abaixo                                                                                 | - | - | - |
| dadosCobranca          | Array descrito abaixo                                                                                 | - | - | - |
| dadosEntrega           | Array descrito abaixo                                                                                 | - | - | - |
| quantidadeCobrancas    | Quantidade de cobranças, caso 0 a recorrência será feita até que ocorra um cancelamento               | Numérico | Até 10 dígitos | Sim |
| diaCobranca            | Dia para cobrança                                                                                     | Numérico | Até 2 dígitos  | Sim |
| mesCobranca            | Mês para cobrança                                                                                     | Numérico | Até 2 dígitos  | Sim |
| periodicidade          | 1 – Semanal, 2 – Quinzenal, 3 – Mensal, 4 – Bimestral, 5 – Trimestral, 6 – Semestral e 7 – Anual      | Numérico | 1 dígito       | Sim |
| urlNotificacao         | URL para notificação de cada cobrança da recorrência                                                  | Alfa Numérico | Até 200 caracteres | Sim |
| primeiraCobranca       | 1– Cobrança será efetuada no mês corrente ao cadastro da recorrência / 2–Cobrança será efetuada no mês seguinte. | Numérico | 1 dígito | Sim |
| processarImediatamente | 1 – A recorrência será processada imediatamente ao cadastro                                           | Numérico | 1 dígito | Sim |


_`dadosCartao`_
{: .subtituloAzul }

| Campo           | Descrição                                                            | Tipo          | Tamanho           | Obrigatório |
|-----------------|----------------------------------------------------------------------|---------------|-------------------|-------------|
| nomePortador    | Nome do titular do cartão de crédito                                 | Alfa Numérico | Até 16 caracteres | Sim         |
| numeroCartao    | Numero do cartão de crédito, sem espaços ou traços                   | Numérico      | Até 22 caracteres | Sim         |
| codigoSeguranca | Código de segurança do cartão (campo não é armazenado pelo Yapay)    | Numérico      | Até 4 caracteres  | Sim         |
| dataValidade    | Data de validade do cartão. Formato mm/yyyy                          | Alfa Numérico | 7 caracteres      | Sim         |


_`dadosCobranca`_
{: .subtituloAzul }

| Campo                | Descrição                                      | Tipo          | Tamanho            | Obrigatório                  |
|----------------------|------------------------------------------------|---------------|--------------------|------------------------------|
| nomeComprador        | Nome do comprador                              | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| emailComprador       | E-mail do comprador                            | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| enderecoComprador    | Logrodouro do comprador                        | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| bairroComprador      | Bairro do comprador                            | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude, sim |
| complementoComprador | Complemento do endereço comprador              | Alfa Numérico | Até 50 caracteres  | Não                          |
| cidadeComprador      | Cidade do comprador                            | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude, sim |
| estadoComprador      | Estado do comprador                            | Alfa Numérico | Até 2 caracteres   | Caso utilize antifraude, sim |
| cepComprador         | CEP do comprador. Enviar sem traços ou espaços | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude, sim |
| paisComprador        | Pais do comprador                              | Alfa Numérico | Até 50 caracteres  | Não                          |
| telefone[]           | Lista de Telefones                             | List          | -                  | -                            |


_`dadosEntrega`_
{: .subtituloAzul }

| Campo              | Descrição                                    | Tipo          | Tamanho            | Obrigatório                  |
|--------------------|----------------------------------------------|---------------|--------------------|------------------------------|
| nomeEntrega        | Nome de entegra                              | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| emailEntrega       | Email de entrega                             | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| enderecoEntrega    | Logradouro de entrega                        | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| bairroEntrega      | Bairro de entrega                            | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude, sim |
| complementoEntrega | Complemento do endereço de entrega           | Alfa Numérico | Até 50 caracteres  | Não                          |
| cidadeEntrega      | Cidade de entrega                            | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude, sim |
| estadoEntrega      | Estado de entrega                            | Alfa Numérico | 2 caracteres       | Caso utilize antifraude, sim |
| cepEntrega         | CEP de entrega. Enviar sem traços ou espaços | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude, sim |
| paisEntrega        | Pais de entrega                              | Alfa Numérico | Até 50 caracteres  | Não                          |
| telefone[]         | Lista de Telefones                           | List          | -                  | -                            |


_`telefone`_
{: .subtituloAzul }

| Campo        | Descrição                                | Tipo          | Tamanho           | Obrigatório                  |
|--------------|------------------------------------------|---------------|-------------------|------------------------------|
| ddd          | DDD do telefone do comprador             | Alfa Numérico | Até 3 caracteres  | Caso utilize antifraude, sim |
| ddi          | DDI do telefone do comprador             | Alfa Numérico | Até 3 caracteres  | Caso utilize antifraude, sim |
| telefone     | Número do telefone                       | Alfa Numérico | Até 10 caracteres | Caso utilize antifraude, sim |
| tipoTelefone | 1 - Outros 2 - Residencial 3 - Comercial | Numérico      | Até 2 dígitos     | Sim                          |




**RESPOSTA**

| Campo             | Descrição                                                |
| numeroRecorrencia | Número da Recorrência                                    |
| estabelecimento   | Código do estabelecimento, fornecido pelo Yapay          |
| valor             | Valor                                                    |
| status            | Status da Recorrência ( True - Ativo, False - Inativo)   |


Ao lado você pode visualizar um exemplo de retorno da transação.




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>