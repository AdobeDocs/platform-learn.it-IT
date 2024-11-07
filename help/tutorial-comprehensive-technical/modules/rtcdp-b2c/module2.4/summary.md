---
title: 'Attivazione dei segmenti nell’hub eventi di Microsoft Azure: riepilogo e vantaggi'
description: 'Attivazione dei segmenti nell’hub eventi di Microsoft Azure: riepilogo e vantaggi'
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# Riepilogo e vantaggi

Congratulazioni e grazie per aver dedicato il tuo tempo all’apprendimento di Microsoft Azure Event Hub e Adobe Experience Platform.
In questo modulo hai imparato a configurare un’istanza di Azure Event Hub e a connetterla a Adobe Experience Platform.

## Vantaggi

Evidenziamo i vantaggi dell’integrazione di Adobe Experience Platform con Microsoft Azure Event Hub:

- Gli hub eventi di Microsoft Azure come destinazione di Adobe Experience Platform consentono di acquisire la qualifica dei segmenti in tempo reale ed elaborarli utilizzando una funzione dell’hub eventi di Azure. Con tale funzione di Azure Event Hub puoi generare qualsiasi tipo di gestore di attivazione dei segmenti personalizzato e come tale integrare qualsiasi tipo di destinazione di terze parti.

- Anche se le destinazioni vengono attivate solo dai segmenti specificati, il payload di attivazione includerà tutti i segmenti per i quali un determinato profilo è idoneo.

- Un segmento attiva un’attivazione solo quando il suo stato cambia. Ad esempio, un profilo idoneo quattro volte per un segmento in un periodo di tre mesi, verranno attivati solo i primi due. Il primo è un cambiamento di stato da a **realizzato**, il secondo è attivato da un cambiamento di stato da **realizzato** a **esistente**.

- Quando si attivano segmenti per profili noti, nel payload di attivazione viene inclusa una mappa di identità completa. La funzione Azure può utilizzare una qualsiasi delle identità disponibili per mappare i segmenti su un profilo gestito in un’applicazione di terze parti, utilizzando al contempo l’identificatore cliente dell’applicazione.

- In questo modulo, la funzione hub eventi è stata distribuita localmente (modalità di debug in Visual Studio Code), offrendo numerose opzioni di risoluzione dei problemi e debug.

## Guarda qui

- N/D

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
