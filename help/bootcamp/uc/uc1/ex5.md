---
title: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360
description: Bootcamp - Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Intervenire: inviare il segmento a Facebook

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, è necessario selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella linea blu sopra lo schermo. Dopo aver selezionato la [!UICONTROL sandbox], verrà visualizzata la modifica dello schermo e ora si è nel [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Vedrai quindi il **Catalogo delle destinazioni**. In entrata **Destinazioni**, fai clic su **Attivare segmenti** il **Pubblico personalizzato facebook** Card.

![RTCDP](./images/rtcdpgoogleseg.png)

Seleziona la destinazione **bootcamp-facebook** e fai clic su **Successivo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Nell’elenco dei segmenti disponibili, seleziona il segmento creato nell’esercizio precedente. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest3.png)

Il giorno **Mappatura** , assicurati che il **Applica trasformazione** la casella di controllo è attivata. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Il giorno **Pianificazione segmento** , seleziona la **Origine del pubblico** e impostarlo su **Direttamente dai clienti**. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4.png)

Infine, sulla **Revisione** pagina, fai clic su **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Il segmento ora è collegato ai tipi di pubblico personalizzati di Facebook. Ogni volta che un cliente si qualifica per questo segmento, viene inviato un segnale a Facebook lato server per includere tale cliente nel pubblico personalizzato sul lato Facebook.

In Facebook, il segmento proveniente da Adobe Experience Platform è disponibile in Tipi di pubblico personalizzati:

![RTCDP](./images/rtcdpcreatedest5b.png)

Ora puoi visualizzare il pubblico personalizzato in Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
