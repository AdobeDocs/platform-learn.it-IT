---
title: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360 - Brasile
description: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360 - Brasile
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Ação: envie seu para o Facebook

[Adobe Experience Platform](https://experience.adobe.com/platform). Accesso Depois de fazer, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, vá para **Destinazioni** e, em seguida, vá para **Catalogo**. Você verá o **Catalogo delle destinazioni**. **Destinazioni**, Cricca em **Attiva segmenti** senza cartone **Pubblico personalizzato Facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Selecione o **bootcamp-facebook** e cricca em **Successivo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, selecione o você criou no exercício anteriore. **Avanti**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mappatura**, verifica se a caixa de seleção **Applica trasformazione** está marcada. **Avanti**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **Pianificazione segmento**, seleziona una **Origine del pubblico** e definisce un como **Direttamente dai clienti**. **Avanti**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, na página **Recensione**, cricca em **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se qualificar para esse, um sinal será enviado ao lado do servidor (lato server) do Facebook para incluir esse cliente no Público Personalizado no lado do Facebook.

Niente Facebook, voce encontrará seu da Adobe Experience Platform em Públicos Personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público personalizado aparecer no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
