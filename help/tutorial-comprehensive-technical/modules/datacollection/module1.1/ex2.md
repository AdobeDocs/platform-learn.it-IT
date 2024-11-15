---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Edge Network, flussi di dati e raccolta dati lato server
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Edge Network, flussi di dati e raccolta dati lato server
kt: 5342
doc-type: tutorial
exl-id: e97d40b5-616d-439c-9d6b-eaa4ebf5acb0
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 1.1.2 Edge Network, flussi di dati e raccolta dati lato server

## Contesto

In questo esercizio creerai un **flusso di dati**. Un **datastream** indica ai server Adobe Edge dove inviare i dati dopo che sono stati raccolti dall&#39;SDK Web. Inviare ad esempio i dati a Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target?

Gli stream di dati vengono sempre gestiti nell’interfaccia utente di Adobe Experience Platform Data Collection e sono fondamentali per la raccolta dati di Adobe Experience Platform con Web SDK. Anche quando implementi Web SDK con una soluzione di gestione dei tag non Adobe, dovrai comunque creare lo stream di dati nell’interfaccia utente di Adobe Experience Platform Data Collection.

Il prossimo esercizio illustra l’implementazione dell’SDK per web nel browser. Sarà quindi più chiaro come si presenteranno i dati raccolti. Per il momento, stiamo solo dicendo al Datastream dove inoltrare i dati.

## Creare uno stream di dati

In [Guida introduttiva](./../../../modules/gettingstarted/gettingstarted/ex2.md) hai già creato uno stream di dati, ma non sono stati discussi lo sfondo e il motivo per cui lo stream di dati appartiene.

Un flusso di dati indica ai server di Adobe Edge dove inviare i dati dopo che sono stati raccolti dall’SDK per web. Inviare ad esempio i dati a Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target? Gli stream di dati vengono gestiti nell’interfaccia utente di Adobe Experience Platform Data Collection e sono fondamentali per la raccolta di dati con Web SDK, indipendentemente dal fatto che si stia implementando Web SDK tramite Adobe Experience Platform Data Collection.

Esaminiamo il **[!UICONTROL flusso di dati]**:

Vai a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Fai clic su **[!UICONTROL Datastreams]** nel menu a sinistra.

![Fai clic sull&#39;icona dello stream di dati nell&#39;area di navigazione a sinistra](./images/edgeconfig1.png)

Apri lo stream di dati denominato `--aepUserLdap-- - Demo System Datastream`.

![Denomina lo stream di dati e salva](./images/edgeconfig2.png)

Vengono quindi visualizzati i dettagli dello stream di dati.

![Denomina lo stream di dati e salva](./images/edgecfg1.png)

Fai clic su **...** accanto a **Adobe Experience Platform** e fai clic su **Modifica**.

![Denomina lo stream di dati e salva](./images/edgecfg1a.png)

Poi vedrai questo. Al momento, hai abilitato solo Adobe Experience Platform. La configurazione sarà simile a quella riportata di seguito. (A seconda dell’ambiente e dell’istanza di Adobe Experience Platform, il nome della sandbox potrebbe essere diverso)

![Denomina lo stream di dati e salva](./images/edgecfg2.png)

È necessario interpretare i campi seguenti in questo modo:

Per questo flusso di dati...

- Tutti i dati raccolti verranno memorizzati nella sandbox `--aepSandboxName--` in Adobe Experience Platform
- Tutti i dati di Experience Event vengono raccolti per impostazione predefinita nel set di dati **Demo System - Set di dati evento per il sito Web (Global v1.1)**
- Tutti i dati profilo verranno raccolti per impostazione predefinita nel set di dati **Demo System - Set di dati profilo per il sito Web (Global v1.1)** (l&#39;acquisizione nativa dei dati profilo con Web SDK attualmente non è ancora supportata da Web SDK)
- Se desideri utilizzare il servizio applicativo **Offer Decisioning** per questo flusso di dati, devi selezionare la casella ad Offer decisioning. (farà parte del [modulo 3.3](./../../../modules/ajo-b2c/module3.3/offer-decisioning.md))
- **La segmentazione di Edge** è abilitata per impostazione predefinita, il che significa che i segmenti qualificati verranno valutati al limite al momento dell&#39;acquisizione del traffico in ingresso
- Se desideri utilizzare le **Destinazioni Personalization**, seleziona la casella per Destinazioni Personalization.
- 
   - Se desideri utilizzare le funzionalità di **Adobe Journey Optimizer** in questo flusso di dati, devi selezionare la casella per Adobe Journey Optimizer.


Per il momento, non è necessaria alcuna altra configurazione per lo stream di dati.

Passaggio successivo: [1.1.3 Introduzione alla raccolta dati di Adobe Experience Platform](./ex3.md)

[Torna al modulo 1.1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../../overview.md)
