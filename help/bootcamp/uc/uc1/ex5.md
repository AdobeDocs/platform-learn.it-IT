---
title: Bootcamp - Real-time CDP - Creare un pubblico e intervenire - Inviare il pubblico a DV360
description: Bootcamp - Real-time CDP - Creare un pubblico e intervenire - Inviare il pubblico a DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# 1.5 Intervenire: inviare il pubblico a Facebook

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Verrà quindi visualizzato il **Catalogo destinazioni**. In **Destinazioni**, fai clic su **Attiva tipi di pubblico** nella scheda **Pubblico personalizzato di Facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Seleziona la destinazione **bootcamp-facebook** e fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest2.png)

Nell’elenco dei tipi di pubblico disponibili, seleziona il pubblico creato nell’esercizio precedente. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest3.png)

Nella pagina **Mapping**, verificare che la casella di controllo **Applica trasformazione** sia abilitata. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Nella pagina **Pianificazione pubblico**, seleziona **Origine del pubblico** e impostala su **Direttamente dai clienti**. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4.png)

Infine, nella pagina **Revisione**, fare clic su **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Il pubblico è ora collegato ai tipi di pubblico personalizzati di Facebook. Ogni volta che un cliente si qualifica per questo pubblico, viene inviato un segnale a Facebook lato server per includere tale cliente nel pubblico personalizzato sul lato Facebook.

In Facebook, il pubblico si trova in Adobe Experience Platform in Tipi di pubblico personalizzati:

![RTCDP](./images/rtcdpcreatedest5b.png)

Ora puoi visualizzare il pubblico personalizzato in Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
