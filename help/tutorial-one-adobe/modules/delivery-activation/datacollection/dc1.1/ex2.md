---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Edge Network, Datastreams e Server Side Data Collection
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Edge Network, Datastreams e Server Side Data Collection
kt: 5342
doc-type: tutorial
exl-id: f805b2a6-c813-4734-8a78-f8588ecd0683
source-git-commit: 31466040336580e9e4b2308801347dc387be4da5
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 1%

---

# 1.1.2 Edge Network, flussi di dati e raccolta dati lato server

## Contesto

In questo esercizio creerai un **flusso di dati**. Un **datastream** indica ai server Adobe Edge Network dove inviare i dati dopo che sono stati raccolti da Web SDK. Inviare ad esempio i dati a Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target?

Gli stream di dati vengono sempre gestiti nell&#39;interfaccia utente di Experience Platform Data Collection e sono fondamentali per la raccolta dati di Experience Platform con [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home). Anche quando si implementa Web SDK con una soluzione di gestione dei tag non Adobe, è comunque necessario creare un flusso di dati.

Nel prossimo esercizio, implementerai il Web SDK nel browser. Sarà quindi più chiaro come si presenteranno i dati raccolti. Per il momento, stiamo solo indicando al flusso di dati dove inoltrare i dati.

## Creare un flusso di dati

In [Guida introduttiva](./../../../../modules/getting-started/gettingstarted/ex2.md) hai già creato uno stream di dati, ma non sono stati discussi lo sfondo e il motivo per cui lo hai creato.

Un [datastream](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) indica ai server Edge Network dove inviare i dati dopo che sono stati raccolti dal Web SDK. Per informazioni dettagliate su dove puoi inviare i dati tramite lo stream di dati, consulta la documentazione di [aggiunta di servizi a uno stream di dati](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure#add-services).

Gli stream di dati vengono gestiti nell’interfaccia utente di Experience Platform Data Collection e sono fondamentali per la raccolta dei dati con Web SDK, indipendentemente dal fatto che si stia implementando Web SDK tramite Adobe Experience Platform Data Collection.

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
- Tutti i dati profilo verranno raccolti per impostazione predefinita nel set di dati **Demo System - Set di dati profilo per il sito Web (Global v1.1)** (l&#39;acquisizione nativa dei dati profilo con Web SDK non è ancora supportata da Web SDK)
- **La segmentazione di Edge** è abilitata per impostazione predefinita, il che significa che i tipi di pubblico idonei verranno valutati al limite, al momento dell&#39;acquisizione del traffico in ingresso
- Se desideri utilizzare [destinazioni di personalizzazione](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/overview), seleziona la casella per **Destinazioni Personalization**.
- Se desideri utilizzare le funzionalità di **Adobe Journey Optimizer** in questo flusso di dati, devi selezionare la casella per **Adobe Journey Optimizer**.

Per il momento, non è necessaria alcuna altra configurazione per lo stream di dati.

## Passaggi successivi

Vai a [1.1.3 Introduzione alla raccolta dati di Adobe Experience Platform](./ex3.md){target="_blank"}

Torna a [Configurazione della raccolta dati di Adobe Experience Platform ed estensione tag Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
