---
title: 'Hub eventi da Audience Activation a Microsoft Azure: riepilogo e vantaggi'
description: 'Hub eventi da Audience Activation a Microsoft Azure: riepilogo e vantaggi'
kt: 5342
doc-type: tutorial
exl-id: f081af11-3ea0-47cc-ae74-24a0e0231d66
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Riepilogo e vantaggi

Congratulazioni e grazie per aver dedicato il tuo tempo all’apprendimento di Microsoft Azure Event Hub e Adobe Experience Platform.
In questo modulo hai imparato a configurare un’istanza di Azure Event Hub e a connetterla a Adobe Experience Platform.

## Vantaggi

Evidenziamo i vantaggi dell’integrazione di Adobe Experience Platform con Microsoft Azure Event Hub:

- Gli hub eventi di Microsoft Azure come destinazione di Adobe Experience Platform consentono di acquisire in tempo reale le qualifiche del pubblico ed elaborarle utilizzando una funzione dell’hub eventi di Azure. Con tale funzione di Azure Event Hub puoi generare qualsiasi tipo di gestore di attivazione del pubblico personalizzato e come tale integrare qualsiasi tipo di destinazione di terze parti.

- Anche se le destinazioni vengono attivate solo da tipi di pubblico specifici, il payload di attivazione includerà tutti i tipi di pubblico per i quali un determinato profilo è idoneo.

- Un pubblico attiva un’attivazione solo quando il suo stato cambia. Ad esempio, un profilo idoneo quattro volte per un pubblico in un periodo di tre mesi, solo i primi due verranno attivati. Il primo è un cambiamento di stato da a **realizzato**, il secondo è attivato da un cambiamento di stato da **realizzato** a **esistente**.

- Quando si attivano tipi di pubblico per profili noti, nel payload di attivazione viene inclusa una mappa di identità completa. La funzione Azure può utilizzare una qualsiasi delle identità disponibili per mappare i tipi di pubblico a un profilo gestito in un&#39;applicazione di terze parti, utilizzando l&#39;identificatore cliente dell&#39;applicazione.

- In questo modulo, la funzione hub eventi è stata distribuita localmente (modalità di debug in Visual Studio Code), offrendo numerose opzioni di risoluzione dei problemi e debug.

## Guarda qui

- N/D

## Passaggi successivi

Torna a [Real-Time CDP: da Audience Activation a Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
