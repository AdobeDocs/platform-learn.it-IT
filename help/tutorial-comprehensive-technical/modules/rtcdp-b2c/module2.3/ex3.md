---
title: Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360
description: Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 1%

---

# 2.3.3 Intervenire: inviare il segmento a DV360

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Verrà quindi visualizzato il **Catalogo destinazioni**.

![RTCDP](./images/rtcdpmenudest.png)

In **Destinazioni**, fai clic su **Attiva segmenti** nella scheda **Google Display &amp; Video 360**.

![RTCDP](./images/rtcdpgoogleseg.png)

Seleziona la destinazione e fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest2.png)

Nell’elenco dei segmenti disponibili, seleziona il segmento creato nell’esercizio precedente. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest3.png)

Nella pagina **Pianificazione segmento**, fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4.png)

Infine, nella pagina **Revisione**, fare clic su **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Il segmento è ora collegato a Google DV360. Ogni volta che un cliente si qualifica per questo segmento, viene inviato un segnale a Google DV360 per includere tale cliente nel pubblico di Google DV360.

Passaggio successivo: [2.3.4 Intervenire: inviare il segmento a una destinazione S3](./ex4.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)
