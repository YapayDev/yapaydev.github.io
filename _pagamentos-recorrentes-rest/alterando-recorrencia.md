---
title: Alterando recorrência
position: 2
menu: gateway
right_code: |
  ~~~ json
    curl
        --request PUT https://sandbox.gateway.yapay.com.br/checkout/api/v3/recorrencia/agg/10000000000000/2/atualizar
        --header "Content-Type: application/json"
        --curl -u usuario:senha .........
        --data-binary
        {
        "diaCobranca": 20
        }

  ~~~
  {: title="Exemplo alteração de dia da cobrança" }

  ~~~ json
    --header "Content-Type: application/json"
        {
        "tipo": "REST",
        "periodicidade": "MENSAL",
        "codigoEstabelecimento": "10000000000000",
        "numero": 2,
        "ativo": true,
        "dataCriacao": "02/05/2018 13:22:25",
        "formaPagamento": 170,
        "formaPagamentoDescricao": "Visa Cielo API",
        "valor": 13000,
        "quantidadeCobranca": 0,
        "diaCobranca": 20,
        "mesCobranca": 0,
        "primeiraCobranca": 0,
        "detalhes": null,
        "logs": null,
        "periodicidadeCodigo": 3
        }
  ~~~
  {: title="Exemplo retorno transação" }
  


---

Esta funcionalidade está disponível em um EndPoint diferenciado:

 <i class="fa fa-exclamation-circle" aria-hidden="true"></i>  SANDBOX: https://sandbox.gateway.yapay.com.br/checkout/api/v3/recorrencia/agg/`codigoEstabelecimento>>`/`numeroRecorrencia`/atualizar 
{: .informativoVermelho }

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> PRODUÇÃO: https://gateway.yapay.com.br/checkout/api/v3/recorrencia/agg/`codigoEstabelecimento>>`/`numeroRecorrencia`/atualizar
{: .informativoVermelho }

 

Com este método é possível a alteração do dia de cobrança e valor de uma recorrência já cadastrada no Gateway.

Alterando dia de cobrança
{: .subtitulo }

<i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="put">PUT</span>.


**REQUISIÇÃO**


Para autenticação, enviar `login` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo       | Descrição                       | Tipo     | Tamanho       |
|-------------|---------------------------------|----------|---------------|
| diaCobranca | Novo dia da cobrança recorrente | Numérico | Até 2 dígitos |


**RESPOSTA**


| Campo                   | Descrição                                                                         | Tipo          | Tamanho           |
|-------------------------|-----------------------------------------------------------------------------------|---------------|-------------------|
| tipo                    | Tipo da integração                                                                | Alfa Numérico | 4 caracteres      |
| periodicidade           | Periodicidade da cobrança                                                         | Alfa Numérico | Até 10 caracteres |
| codigoEstabelecimento   | Código do estabelecimento                                                         | Numérico      | 13 dígitos        |
| numero                  | Número da recorrência                                                             | Numérico      | Até 15 dígitos    |
| ativo                   | Status da recorrência                                                             | Boleano       | Até 4 caracteres  |
| dataCriacao             | Data da criação da recorrência                                                    | Alfa Numérico | Até 20 caracteres |
| formaPagamento          | Código da forma de pagamento                                                      | Numérico      | Até 3 dígitos     |
| formaPagamentoDescricao | Descrição da forma de pagamento                                                   | Alfa Numérico | Até 50 caracteres |
| valor                   | Valor da Recorrência                                                              | Numérico      | Até 10 dígitos    |
| quantidadeCobranca      | Quantidade de cobranças                                                           | Numérico      | Até 10 dígitos    |
| numeroCobrancaRestantes | Quantidade das cobranças restantes                                                | Numérico      | Até 10 dígitos    |
| diaCobranca             | Dia da cobrança                                                                   | Numérico      | Até 10 dígitos    |
| mesCobranca             | Mês da cobrança, retorna apenas para SOAP                                         | Numérico      | Até 10 dígitos    |
| primeiraCobranca        | 1 – Cobrança no mês corrente 2 – Cobrança no próximo mês Retorna apenas para SOAP | Numérico      | 1 dígito          |
| detalhes                | - | - |
| logs                    | - | - |
| periodicidadeCodigo     | Código da periodicidade                                                           | Numérico      | 1 dígito          |


Alterando valor de cobrança
{: .subtitulo }

 <i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="put">PUT</span>.


Para autenticação, enviar `login` e `senha` no HEADER:

| Campo   | Descrição                |
|---------|--------------------------|
| usuario | Login do estabelecimento |
| senha   | Senha do estabelecimento |


| Campo       | Descrição                          | Tipo     | Tamanho        |
|-------------|------------------------------------|----------|----------------|
| valor       | Novo valor da cobrança recorrente  | Numérico | Até 10 dígitos |

**RESPOSTA**


| Campo                   | Descrição                                                                          | Tipo           | Tamanho           |
|-------------------------|------------------------------------------------------------------------------------|----------------|-------------------|
| tipo                    | Tipo da integração                                                                 | Alfa Numérico  | 4 caracteres      |
| periodicidade           | Periodicidade da cobrança                                                          | Alfa Numérico  | Até 10 caracteres |
| codigoEstabelecimento   | Código do estabelecimento                                                          | Numérico       | 13 dígitos        |
| numero                  | Número da recorrência                                                              | Numérico       | Até 15 dígitos    |
| ativo                   | Status da recorrência                                                              | Boleano        | Até 4 caracteres  |
| dataCriacao             | Data da criação da recorrência                                                     | Alfa Numérico  | Até 20 caracteres |
| formaPagamento          | Código da forma de pagamento                                                       | Numérico       | Até 3 dígitos     |
| formaPagamentoDescricao | Descrição da forma de pagamento                                                    | Alfa Numérico  | Até 50 caracteres |
| valor                   | Valor da Recorrência                                                               | Numérico       | Até 10 dígitos    |
| quantidadeCobranca      | Quantidade de cobranças                                                            | Numérico       | Até 10 dígitos    |
| numeroCobrancaRestantes | Quantidade das cobranças restantes                                                 | Numérico       | Até 10 dígitos    |
| diaCobranca             | Dia da cobrança                                                                    | Numérico       | Até 10 dígitos    |
| mesCobranca             | Mês da cobrança, retorna apenas para SOAP                                          | Numérico       | Até 10 dígitos    |
| primeiraCobranca        | 1 – Cobrança no mês corrente 2 – Cobrança no próximo mês Retorna apenas para SOAP  | Numérico       | 1 dígito          |
| detalhes | - | - |
| logs     | - | - |
| periodicidadeCodigo     | Código da periodicidade     Numérico	1 dígito




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>
