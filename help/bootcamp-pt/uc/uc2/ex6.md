---
title: Bootcamp - Personalizzazione nel call center - Brasile
description: Bootcamp - Personalizzazione nel call center - Brasile
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 7acf778b-042f-4deb-9406-ddcf63daacda
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 2.6 Personalização nessun call center

Conforme discutido várias vezes durante o bootcamp, personalizar a experiência do cliente é algo que deve acontecer de maneira omnichannel. Il call center geralmente é bastante desconectado do restante da jornada do cliente e isso pode, com frequência, levar a experiências fruantes do cliente, mas não ser assim. Vamos mostrar um exemplo de como o call center pode facilmente conectado à Adobe Experience Platform, em tempo real.

## Fluxo da jornada do cliente

Nessun exercício anteriore, o aplicativo móvel, você comprou um produto clicando no botão **Acquista**.

![DSN](./images/app20.png)

Vamos supor que você tenha uma pergunta sobre o status do seu pedido, o que você faria? Normalmente, você ligaria para o call center.

Antes de ligar para o call center, você saber seu **ID fedeltà**. Você pode encontrar seu ID de fidelidade no Visualizador de Perfil do site.

![DSN](./images/cc1.png)

Nesse caso, o **ID fedeltà** é **5863105**. Como parte de nossa implementação personalizada do recurso de call center no ambiente de dimostração, você deve adicionar um prefixo ao seu **ID fedeltà**. O prefisso é **11373**, portanto, o ID de fidelidade a ser usado neste exemplo é **5863105 11373**.

Vamos fazer è agorà. Usa telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Será solicitado que você insira seu ID de fidelidade, seguido de **N.**. Digite seu ID de fidelidade.

![DSN](./images/cc3.png)

Você ouvirá **Ciao, seu nome**. Esse nome é retirado do Perfil do Cliente em tempo real na Adobe Experience Platform. Você punto 3 escolha. Pressione o número **1**, **Stato ordine**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu pedido, você terá a opção de pressionar **1** para voltar ao menu principal ou pressionar 2. Pressione **2**.

![DSN](./images/cc5.png)

Em seguida, será solicitado que você avalie sua experiência de call center, selecionando um número entre 1 e 5, sendo 1 baixo e 5 alto. Face a sua escolha.

![DSN](./images/cc6.png)

Sua chamada para o call center será encerrada.

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Accesso Depois de fazer, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É possível fazer isso clicando no texto **[!UICONTROL Prod produzione]** è una linha azul na parte superior da tela. Depois de selecionar o [!UICONTROL sandbox] apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, acesse **Profili** e **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Selecione o **Spazio dei nomi dell’identità** **E-mail** e insira o endereço de e-mail do seu perfil de cliente. Clique em **Visualizza**. Cricca para abrir seu perfil.

![DSN](./images/cc7.png)

Você verá seu perfil de cliente novamente. Acesse **Eventi**.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **callCenter**. O primeiro evento é o resultado da sua resposta à pergunta **Valuta la soddisfazione della tua chiamata** (avalie seu chamada).

![DSN](./images/cc9.png)

Ruolo um pouco para baixo e você verá o evento que foi registrado quando você selecionou a opção de verificar o **Stato ordine**.

![DSN](./images/cc10.png)

Acesse **Iscrizione al segmento**. Agora você verá que 2 segmentos se qualificam em seu perfil, em tempo real, com base nas interações que você teve por meio do call center. Essas associações de podem e devem ser usadas para impactar qual comunicação e personalização acontece em qualquer canale esterno.

![DSN](./images/cc11.png)

Você terminou este exercício

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
