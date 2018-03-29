---
title: Criando transação com um clique
position: 3
menu: gateway
right_code: |
  ~~~ json
    curl
        --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
        --header "Content-Type: application/json"
        --curl -u usuario:senha .........
        --data-binary
        {
            "codigoEstabelecimento": 1000000000000,
            "codigoFormaPagamento" : 997,
            "transacao": {
                "numeroTransacao": 123,
                "valor": 2000,
                "valorDesconto": 0,
                "dataVencimentoBoleto":,
                "parcelas": 1,
                "urlCampainha": "http://sualoja.com.br_campainha/",
                "urlResultado": "http://sualoja.com.br",
                "ip": "192.168.12.110",
                "idioma": 1
            },
            "checkout": {
                "processar": 1,
                "tipoPagamento" : 1,

            },
            "itensDoPedido": [
                {
                "codigoProduto": 1,
                "nomeProduto": "Produto 1",
                "codigoCategoria": 1,
                "nomeCategoria": "categoria",
                "quantidadeProduto": 1,
                "valorUnitarioProduto": 2000
                }
            ]
            "dadosCobranca": {
                "nome": "Teste 123",
                "email": "teste@teste.com",
                "documento": "12345671234",
                "endereco": {
                "logradouro": "Rua",
                "numero": "123",
                "complemento": "",
                "cep": "12345-678",
                "bairro": "Bairro",
                "cidade": "Cidade",
                "estado": "SP",
                "pais": "BR"
                },
                "telefone": [
                    {
                    "tipoTelefone": "1",
                    "ddi": "55",
                    "ddd": "12",                                                 
                    "telefone": "1234-5678"
                    }
                ]
            },
            "dadosEntrega": {
                "nome": "Teste 123",
                "email": "teste@teste.com",
                "endereco": {
                    "logradouro": "Rua",
                    "numero": "123",
                    "complemento": "",
                    "cep": "12345-678",
                    "bairro": "Bairro",
                    "cidade": "Cidade",
                    "estado": "SP",
                    "pais": "BR"
                },
                "telefone": [
                    {
                    "tipoTelefone": "1",
                    "ddi": "55",
                    "ddd": "12",
                    "telefone": "1234-5678"
                    }
                ]
            }
        }

  ~~~
  {: title="Exemplo criação transação" }

  ~~~ json
    --header "Content-Type: application/json"
        {
            "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/checkout/redirecionaPagamento?codigoPagamento=150609150796704e7-5b25-4a41-a753-a09bfb66db8d&tipoPagamento=0&oneClick=false"
        }
  ~~~
  {: title="Exemplo retorno transação" }
---

**Particulariedades**

* Disponível apenas no Plano Corporativo;
* Funcionalidade com redirecionamento;
* Importante a utilização do recurso de Campainha, para atualização dos pedidos no Ecommerce;

Neste modelo os dados de cartão, como nome titular, número e data de validade, são cadastrados no sistema de forma segura e assim o consumidor não precisará incluir estes dados em sua próxima compra, tendo que incluir apenas seu código de segurança para finalizar a transação. Os cartões cadastrados são vinculados ao email do consumidor.


REQUISIÇÃO
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="post">POST</span>.
{: .informativo }

Para autenticação, enviar `login` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo                 | Descrição                                                     | Tipo     | Obrigatório |
|-----------------------|---------------------------------------------------------------|----------|-------------|
| codigoEstabelecimento | Código único que identifica o estabelecimento dentro do Yapay | Numérico | Sim         |
| codigoFormaPagamento  | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a> - Enviar 997                     | Numérico | Sim         |

_`transacao`_
{: .subtituloAzul }

| Campo                | Descrição                                                                                                      | Tipo          | Obrigatório |
|----------------------|----------------------------------------------------------------------------------------------------------------|---------------|-------------|
| numeroTransacao      | Código único que identifica o pedido                                                                           | Numérico      | Sim         |
| valor                | Valor da transação. Não utilizar vírgulas ou pontos                                                            | Numérico      | Sim         |
| valorDesconto        | Valor do desconto da transação. Campo apenas informativo                                                       | Numérico      | Sim         |
| parcelas             | Quantidade de parcelas da transação                                                                            | Numérico      | Sim         |
| urlCampainha         | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha | Alfa Numérico | Não         |
| urlResultado         | Consumidor será redirecionado para esta URL, quando finalizar o pagamento                                      | Alfa Numérico | Não         |
| idioma               | 1 - Português 2 - Inglês 3 - Espanhol                                                                          | Numérico      | Sim         |
| ip                   | Número do IP do usuário final/cliente. Formato xxx.xxx.xxx.xxx                                                 | Alfa Numérico | Caso utilizar antifraude, sim |
| dataVencimentoBoleto | Data do Vencimento do boleto. Formato dd/mm/aaaa                                                               | Alfa Numérico | Não         |
| campoLivre1          | Campo Livre 1                                                                                                  | Alfa Numérico | Não         |
| campoLivre2          | Campo Livre 2                                                                                                  | Alfa Numérico | Não         |
| campoLivre3          | Campo Livre 3                                                                                                  | Alfa Numérico | Não         |
| campoLivre4          | Campo Livre 4                                                                                                  | Alfa Numérico | Não         |
| campoLivre5          | Campo Livre 5                                                                                                  | Alfa Numérico | Não         |


_`checkout`_
{: .subtituloAzul }

| Campo          | Descrição                                                                                                    | Tipo     | Obrigatório |
|----------------|--------------------------------------------------------------------------------------------------------------|----------|-------------|
| processar      | Enviar 0 - pagamento comum                                                                                   | Numérico | Sim         |
| tipoPagamento  | 0 - Todas formas de pagamento; 1 - Cartões de Crédito; 2 - Cartões de Débito; 3 - Boleto; 4 - Transferência; | Numérico | Sim         |
| multiploCartao | Enviar 1                                                                                                     | Numérico | Sim         |

_`itensDoPedido`_
{: .subtituloAzul }

| Campo                | Descrição                                                          | Tipo          | Obrigatório                  |
|----------------------|--------------------------------------------------------------------|---------------|------------------------------|
| codigoProduto        | Código único que identifica o produto                              | Alfa Numérico | Caso utilize antifraude, sim |
| nomeProduto          | Nome do Produto                                                    | Alfa Numérico | Caso utilize antifraude, sim |
| quantidadeProduto    | Quantidade do produto                                              | Numérico      | Sim                          |
| valorUnitarioProduto | Valor unitário do produto. Deve ser enviado sem pontos ou vírgulas | Numérico      | Sim                          |
| codigoCategoria      | Código que identifica categoria do produto                         | Alfa Numérico | Caso utilize antifraude, sim |
| nomeCategoria        | Nome da categoria do produto                                       | Alfa Numérico | Caso utilize antifraude, sim |


_`dadosCobranca`_
{: .subtituloAzul }

| Campo       | Descrição                                        | Tipo           | Obrigatório                  |
|-------------|--------------------------------------------------|----------------|------------------------------|
| nome        | Nome do comprador                                |  Alfa Numérico | 20 caracteres                |
| email       | E-mail do comprador                              |  Alfa Numérico | 20 caracteres                |
| documento   | Documento do Comprador                           |  Alfa Numérico | 100 caracteres               |
| tipoCliente | 1 - Pessoa Física 2 - Pessoa Jurídica            |  Numérico      | Caso utilize antifraude, sim |
| endereco    | Nó reservado para dados de endereço do comprador | -              | -                            |
| telefone    | Nó reservado para dados de telefone do comprador | -              | -                            |

_`endereco`_
{: .subtituloAzul }

| Campo       | Descrição               | Tipo          | Obrigatório                  |
|-------------|-------------------------|---------------|------------------------------|
| logradouro  | Endereço do comprador   | Alfa Numérico | Caso utilize antifraude, sim |
| numero      | Número do comprador     | Alfa Numérico | Caso utilize antifraude, sim |
| bairro      | Bairro do comprador     | Alfa Numérico | Caso utilize antifraude, sim |
| complemento | Complemento do endereço | Alfa Numérico | Não                          |
| cidade      | Cidade do comprador     | Alfa Numérico | Caso utilize antifraude, sim |
| estado      | Estado do comprador     | Alfa Numérico | Caso utilize antifraude, sim |
| cep         | CEP do comprador        | Alfa Numérico | Caso utilize antifraude, sim |
| pais        | País do comprador       | Alfa Numérico | Caso utilize antifraude, sim |


_`telefone`_
{: .subtituloAzul }

| Campo        | Descrição                                | Tipo          | Tamanho           | Obrigatório                  |
|--------------|------------------------------------------|---------------|-------------------|------------------------------|
| ddd          | DDD do telefone do comprador             | Alfa Numérico | Até 3 caracteres  | Caso utilize antifraude, sim |
| ddi          | DDI do telefone do comprador             | Alfa Numérico | Até 3 caracteres  | Caso utilize antifraude, sim |
| telefone     | Número do telefone                       | Alfa Numérico | Até 10 caracteres | Caso utilize antifraude, sim |
| tipoTelefone | 1 - Outros 2 - Residencial 3 - Comercial | Numérico      | Até 2 dígitos     | Sim                          |


_`dadosEntrega`_
{: .subtituloAzul }

| Campo    | Descrição                                        | Tipo          | Obrigatório |
|----------|--------------------------------------------------|---------------|-------------|
| nome     | Nome do comprador                                | Alfa Numérico | Não         |
| email    | E-mail do comprador                              | Alfa Numérico | Não         |
| endereco | Nó reservado para dados de endereço do comprador | -             | -           |
| telefone | Nó reservado para dados de telefone do comprador | -             | -           |


**RESPOSTA**

| Campo        | Descrição                                          |
|--------------|----------------------------------------------------|
| urlPagamento | URL para redirecionar o consumidor para o Checkout |


Ao lado você pode visualizar um exemplo de retorno da transação.
