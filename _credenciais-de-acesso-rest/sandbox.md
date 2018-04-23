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
|---------------------------|-----------------------------------------------------------------|
| Ambiente de Testes        | https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao  |
| Protocolo                 | REST                                                            |


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


E REDE
{: .subtituloAzul }

Utilize os cartões e valores abaixo para simular uma aprovação ou reprovação.


**Aprovação**

| Bandeira   | Número do cartão | Código de segurança | Data de validade | Valor do Pedido |
|------------|------------------|---------------------|------------------|-----------------|
| Visa       | 4002479199570736 | 132                 | 02/2019          | 511100          |
| MasterCard | 5448280000000007 | 132                 | 01/2019          | 500900          |


**Negação**

| Bandeira   | Número do cartão | Código de segurança | Data de validade | Valor do Pedido |
|------------|------------------|---------------------|------------------|-----------------|
| Visa       | 4002479199570736 | 132                 | 02/2019          | 511201          |
| MasterCard | 5448280000000007 | 132                 | 01/2019          | 501001          |



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


| Categoria  | Número de parcelas | Valor    | Exemplo  |
|------------|--------------------|----------|----------|
| A vista    |  1                 | nnnnn    | 10000    |
| Parcelado  |  2                 | nn6nn02  | 10060002 |
| Parcelado  |  3                 | nn6nn03  | 10060003 |
| Parcelado  |  4                 | nn6nn04  | 10060004 |


BOLETOS OFFLINE
{: .subtituloAzul }

Neste ambiente não configuramos dados reais para geração dos boletos por segurança. Caso queira utilizar esta forma de pagamento solicite ao Suporte Yapay e o boleto será configurado com dados fictícios.

Obs: Neste ambiente os testes ocorrem apenas com boletos sem registros.

INTERMEDIÁRIOS FINANCEIROS
{: .subtituloAzul }

Para testes com este meio de pagamento é preciso possuir cadastro com a instituição financeira.

