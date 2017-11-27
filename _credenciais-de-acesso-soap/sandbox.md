---
title: Sandbox
position: 1
menu: gateway
---

O Yapay disponibiliza um ambiente totalmente gratuito para sua equipe de desenvolvimento realizar testes. Basta solicitar seu ambiente para nossa equipe comercial através do email [comercial@yapay.com.br] com as seguintes informações:

* Nome da Loja;
* CNPJ;
* Email para criação do cadastro.


| Endereço para Integração  |                                                                                         |
|---------------------------|-----------------------------------------------------------------------------------------|
| Ambiente de Testes        | https://homologacao.superpay.com.br/checkout/servicosPagamentoCompletoWS.Services?wsdl  |
| Protocolo                 | SOAP/WebService                                                                         |


CARTÕES E REGRAS PARA TESTES
{: .subtitulo }

CIELO API 3.0
{: .subtituloAzul }

**Aprovação**

| Bandeira  | Número do cartão  | Código de segurança  | Data de validade                    |
|-----------|-------------------|----------------------|-------------------------------------|
| Qualquer  | 0000000000000001  | 123                  | qualquer posteiror ao dia corrente  |


**Negação**

| Bandeira | Número do cartão | Código de segurança | Data de validade                    | 
| ---------|------------------|---------------------|-------------------------------------|
| Qualquer | 0000000000000002 | 123                 | qualquer posteiror ao dia corrente  |


ELAVON
{: .subtituloAzul }

Para testar esta modalidade as seguintes regras abaixo devem ser utilizadas:

* Para aprovação da venda, o valor total da venda deve ser em valor inteiro, ou seja, sem centavos;
* Para negação, basta enviar o valor total da venda quebrado, ou seja, com centavos;
* Como o ambiente de testes da Elavon é compartilhado, sugerimos gerar o número do pedido baseado em YYMMDDHHMMSS (ano, mês, dia, hora, minuto, segundo).

| Bandeira   | Número do cartão | Código de segurança  | Data de validade                   |
|------------|------------------|----------------------|------------------------------------|
| Visa       | 4444111122223333 | 123                  | Qualquer posterior ao dia corrente | 
| MasterCard | 5431111111111111 | 123                  | Qualquer posterior ao dia corrente | 
| Diners     | 38000000000006   | 123                  | Qualquer posterior ao dia corrente | 
| Discover   | 6011111111111117 | 123                  | Qualquer posterior ao dia corrente | 


REDE KOMERCI
{: .subtituloAzul }

Para testes com esta operadora não há necessidade de contratação, basta solicitar ao Suporte Yapay a configuração desta forma de pagamento. Esta operadora não possui regras para aprovação ou negação dos pedidos, os retornos são aleatórios independente dos dados enviados.


BIN - FIRST DATA
{: .subtituloAzul }

* Utilizar os dados abaixo para aprovação;
* Para aprovação com a bandeira Cabal, o valor do pedido deve ser superior a R$100,00.

| Bandeira   | Número do cartão     | Código de segurança  | Data de validade |
|------------|----------------------|----------------------|------------------|
| Visa       | 4488540010253330004  | 123                  | 12/2026          |
| MasterCard | 5547220000000102     | 123                  | 12/2017          |
| Cabal*     | 6042030000204200     | 123                  | 09/2029          |


GETNET
{: .subtituloAzul }

Para aprovação das vendas, seguir tabelas abaixo:

| Bandeira   | Número do cartão | Código de segurança | Data de validade |
|------------|------------------|---------------------|------------------|
| Visa       | 4012001038166662 | 456                 | 10/2017          |
| MasterCard | 5453010000083303 | 321                 | 10/2017          |


| Categoria  | Número de parcelas | Valor    |
|------------|--------------------|----------| 
| A vista    |  1                 | nnn,nn   |
| Parcelado  |  2                 | nn6nn,02 |
| Parcelado  |  3                 | nn6nn,03 |
| Parcelado  |  4                 | nn6nn,04 |


BOLETOS OFFLINE
{: .subtituloAzul }

Neste ambiente não configuramos dados reais para geração dos boletos por segurança. Caso queira utilizar esta forma de pagamento solicite ao Suporte SuperPay e o boleto será configurado com dados fictícios.

Obs: Neste ambiente os testes ocorrem apenas com boletos sem registros.

INTERMEDIÁRIOS FINANCEIROS
{: .subtituloAzul }

Para testes com este meio de pagamento é preciso possuir cadastro com a instituição financeira.

