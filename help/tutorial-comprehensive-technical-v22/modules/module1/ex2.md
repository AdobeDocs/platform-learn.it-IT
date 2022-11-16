---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell'estensione Web SDK - Edge Network, Datastreams e Server Side Data Collection
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell'estensione Web SDK - Edge Network, Datastreams e Server Side Data Collection
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6f7c540f-3804-483d-90f9-b26b4a252b8b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 2%

---

# 1.2 Rete Edge, Datastreams e raccolta dati lato server

## Contesto

In questo esercizio creerai un **Datastream**. A **Datastream** indica ai server Adobe Edge dove inviare i dati dopo essere stati raccolti dall’SDK per web. Ad esempio, si desidera inviare i dati a Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target?

I Datastreams sono sempre gestiti nell’interfaccia utente di raccolta dati di Adobe Experience Platform e sono fondamentali per la raccolta dati di Adobe Experience Platform con l’SDK per web. Anche quando implementi l’SDK web con una soluzione di gestione tag non Adobe, dovrai comunque creare il tuo Datastream nell’interfaccia utente di Adobe Experience Platform Data Collection.

Nel prossimo esercizio implementerai l&#39;SDK per web nel browser. Sarà quindi più chiaro a voi come saranno i dati raccolti. Per ora, stiamo solo dicendo al Datastream dove inoltrare i dati.

## Creare un archivio dati

In [Esercizio 0.2](./../module0/ex2.md) hai già creato un Datastream, ma non abbiamo discusso lo sfondo e la ragione per essere del Datastream.

Un Datastream indica ai server Adobe Edge dove inviare i dati dopo essere stati raccolti dall&#39;SDK Web. Ad esempio, si desidera inviare i dati a Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target? I Datastreams sono gestiti nell’interfaccia utente di raccolta dati di Adobe Experience Platform e sono fondamentali per la raccolta dati di Platform con l’SDK per web, indipendentemente dal fatto che si stia implementando l’SDK per web tramite la raccolta dati di Adobe Experience Platform.

Rivediamo il tuo **[!UICONTROL Datastream]**:

Vai a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Fai clic su **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]** nel menu a sinistra.

![Fai clic sull’icona Datastream nella navigazione a sinistra](./images/edgeconfig1.png)

Cerca il tuo Datastream, che si chiama `--demoProfileLdap-- - Demo System Datastream`.

![Assegna un nome al Datastream e salva](./images/edgeconfig2.png)

Vedrai i dettagli del tuo Datastream.

![Assegna un nome al Datastream e salva](./images/edgecfg1.png)

Fai clic su **...** accanto a **Adobe Experience Platform** e fai clic su **Modifica**.

![Assegna un nome al Datastream e salva](./images/edgecfg1a.png)

Vedrete questo. Al momento, hai abilitato solo Adobe Experience Platform. La configurazione sarà simile a quella riportata di seguito. (A seconda dell’ambiente e dell’istanza di Adobe Experience Platform, il nome della sandbox potrebbe essere diverso)

![Assegna un nome al Datastream e salva](./images/edgecfg2.png)

È necessario interpretare i campi seguenti come questo:

Per questo datastream...

- Tutti i dati raccolti verranno memorizzati nel `--aepSandboxId--` sandbox in Adobe Experience Platform
- Tutti i dati dell’evento esperienza vengono raccolti per impostazione predefinita nel set di dati **Sistema di demo - Set di dati evento per il sito web (Global v1.1)**
- Tutti i dati del profilo verranno raccolti per impostazione predefinita nel set di dati **Sistema di demo - Set di dati di profilo per il sito web (Global v1.1)** (l’acquisizione dei dati di profilo in modo nativo con SDK per web al momento non è ancora supportata dall’SDK per web e sarà resa disponibile in un secondo momento)
- Se desideri utilizzare il **offer decisioning** servizio applicazione per questo Datastream, è necessario selezionare la casella per Offer decisioning. (farà parte di [Modulo 9](./../module9/offer-decisioning.md))
- Se desideri utilizzare il **Segmentazione Edge**, è necessario selezionare la casella Segmentazione bordo.
- Se desideri utilizzare il **Destinazioni personalizzazione**, devi selezionare la casella per Destinazioni personalizzazione.

Per il momento, non sono necessarie altre configurazioni per il Datastream.

Passaggio successivo: [1.3 Introduzione alla raccolta dati di Adobe Experience Platform](./ex3.md)

[Torna al modulo 1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../overview.md)
