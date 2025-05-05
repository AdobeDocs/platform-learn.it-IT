---
title: Hub eventi da Audience Activation a Microsoft Azure - Attiva pubblico
description: Hub eventi da Audience Activation a Microsoft Azure - Attiva pubblico
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%

---

# 2.4.5 Attivare il pubblico

## Aggiungi pubblico alla destinazione dell’hub eventi di Azure

In questo esercizio aggiungerai il pubblico `--aepUserLdap-- - Interest in Plans` alla destinazione dell&#39;hub eventi di Azure `--aepUserLdap---aep-enablement`.

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Vai a **Destinazioni**, quindi fai clic su **Sfoglia**. Vedrai quindi tutte le destinazioni disponibili. Individua la destinazione e fai clic sui tre punti&#x200B;**...** come indicato di seguito, quindi fai clic su **Attiva pubblico**.

![5-01-select-destination.png](./images/501selectdestination.png)

Poi vedrai questo. Cerca il tuo pubblico utilizzando il tuo ldap e seleziona `--aepUserLdap-- - Interest in Plans` dall&#39;elenco dei tipi di pubblico.

Fai clic su **Avanti**.

![5-04-select-segment.png](./images/504selectsegment.png)

Fai clic su **Aggiungi nuovo campo**, fai clic su Sfoglia schema e seleziona il campo `--aepTenantId--identification.core.ecid` (elimina qualsiasi altro campo che verrebbe visualizzato automaticamente).

Fai clic su **Avanti**.

![5-05-select-attributes.png](./images/505selectattributes.png)

Fai clic su **Fine**.

![5-06-destination-finish.png](./images/506destinationfinish.png)

Il pubblico ora è attivato verso la destinazione dell’hub eventi di Microsoft.

![5-07-destination-segment-ADDED.png](./images/507destinationsegmentadded.png)

## Passaggi successivi

Vai a [2.4.6 Creare il progetto Microsoft Azure](./ex6.md){target="_blank"}

Torna a [Real-Time CDP: da Audience Activation a Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
