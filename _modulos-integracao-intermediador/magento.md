---
title: Magento
position: 2
menu: intermediador
---

Para disponibilizar a API de Pagamento do **Yapay** como facilitador de pagamento na plataforma Magento, basta acessar o _Magento Connect Manager_ de sua loja e instalar o módulo disponível no repositório Magento Connect ou baixar o pacote disponível no site institucional do Yapay.

Instalação do Módulo Magento
{: .subtitulo }

Existem duas formas de realizar a instalação do módulo Magento:

1. Instalação através da Chave da Extensão (**_Extension Key_**)

2. Instalação através do Pacote da Extensão

---

1- Instalação através da Chave da Extensão _(Extension Key)_
{: .subtitulo }

Para instalar módulo é necessário ter a **_extension key_** do módulo, localizada no site do _Magento Connect_. A **_extension key_** do módulo pode ser resgatada através do link:

<a href="http://www.magentocommerce.com/magento-connect/catalog/product/view/id/21274/" class="btn  btn-default btn-wide btn-call-to-action btnMagento"><i class="fa fa-external-link" aria-hidden="true"></i>Magento Connect</a>

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_9.png "Magento Connect, instalação"){: width="100%" height="auto"  }

Após isso, acesse o _Magento Connect Manager_ de sua loja Magento (menu **Sistema > Conexão Magento > Gerenciador de Conexão Magento**), e cole a **_extension key_** do Yapay no campo correspondente da área marcada em vermelho, em seguida clique em **Install**.

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_1.png "Magento Connect, instalação"){: width="100%" height="auto"}

Após a instalação do pacote, será exibido um log semelhante à imagem abaixo:

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_2.png "Magento Connect, instalação"){:width="100%" height="auto"}


Clique no botão **Refresh** e verifique se o módulo **Tray_CheckoutApi** é listado nos módulos instalados, conforme abaixo:

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_6.png "Magento Connect, instalação"){:width="100%" height="auto"}

Clique em **Return to Admin** para voltar à área administrativa de sua loja virtual.

O próximo passo é configurar o módulo (veja o item 3).


2- Instalação através do Pacote da Extensão
{: .subtitulo }

Para instalar o módulo é necessário baixar o arquivo através da página a seguir:

<a href="#" class="btn  btn-default btn-wide btn-call-to-action btnMagento"><i class="fa fa-arrow-circle-down" aria-hidden="true"></i>Magento</a>

Acesse o _Magento Connect Manager_ de sua loja Magento (menu **Sistema > Conexão Magento > Gerenciador de Conexão Magento**), e clique no botão **Selecionar arquivo** da opção _Upload Package File_, conforme imagem abaixo. Selecione o pacote do Yapay baixado anteriormente, em seguida clique em **Upload**.


![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_4.png "Magento Connect, instalação"){:width="100%" height="auto"}

Após a instalação do pacote, será exibido um log semelhante à imagem abaixo:

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_5.png "Magento Connect, instalação"){:width="100%" height="auto"}

Clique no botão **Refresh** e verifique se o módulo **Tray_CheckoutApi** é listado nos módulos instalados, conforme abaixo:

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_6.png "Magento Connect, instalação"){:width="100%" height="auto"}

Clique em **Return to Admin** para voltar à área administrativa de sua loja virtual.

O próximo passo é configurar o módulo (veja o item 3).


3- Configuração do Módulo
{: .subtitulo }

Para utilizar o módulo da API de Pagamento do Yapay é necessário realizar duas etapas:

1. Configurar sua loja virtual para disponibilizar os campos necessários para a integração

2. Configurar o módulo de pagamento Yapay


3.1- Configuração dos Campos de Integração do Magento
{: .subtitulo }

Na integração com a API de Pagamento do Yapay é necessário o envio de alguns campos obrigatórios, onde será necessário disponibilizar estes campos na plataforma Magento.

Para a configuração do módulo, acesse o menu **Sistema > Configuração**, e no menu lateral esquerdo procure por **Configuração do Cliente** (faz parte do sub-menu **Clientes**). Ao clicar no link, serão listados as opções para configuração do cliente na loja virtual, procure pela aba **Opções de Nome e Endereço** para configurar os campos no Magento.

Após abrir a aba **Opções de Nome e Endereço**, encontre a opção **Número de linhas em um endereço de rua** e altere o valor para **4**, onde serão disponibilizados 4 campos para cadastro do endereço, sendo respectivamente o logradouro, número, complemento e bairro.

Após alterar a opção acima, encontre a opção **Exibir número fiscal** e altere a opção para **Obrigatório**, assim será exibida a opção para o cliente informar o CPF no cadastro ou finalização da compra.

Segue abaixo imagem com a tela de configuração dos campos na plataforma Magento:

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_7.png "Magento Connect, instalação"){:width="100%" height="auto"}


3.2- Configuração do Módulo de Pagamento Yapay
{: .subtitulo }

Para a configuração do módulo, acesse o menu **Sistema > Configuração**, e no menu lateral esquerdo procure por **Métodos de Pagamento** (faz parte do sub-menu **Vendas**). Ao clicar no link, será listado todos os métodos de pagamento disponíveis, procure pela aba **Yapay – Transparente** para habilitar e configurar o método de pagamento.

Segue abaixo imagem com a tela de configuração:

![Magento Connect, instalação](/images/intermediador/conteudo/install_magento_8.png "Magento Connect, instalação"){:width="100%" height="auto"}


3.3- Opções de configuração Yapay:
{: .subtitulo }

**Ativado:** opção para habilitar o Yapay na finalização de compra

**Título:** título que aparecerá para seu cliente na hora de escolher a forma de pagamento

**Status dos Novos Pedidos:** status de cada novo pedido ao ser enviado para a Tray

**Token:** chave gerada no seu painel de administração do Yapay, localizado no menu **Perfil da Conta > Minha Conta > Dados da Conta**

**Gerar Fatura automaticamente para pedidos com produtos virtuais:** caso esteja em “Sim”, os pedidos que contiverem ao menos um (1) produto virtual serão automaticamente marcados como “concluídos”, após o recebimento automático do pagamento. Isto se dá em função da não existência da etapa de “Envio” para estes produtos

**Quantidade Máxima de Parcelas:** representa a quantidade máxima de parcelas oferecida pela loja virtual, utilizando o Yapay

**Meios de Pagamento Disponíveis:** Meios de pagamento que serão exibidos para o consumidor ao finalizar a compra pelo Yapay

**Parcelas sem Acréscimo:** as parcelas selecionadas serão exibidas como sem acréscimo ao consumidor quando o mesmo finalizar a compra através do Yapay. Esta opção somente representa a visualização no checkout da loja virtual, onde também é necessário configurar na área administrativa do Yapay (menu **Perfil da Conta > Configurações > Parcelamento de Vendas**)

**Taxa de Acréscimo:** representa o percentual de acréscimo cobrado pelo Yapay

**Prefixo do Pedido:** campo utilizado para concatenar com o número do pedido da loja ao integrar com a Tray

**Ordem de exibição:** ordem de exibição, caso exista mais de um método de pagamento

**Ambiente de Teste (Sandbox):** ambiente utilizado para que a loja possa realizar testes de integração – muita atenção para não manter este ambiente habilitado quando a loja estiver efetivamente vendendo