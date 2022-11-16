---
title: Attivazione del segmento nell’hub eventi di Microsoft Azure - Riepilogo e vantaggi
description: Attivazione del segmento nell’hub eventi di Microsoft Azure - Riepilogo e vantaggi
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2174ac52-b5dd-4bc8-ab5f-4d84ae9ef19b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# Riepilogo e vantaggi

Congratulazioni e grazie per aver investito il tuo tempo nell’apprendimento di Microsoft Azure Event Hub e Adobe Experience Platform!
In questo modulo hai imparato a configurare un’istanza di Azure Event Hub e a come connetterla a Adobe Experience Platform.

## Vantaggi

Evidenziamo i vantaggi dell’integrazione di Adobe Experience Platform con Microsoft Azure Event Hub:

- Gli hub eventi di Microsoft Azure come destinazione Adobe Experience Platform consentono di acquisire la qualificazione dei segmenti in tempo reale ed elaborarli utilizzando una funzione di Azure Event Hub. Con questa funzione di Azure Event Hub puoi creare qualsiasi tipo di gestore di attivazione di segmenti personalizzati e, come tale, integrare qualsiasi tipo di destinazione di terze parti.

- Anche se le destinazioni vengono attivate solo da segmenti specifici, il payload di attivazione includerà tutti i segmenti per i quali un determinato profilo è idoneo.

- Un segmento attiva un’attivazione solo quando il suo stato cambia. Ad esempio, un profilo che si qualifica quattro volte per un segmento in un periodo di tre mesi, verranno attivati solo i primi due. Il primo è un cambiamento di stato da a **realizzato**, il secondo viene attivato da una modifica dello stato da **realizzato** a **esistente**.

- Quando si attivano i segmenti per i profili noti, nel payload di attivazione viene inclusa una mappa di identità completa. La funzione Azure può utilizzare una qualsiasi delle identità disponibili per mappare i segmenti su un profilo gestito in un’applicazione di terze parti, utilizzando l’identificatore cliente dell’applicazione.

- In questo modulo, la funzione di hub eventi è stata implementata localmente (modalità di debug in Visual Studio Code), offrendo molte opzioni di risoluzione dei problemi e debug.

## Controlla questo

- N/D

[Torna al modulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../overview.md)
