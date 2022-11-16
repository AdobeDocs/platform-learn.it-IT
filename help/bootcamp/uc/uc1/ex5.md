---
title: Bootcamp - Real-time CDP - Costruire un segmento e agire - Invia il segmento a DV360
description: Bootcamp - Real-time CDP - Costruire un segmento e agire - Invia il segmento a DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Intervenire: inviare il segmento a Facebook

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Vedrai il **Catalogo delle destinazioni**. In **Destinazioni**, fai clic su **Attiva segmenti** sulla **Pubblico personalizzato facebook** il Card.

![RTCDP](./images/rtcdpgoogleseg.png)

Selezionare la destinazione **bootcamp-facebook** e fai clic su **Successivo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Nell’elenco dei segmenti disponibili, seleziona il segmento creato nell’esercizio precedente. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest3.png)

Sulla **Mappatura** assicurati che **Applica trasformazione** la casella di controllo è abilitata. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Sulla **Pianificazione del segmento** , seleziona la **Origine del pubblico** e impostarlo su **Direttamente dai clienti**. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4.png)

Infine, **Revisione** pagina, fai clic su **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Il segmento è ora collegato a tipi di pubblico personalizzati di Facebook. Ogni volta che un cliente si qualifica per questo segmento, viene inviato un segnale al server Facebook per includere tale cliente nel pubblico personalizzato sul lato Facebook.

In Facebook, troverai il segmento da Adobe Experience Platform in Tipi di pubblico personalizzati :

![RTCDP](./images/rtcdpcreatedest5b.png)

Ora puoi vedere il pubblico personalizzato visualizzato in Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Torna al flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
