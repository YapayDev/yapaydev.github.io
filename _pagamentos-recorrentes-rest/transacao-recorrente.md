---
title: Criando uma transação recorrente
position: 1
menu: gateway
right_code: |
  ~~~ json
    curl
    --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/recorrencia
    --header "Content-Type: application/json"
    --curl -u usuario:senha .........
    --data-binary
    {
        "estabelecimento": "1000000000000",
        "recorrencia": {
            "formaPagamento": 170,
            "numeroRecorrencia": 2,
            "valor": 13000,
            "modalidade": "1",
            "periodicidade": "3",
            "urlNotificacao": "http://teste.com.br/campainha",
            "processarImediatamente": "true",
            "quantidadeCobrancas": "0",
            "dataPrimeiraCobranca": "30/06/2030",

            "dadosCobranca": {
                "nomeComprador": "Teste Recorrencia",
                "documento": "12312312312",
                "emailComprador": "teste@teste.com.br",
                "tipoCliente": "1",
                "telefone": {
                    "tipoTelefone": "1"
                }
            },
            "dadosCartao": {
                "nomePortador": "Teste",
                "numeroCartao": "0000000000000001",
                "codigoSeguranca": "287",
                "dataValidade": "01/2018"
            }
        }
    }


  ~~~
  {: title="Exemplo criação transação" }

  ~~~ json
    --header "Content-Type: application/json"
    "recorrencia": {
        "estabelecimento": "1000000000000",
        "numeroRecorrencia": 2,
        "codigoFormaPagamento": 170,
        "valor": 13000,
        "numeroCobrancaTotal": 0,
        "numeroCobrancaRestantes": -1,
        "status": 0,
        "mensagem": "Processamento realizado com sucesso.",
        "numeroPedido": 20001,
        "statusTransacao": 1,
        "autorizacao": "123456",
        "codigoTransacaoOperadora": "00",
        "dataAprovacaoOperadora": "30/05/2030",
        "numeroComprovanteVenda": "1006993069000891071A",
        "mensagemVenda": "Operation Success"
    }


  ~~~
  {: title="Exemplo retorno transação" }
  


---

 <i class="fa fa-exclamation-circle" aria-hidden="true"></i> SANDBOX: `https://sandbox.gateway.yapay.com.br/checkout/api/v3/recorrencia`
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: `https://gateway.yapay.com.br/checkout/api/v3/recorrencia`
{: .informativoVermelho }

 
Neste modelo, o Yapay controla os pagamentos que foram cadastrados pelo estabelecimento, de acordo com sua periodicidade, valor e dia de cobrança.

O gateway possui um processo que verifica todos os dias se existem recorrências a serem processadas. Se sim, elas são agendadas para processamento na madrugada e assim que finalizadas, o Yapay notifica o estabelecimento através do acionamento da campainha, enviada no cadastro da recorrência.

**Particulariedades**

* Disponível apenas para cartão de crédito no modelo WebService;
* Renova Fácil com a operadora Cielo;
* Importante a utilização do recurso de Campainha, para atualização dos pedidos no Ecommerce;


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="post">POST</span>.
{: .informativo }

Para autenticação, enviar `login` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |



| Campo                  | Descrição                                                                                 | Tipo          | Tamanho           | Obrigatório |
|------------------------|-------------------------------------------------------------------------------------------|---------------|-------------------|-------------|
| numeroRecorrencia      | Número da Recorrência deve ser único                                                                            | Numérico      | Até 15 dígitos     | Sim |
| estabelecimento        | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)                                | Numérico      | 13 dígitos         | Sim |
| valor                  | Valor da recorrência. Não devem ser utilizados virgulas nem pontos                                              | Numérico      | Até 10 dígitos     | Sim |
| modalidade             | Modalidade do pagamento, enviar 1                                                                               | Numérico      | 1 dígito           | Sim |
| formaPagamento         | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                                                                                                                                   | Numérico      | Até 3 dígitos      | Sim |
| dadosCartao            | Array descrito abaixo                                                                                           | -             | -                  | -   |
| dadosCobranca          | Array descrito abaixo                                                                                           | -             | -                  | -   |
| dadosEntrega           | Array descrito abaixo                                                                                           | -             | -                  | -   |
| quantidadeCobrancas    | Quantidade de cobranças, caso 0 a recorrência será feita até que ocorra um cancelamento                         | Numérico      | Até 10 dígitos     | Sim |
| dataPrimeiraCobranca   | Data para a primeira cobrança. Formato dd/mm/aaaa                                                               | Alfa Numérico | 10 caracteres      | Sim |

| periodicidade          | 1 – Semanal, 2 – Quinzenal, 3 – Mensal, 4 – Bimestral, 5 – Trimestral, 6 – Semestral e 7 – Anual                | Numérico      | 1 dígito           | Sim |
| urlNotificacao         | URL para notificação de cada cobrança da recorrência                                                            | Alfa Numérico | Até 200 caracteres | Sim |
| processarImediatamente | true – A recorrência será processada imediatamente ao cadastro                                                  | Booleano      | 4 caracteres       | Sim |
| campoLivre1            | Campo Livre 1                                                                                                   | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre2            | Campo Livre 2                                                                                                   | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre3            | Campo Livre 3                                                                                                   | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre4            | Campo Livre 4                                                                                                   | Alfa Numérico | Até 16 caracteres  | Não |
| campoLivre5            | Campo Livre 5                                                                                                   | Alfa Numérico | Até 16 caracteres  | Não |



_`dadosCartao`_
{: .subtituloAzul }

| Campo           | Descrição                                                                | Tipo          | Tamanho           | Obrigatório |
|-----------------|--------------------------------------------------------------------------|---------------|-------------------|-----|
| nomePortador    | Nome do titular do cartão de crédito (Exatamente como escrito no cartão) | Alfa Numérico | Até 16 dígitos    | Sim |
| numeroCartao    | Numero do cartão de crédito, sem espaços ou traços                       | Numérico      | Até 22 caracteres | Sim |
| codigoSeguranca | Código de segurança do cartão (campo não é armazenado pelo Yapay)     | Numérico      | Até 4 caracteres  | Sim |
| dataValidade    | Data de validade do cartão. Formato mm/yyyy                              | Alfa Numérico | 7 caracteres      | Sim |


_`dadosCobranca`_
{: .subtituloAzul }

| Campo                | Descrição                                               | Tipo          | Tamanho            | Obrigatório                  |
|----------------------|---------------------------------------------------------|---------------|--------------------|------------------------------|
| nomeComprador        | Nome do comprador                                       | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| emailComprador       | E-mail do comprador                                     | Alfa Numérico | Até 100 caracteres | Caso utilize antifraude, sim |
| enderecoComprador    | Logrodouro do comprador                                 | Alfa Numérico | Até 100 caracteres | Sim                          |
| bairroComprador      | Bairro do comprador                                     | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude, sim |
| complementoComprador | Complemento do endereço comprador                       | Alfa Numérico | Até 50 caracteres  | Não                          |
| cidadeComprador      | Cidade do comprador                                     | Alfa Numérico | Até 50 caracteres  | Caso utilize antifraude, sim |
| estadoComprador      | Estado do comprador                                     | Alfa Numérico | Até 2 caracteres   | Caso utilize antifraude, sim |
| cepComprador         | CEP do comprador. Enviar sem traços ou espaços          | Alfa Numérico | Até 10 caracteres  | Caso utilize antifraude, sim |
| paisComprador        | Pais do comprador                                       | Alfa Numérico | Até 50 caracteres  | Não                          |
| telefone[]           | Lista de Telefones                                      | List          | -                  |  -                           |
| tipoCliente          | Tipo do Cliente - 1 - Pessoa Física 2 - Pessoa Jurídica | Alfa Numérico | 1                  | Sim |

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

| Campo                    | Descrição                                                                      | Tipo          | Tamanho           |
|--------------------------|--------------------------------------------------------------------------------|---------------|-------------------|
| numeroRecorrencia        | Número da Recorrência                                                          | Numérico      | Até 15 dígitos    |
| estabelecimento          | Código do estabelecimento, fornecido pelo Yapay                                | Numérico      | 13 dígitos        |
| valor                    | Valor                                                                          | Numérico      | Até 10 dígitos    |
| codigoFormaPagamento     | Código de retorno da adquirente                                        | Numérico      | Até 3 dígitos     |
| numeroCobrancaTotal      | Quantidade máxima de cobranças                                                 | Numérico      | Até 10 dígitos    |
| numeroCobrancaRestantes  | Quantidade de cobranças restantes                                              | Numérico      | Até 10 dígitos    |
| status                   | Status atual da recorrência, sendo 0 para recorrência cancelada e 1 para ativa | Numérico      | 1 dígito          |
| mensagem                 | Mensagem da recorrência                                                        | Alfa Numérico | Até 50 caracteres |
| numeroPedido             | Número da Cobrança Recorrente                                                  | Numérico      | Até 19 dígitos    |
| statusTransacao          | <a href="/gateway/rest/codigos-da-api-rest/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação recorrente</a>                                           | Numérico      | Até 2 dígitos     |
| autorizacao              | Código de autorização da Adquirente                                            | Alfa Numérico | Até 20 caracteres |
| codigoTransacaoOperadora | Código de retorno da adquirente                                                | Alfa Numérico | Até 20 caracteres |
| dataAprovacaoOperadora   | Data aprovação Adquirente                                                      | Alfa Numérico | Até 10 caracteres |
| numeroComprovanteVenda   | Número Comprovante Adquirente                                                  | Alfa Numérico | Até 20 caracteres |
| mensagemVenda            | Mensagem Venda Adquirente                                                      | Alfa Numérico | Até 50 caracteres |
|

Ao lado você pode visualizar um exemplo de retorno da transação.




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>

