---
title: 'Audience Activation dell’hub eventi di Microsoft Azure: attiva pubblico'
description: 'Audience Activation dell’hub eventi di Microsoft Azure: attiva pubblico'
kt: 5342
doc-type: tutorial
exl-id: 89cfda0e-6c5e-45ab-9506-f0f0f6211e7f
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 2%

---

# 2.4.5 Attivare il pubblico

## Aggiungi pubblico alla destinazione dell’hub eventi di Azure

In questo esercizio aggiungerai il pubblico `--aepUserLdap-- - Interest in Equipment` alla destinazione dell&#39;hub eventi di Azure `--aepUserLdap---aep-enablement`.

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Vai a **Destinazioni**, quindi fai clic su **Sfoglia**. Vedrai quindi tutte le destinazioni disponibili. Individua la destinazione e fai clic sui tre punti**...** come indicato di seguito, quindi fai clic su **Attiva pubblico**.

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

Passaggio successivo: [2.4.6 Creare il progetto Microsoft Azure](./ex6.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
