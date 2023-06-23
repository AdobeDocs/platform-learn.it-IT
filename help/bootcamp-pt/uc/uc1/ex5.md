---
title: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360 - Brasile
description: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360 - Brasile
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Ação: envie seu para o Facebook

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Accesso Depois de fazer, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Prod produzione]** è una linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, vá para **Destinazioni** e, em seguida, vá para **Catalogo**. Você verá o **Catalogo delle destinazioni**. Em **Destinazioni**, cricca em **Attivare segmenti** nessun cartone **Pubblico personalizzato facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Selecione o **bootcamp-facebook** e cricca em **Successivo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, selecione o você criou no exercício anteriore. Clique em **Successivo**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mappatura**, verifique se a caixa de seleção **Applica trasformazione** está marcada. Clique em **Successivo**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **Pianificazione segmento**, selecione a **Origine del pubblico** e defina como **Direttamente dai clienti**. Clique em **Successivo**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, na página **Revisione**, cricca em **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se qualificar para esse, um sinal será enviado ao lado do servidor (lato server) do Facebook para incluir esse cliente no Público Personalizado no lado do Facebook.

Niente Facebook, voce encontrará seu da Adobe Experience Platform em Públicos Personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público personalizado aparecer no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
