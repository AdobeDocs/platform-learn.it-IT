---
title: Attivazione segmento nell’hub eventi di Microsoft Azure
description: Attivazione segmento nell’hub eventi di Microsoft Azure
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 2.4 Real-Time CDP: attivazione dei segmenti in Microsoft Azure Event Hub

**Autori: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo verrà impostata una destinazione Microsoft Azure EventHub come destinazione in tempo reale per Adobe Experience Platform Real-time CDP. Puoi anche configurare e distribuire una funzione di Azure che verrà attivata in tempo reale ogni volta che Adobe Experience Platform distribuisce un payload di segmento alla destinazione di Azure EventHub. La funzione di Azure che verrà attivata mostrerà il meccanismo delle funzionalità di attivazione di Adobe Experience Platform Real-time CDP.

Come parte di questo modulo, comprenderai anche cosa attiva Real-time CDP per consegnare effettivamente un payload a una destinazione specifica. Vengono inoltre illustrati lo stato di qualificazione di un segmento e il modo in cui si relaziona all’attivazione.

Adobe Experience Platform Real-time CDP supporta l’attivazione dei dati nelle destinazioni di archiviazione cloud in streaming, consentendoti di esportare i dati e gli eventi del pubblico in tempo reale in queste destinazioni in formato JSON. Puoi quindi descrivere la logica di business oltre a questi eventi nelle tue destinazioni

Microsoft Azure Event Hubs è un servizio di acquisizione dati in tempo reale, completamente gestito, semplice, affidabile e scalabile. Trasmetti milioni di eventi al secondo da qualsiasi origine per creare pipeline di dati dinamiche e rispondere immediatamente alle sfide aziendali.

## Finalità di apprendimento

- Acquisisci familiarità con gli hub eventi di Microsoft Azure
- Configurare una destinazione RTCDP nell&#39;hub eventi di Microsoft Azure
- Comprendere quando Real-time CDP si attiva e come si presenta il payload di attivazione
- Configurare il codice Visual Studio per sviluppare, testare e distribuire il progetto Azure
- Crea e distribuisci una funzione di Azure che utilizza i segmenti e le qualifiche consegnate in tempo reale da RTCDP

## Prerequisiti

- Accesso a [Adobe Experience Platform](https://experience.adobe.com/platform)
- Familiarità con l’ambiente del sito web AEP Demo
- Come definire, utilizzare e attivare i segmenti di streaming in Adobe Experience Platform

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l&#39;estensione Chrome come indicato in [Installare l&#39;estensione Chrome per la documentazione di Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Esercizi

[2.4.0 Configurare l’ambiente](./ex0.md)

In questo esercizio verrà configurato l&#39;ambiente Microsoft Azure.

[2.4.1 Configurare l’ambiente Microsoft Azure EventHub](./ex1.md)

In questo esercizio verrà configurato l’ambiente Microsoft Azure EventHub.

[2.4.2 Configurare la destinazione dell’hub eventi di Azure in Adobe Experience Platform](./ex2.md)

In questo esercizio configurerai la connessione di destinazione Real-time CDP che distribuirà i segmenti in tempo reale a EventHub configurata nell’esercizio precedente.

[2.4.3 Creare un segmento](./ex3.md)

In questo esercizio creerai un segmento di streaming in Adobe Experience Platform

[2.4.4 Attiva segmento](./ex4.md)

In questo esercizio attiverai il segmento di streaming nella destinazione Real-time CDP EventHub.

[2.4.5 Creare il progetto Microsoft Azure](./ex5.md)

In questo esercizio creerai una funzione di Azure che verrà attivata in tempo reale quando Adobe Experience Platform attiva le qualifiche dei segmenti nella destinazione dell’hub eventi di Azure corrispondente.

[2.4.6 Scenario end-to-end](./ex6.md)

A questo punto, tutto è pronto. È ora possibile eseguire alcune esplorazioni nel sito Web AEP Demo e ottenere le qualifiche dei segmenti consegnate alla funzione Trigger di Microsoft Azure EventHub.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all&#39;apprendimento di tutto ciò che c&#39;è da sapere su Adobe Experience Platform e sulle sue applicazioni. Se hai domande, vuoi condividere feedback generali su suggerimenti in merito a contenuti futuri, contatta direttamente Tech Insiders, inviando un&#39;e-mail a **techinsiders@adobe.com**.

[Torna a tutti i moduli](../../../overview.md)
