---
title: Bootcamp - Real-time CDP - Costruire un segmento e agire - Invia il segmento a DV360 - Brasile
description: Bootcamp - Real-time CDP - Costruire un segmento e agire - Invia il segmento a DV360 - Brasile
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Ação: invidia seu segmento para o Facebook

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você precisa selionar um **sandbox**. O nome fare sandbox un ser selionado é Bootcamp. É possível fazer isso clicando nessun texto **[!UICONTROL Produzione Prod]** na linha azul na parte superior da tela. depois de selionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedica.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, vá para **Destinazioni** e, em seguida, vá para **Catalogo**. Você verá o **Catalogo delle destinazioni**. Em **Destinazioni**, clique em **Attiva segmenti** no cartão **Pubblico personalizzato facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Selecione o **bootcamp-facebook** e clique em **Successivo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, selione o segmento que você criou no exercício anteriore. Clipart **Successivo**.

![RTCDP](./images/rtcdpcreatedest3.png)

Página **Mappatura**, verificabile se a caixa de seleção **Applica trasformazione** está marcada. Clipart **Successivo**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Página **Pianificazione del segmento**, seleziona a **Origine del pubblico** e defina como **Direttamente dai clienti**. Clipart **Successivo**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, na página **Revisione**, clique em **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente Qualar para esse segmento, um sinal será enviado ao lado do servdor (lato server) do Facebook para incluir esse cliente no Público Personalizado no lado do do Facebook.

No Facebook, você encontrará seu segmento da Adobe Experience Platform em Públicos Personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público personalizado aparecer no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
