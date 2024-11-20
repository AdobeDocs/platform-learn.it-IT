---
title: Real-time CDP - Creazione di un pubblico e intervento - Invio del pubblico a DV360
description: Real-time CDP - Creazione di un pubblico e intervento - Invio del pubblico a DV360
kt: 5342
doc-type: tutorial
exl-id: bb76524e-52c1-4c2c-8bcd-33cd39d12741
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 1%

---

# 2.3.3 Intervenire: inviare il pubblico a DV360

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Sfoglia**. Verrà quindi visualizzata la destinazione **DV360**. Fai clic sui tre punti **...** e fai clic su **Attiva pubblico**.

![RTCDP](./images/rtcdpmenudest.png)

Nell’elenco dei tipi di pubblico disponibili, seleziona il pubblico creato nell’esercizio precedente. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest3.png)

Nella pagina **Pianificazione pubblico**, fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest4.png)

Infine, nella pagina **Revisione**, fare clic su **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Il pubblico è ora collegato a Google DV360. Ogni volta che un cliente si qualifica per questo pubblico, viene inviato un segnale a Google DV360 per includere tale cliente nel pubblico di Google DV360 side.

Passaggio successivo: [2.3.4 Intervenire: inviare il pubblico a una destinazione S3](./ex4.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)
