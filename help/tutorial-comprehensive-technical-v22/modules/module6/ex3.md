---
title: Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360
description: Real-time CDP - Creare un segmento e intervenire - Inviare il segmento a DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7a78260f-cd25-4ed0-801b-87174babaffe
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# 6.3 Intervenire: inviare il segmento a DV360

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](../module2/images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Vedrai il **Catalogo delle destinazioni**.

![RTCDP](./images/rtcdpmenudest.png)

In **Destinazioni**, fai clic su **Attiva segmenti** sulla **Display Google e video 360** il Card.

![RTCDP](./images/rtcdpgoogleseg.png)

Seleziona la destinazione e fai clic su **Successivo**.

![RTCDP](./images/rtcdpcreatedest2.png)

Nell’elenco dei segmenti disponibili, seleziona il segmento creato nell’esercizio precedente. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpcreatedest3.png)

Sulla **Pianificazione del segmento** pagina, fai clic su **Successivo**.

![RTCDP](./images/rtcdpcreatedest4.png)

Infine, **Revisione** pagina, fai clic su **Fine**.

![RTCDP](./images/rtcdpcreatedest5.png)

Il segmento è ora collegato a Google DV360. Ogni volta che un cliente si qualifica per questo segmento, verrà inviato un segnale a Google DV360 per includere tale cliente nel pubblico sul lato Google DV360.

Passaggio successivo: [6.4 Intervenire: invia il segmento a una destinazione S3](./ex4.md)

[Torna al modulo 6](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../overview.md)
