---
title: Attivazione segmento in Microsoft Azure Event Hub - Attiva segmento
description: Attivazione segmento in Microsoft Azure Event Hub - Attiva segmento
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---

# 2.4.4 Attiva segmento

## 2.4.4.1 Aggiungere un segmento alla destinazione dell’hub eventi di Azure

In questo esercizio aggiungerai il segmento `--aepUserLdap-- - Interest in Equipment` alla destinazione dell&#39;hub eventi di Azure `--aepUserLdap---aep-enablement`.

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Vai a **Destinazioni**, quindi fai clic su **Sfoglia**. Vedrai quindi tutte le destinazioni disponibili. Individua la destinazione e fai clic sull&#39;icona **+** come indicato di seguito.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Poi vedrai questo. Cerca il tuo segmento utilizzando il tuo ldap e seleziona `--aepUserLdap-- - Interest in Equipment` dall&#39;elenco dei segmenti.

Fai clic su **Avanti**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform Real-time CDP può fornire un payload a due tipi di destinazioni, segmenti e profili.

Le destinazioni dei segmenti riceveranno un payload di qualificazione dei segmenti predefinito, che verrà discusso in seguito. Tale payload contiene **all** le qualifiche del segmento per un profilo specifico. Anche per i segmenti che non sono nell’elenco di attivazione della destinazione. Un esempio di tale destinazione di segmento è **Azure Event Hubs** e **AWS Kinesis**.

Le destinazioni basate su profilo consentono di scegliere qualsiasi attributo (firstName, lastName, ...) dallo schema di unione profili XDM e di includerlo nel payload di attivazione. Un esempio di tale destinazione è l&#39;**Email Marketing**.

Poiché la destinazione dell&#39;hub eventi di Azure è una destinazione **segmento**, selezionare ad esempio il campo `--aepTenantId--.identification.core.ecid`.

Fai clic su **Aggiungi nuovo campo**, fai clic su Sfoglia schema e seleziona il campo `--aepTenantId--identification.core.ecid` (elimina qualsiasi altro campo che verrebbe visualizzato automaticamente).

Fai clic su **Avanti**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Fai clic su **Fine**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

Il segmento è ora attivato verso la destinazione dell’hub eventi di Microsoft.

![5-07-destination-segment-ADDED.png](./images/5-07-destination-segment-added.png)

Passaggio successivo: [2.4.5 Creare il progetto Microsoft Azure](./ex5.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
