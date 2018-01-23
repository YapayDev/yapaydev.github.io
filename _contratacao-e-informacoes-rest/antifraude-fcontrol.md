---
title: Antifraude FControl
position: 2
menu: gateway
---

O gateway fornece a possibilidade de incluir um analisador de fraude para garantir a segurança das transações.


Quando um analisador de fraude/risco é ativado, ele se encaixa depois que a transação é autorizada e antes que a mesma seja capturada. O processo como um todo segue o seguinte fluxo:


* Transação é enviada para a operadora /instituição financeira para ser autorizada.
* Uma vez autorizada, o gateway envia a transação para análise de fraude.
* Caso seja aprovada na análise, a transação entrará em modo de espera para ser enviada para a captura (de forma automática ou manual, de acordo com as configurações do estabelecimento). Caso seja negada na análise, a transação será automaticamente cancelada na operadora.

Para contratação acesse: <a href="https://www.fcontrol.com.br/Integracao/Filas" target="_blank" class="linkPadraoVerde">https://www.fcontrol.com.br/Integracao/Filas</a>


Informações para configuração
{: .subtitulo }

**Modalidade Fila**

* Usuário
* Senha




<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>