---
title: Status de transação
position: 1
menu: gateway
---

| Código  | Nome                       | Descrição                                                                           |
|---------|----------------------------|-------------------------------------------------------------------------------------|
| 1       | Pago e Capturado           | Transação está autorizada e confirmada na instituição financeira                    |
| 2       | Pago e Não Capturado       | Transação está apenas autorizada, aguardando confirmação (captura)                  |
| 3       | Não Pago                   | Transação negada pela instituição financeira                                        |
| 5       | Transação em Andamento     | Comum para pagamentos cartão redirect ou pagamentos com autenticação                |
| 8       | Aguardando Pagamento       | Comum para pagamentos com boletos e pedidos em reprocessamento                      |
| 9       | Falha na Operadora         | Houve um problema no processamento com a adquirente                                 |
| 13      | Cancelada                  | Transação cancelada na adquirente                                                   |
| 14      | Estornada                  | A venda foi estornada na adquirente                                                 |
| 15      | Em Análise de Fraude       | A transação foi enviada para o sistema de análise de riscos. Status transitório     |
| 17      | Recusado pelo AntiFraude   | A transação foi negada pelo sistema análise de risco                                |
| 18      | Falha na Antifraude        | Falha. Não foi possível enviar pedido para a análise de Risco, porém será reenviado |
| 21      | Boleto Pago a menor        | O boleto foi pago com valor menor do emitido                                        |
| 22      | Boleto Pago a maior        | O boleto foi pago com valor maior do emitido                                        |
| 23      | Estorno Parcial            | A venda estonada na adquirente parcialmente                                         |
| 24      | Estorno Não Autorizado     | O Estorno não foi autorizado pela adquirente                                        |
| 25      | Falha no estorno           | Falha ao enviar estorno para a operadora                                            |
| 31      | Transação já Paga          | Transação já existente e finalizada na adquirente                                   |
| 40      | Aguardando Cancelamento    | Processo de cancelamento em andamento                                               |