---
title: Como Funciona
position: 1
menu: intermediador
---

Para utilizar algumas APIs do Yapay, é necessário autorizar a aplicação, onde o cliente estará permitindo a utilização da aplicação para sua conta TrayCheckout.

![Fluxo da API](/images/intermediador/conteudo/Integracao_api.png "Fluxo da API"){: width="100%" height="auto" }

O serviço utilizado para a autorização é o padrão aberto para Autorização oAuth (Open Authorization). O oAuth fornece métodos para acesso aos recursos de um servidor, como um cliente diferente ou um usuário final, fornecendo também que os usuários finais autorizem o acesso de terceiros aos seus recursos neste servidor sem compartilhar suas credenciais. 

Nas APIs que não necessitam de autorização, é solicitado o token da conta do vendedor. Essa informação é passada pelo setor Comercial.
