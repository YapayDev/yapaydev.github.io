---
title: Atualizar Automaticamente o pedido
position: 2
menu: intermediador
---

Para realizar a atualização automática do pedido, o Yapay pode realizar a comunicação a cada alteração de status de uma transação, fazendo com que seu sistema acompanhe todo o fluxo de status e esteja sempre atualizado quanto a situação da transação.

Dessa forma você precisa configurar uma URL que receberá a chamada, processará os dados recebidos, e em seguida irá obter mais detalhes da transação através da <a href="/intermediador/apis/#api-consulta-transacao" target="_blank" class="linkPadraoVerde">API de Consulta de Transação</a>. Esse parâmetro está disponível em ambas as integrações (POST ou API) e chama-se **transaction[url_notification]**.


Para mais informações sobre **Notificação Automática de Status**, <a href="/intermediador/notificacao-automatica-status/" target="_blank" class="linkPadraoVerde">clique aqui</a>.
{:.info}



<div class="voltar-ao-topo"><a href="#"><i class="fa fa-arrow-up" aria-hidden="true"></i>Voltar ao topo</a></div>