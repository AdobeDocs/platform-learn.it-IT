---
title: Bootcamp - Personalizzazione nel call center - Brasile
description: Bootcamp - Personalizzazione nel call center - Brasile
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 2.6 Personalizzazione senza call center

Conforme discussione várias vezes durante o bootcamp, personalizza un experiência do clienti é algo que deve acontecer de maneira omnichannel. Um call center geralmente é bastante desconectado do fermoda jornada do cliente e isso pode, com frequência, levar a experiências frustrantes do cliente, mas não precisa ser assim. Vamos mostrar um exemplo call center pode ser conectado à Adobe Experience Platform, em tempo real.

## Fluxo da jornada do cliente

No exercício anteriore, o aplicativo móvel, você comprou um produto clicando no botão **Acquista**.

![DSN](./images/app20.png)

Vamos supor que você tenha uma pergunta sobre o status do seu pedido, o que você faria? Normalmente, você ligaria para o call center.

Antes de ligar para o call center, você precisa saber seu **ID fedeltà**. Você pode encontrar seu ID de fidelidade no Visualizador de Perfil do site.

![DSN](./images/cc1.png)

Nesse Cio, o **ID fedeltà** é **5863105**. Como parte de nossa implementação personalizada do ricorso de call center no ambiente de dimostração, você dev adicionar um prefixo ao seu **ID fedeltà**. O prefixo é **11373**, portanto, o ID de fidelidade a ser usado neste exemplo é **11373 5863105**.

Vamos fazer isso agora. Usa seu telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Será solicitado que você insira seu ID de fidelidade, seguido de **#**. Digite seu ID de fidelidade.

![DSN](./images/cc3.png)

Você ouvirá **Ciao, nome del seu**. Esse nome é retirado do Perfil do Cliente tempo reale na Adobe Experience Platform. Você tem 3 escolide. Pressione o número **1**, **Stato dell&#39;ordine**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu pedido, você terá a opção de pressionar **1** para voltar ao menù principal ou pressionar 2. ssione **2**.

![DSN](./images/cc5.png)

Em seguida, será solicitado que você avalie sua experiência de call center, selecionando um número entre 1 e 5, sendo 1 baixo e 5 alto. Faça a sua escolha.

![DSN](./images/cc6.png)

Sura chamada para o call center será encerrada.

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você precisa selionar um **sandbox**. O nome do sandbox un utente selionado é ``Bootcamp``. É possível fazer isso clicando nessun texto **[!UICONTROL Produzione Prod]** na linha azul na parte superior da tela. Depois de selionar o [!UICONTROL sandbox] apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedica.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, acesse **Profili** e **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Selecione o **Spazio dei nomi identità** **E-mail** e insira o endereço de e-mail do seu perfil de cliente. Clipart **Visualizza**. Clique para abrir seu perfil.

![DSN](./images/cc7.png)

Você verá seu perfil de cliente novamente. Acesse **Eventi**.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **callCenter**. O primeiro evento é o risultante da sua resposta à pergunta **Valuta la tua soddisfazione di chiamata** (avalie seu chamada).

![DSN](./images/cc9.png)

Ruolo um pouco para baixo e você verá o evento que foi registrado quando você selion ou a opção de verify o **Stato dell&#39;ordine**.

![DSN](./images/cc10.png)

Acesse **Iscrizione al segmento**. Agora você verá que 2 segmentos se Qualam em seu perfil, em tempo real, com base nas interações que você teve por meio do call center. Essas associações de segmento podem e devem ser usadas para impactar qual comunicação e personalização ação acontece em qualquer outro canal.

![DSN](./images/cc11.png)

Você terminou este exercício.

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
