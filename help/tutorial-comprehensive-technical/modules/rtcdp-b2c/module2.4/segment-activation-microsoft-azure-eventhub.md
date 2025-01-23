---
title: Audience Activation dell’hub eventi di Microsoft Azure
description: Audience Activation dell’hub eventi di Microsoft Azure
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 2.4 Real-Time CDP: da Audience Activation a Microsoft Azure Event Hub

In questo modulo verrà impostata una destinazione Microsoft Azure EventHub come destinazione in tempo reale per Adobe Experience Platform Real-time CDP. Puoi anche configurare e distribuire una funzione di Azure che verrà attivata in tempo reale ogni volta che Adobe Experience Platform distribuisce un payload di pubblico alla destinazione di Azure EventHub. La funzione di Azure che verrà attivata mostrerà il meccanismo delle funzionalità di attivazione di Adobe Experience Platform Real-time CDP.

Come parte di questo modulo, comprenderai anche cosa attiva Real-time CDP per consegnare effettivamente un payload a una destinazione specifica. Discuteremo anche dello stato di qualifica di un pubblico e di come si relaziona all’attivazione.

Adobe Experience Platform Real-time CDP supporta l’attivazione dei dati nelle destinazioni di archiviazione cloud in streaming, consentendoti di esportare i dati e gli eventi del pubblico in tempo reale in queste destinazioni in formato JSON. Puoi quindi descrivere la logica di business oltre a questi eventi nelle tue destinazioni

Microsoft Azure Event Hubs è un servizio di acquisizione dati in tempo reale, completamente gestito, semplice, affidabile e scalabile. Trasmetti milioni di eventi al secondo da qualsiasi origine per creare pipeline di dati dinamiche e rispondere immediatamente alle sfide aziendali.

## Finalità di apprendimento

- Acquisisci familiarità con gli hub eventi di Microsoft Azure
- Configurare una destinazione RTCDP nell&#39;hub eventi di Microsoft Azure
- Comprendere quando Real-time CDP si attiva e come si presenta il payload di attivazione
- Configurare il codice Visual Studio per sviluppare, testare e distribuire il progetto Azure
- Crea e distribuisci una funzione di Azure che utilizza i requisiti del pubblico forniti in tempo reale da RTCDP

## Prerequisiti

- Accesso a [Adobe Experience Platform](https://experience.adobe.com/platform)
- Come definire, utilizzare e attivare i tipi di pubblico in Adobe Experience Platform

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l&#39;estensione Chrome come indicato in [Installare l&#39;estensione Chrome per la documentazione di Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Esercizi

[2.4.1 Configurare l’ambiente](./ex1.md)

In questo esercizio verrà configurato l&#39;ambiente Microsoft Azure.

[2.4.2 Configurare l’ambiente Microsoft Azure EventHub](./ex2.md)

In questo esercizio verrà configurato l’ambiente Microsoft Azure EventHub.

[2.4.3 Configurare la destinazione dell’hub eventi di Azure in Adobe Experience Platform](./ex3.md)

In questo esercizio configurerai la connessione di destinazione Real-time CDP che fornirà i tipi di pubblico in tempo reale all’istanza dell’hub eventi configurata nell’esercizio precedente.

[2.4.4 Creare un pubblico](./ex4.md)

In questo esercizio creerai un pubblico in Adobe Experience Platform

[2.4.5 Attivare il pubblico](./ex5.md)

In questo esercizio attiverai il pubblico nella destinazione EventHub.

[2.4.6 Creare il progetto Microsoft Azure](./ex6.md)

In questo esercizio creerai una funzione di Azure che verrà attivata in tempo reale quando Adobe Experience Platform rilascerà i requisiti del pubblico alla corrispondente destinazione dell’hub eventi di Azure.

[2.4.7 Scenario completo](./ex7.md)

A questo punto, tutto è pronto. Ora puoi esplorare il sito web demo e ottenere i requisiti del pubblico per la funzione Trigger dell’hub eventi di Microsoft Azure.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

![Informazioni tecniche](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all&#39;apprendimento di tutto ciò che c&#39;è da sapere su Adobe Experience Platform e sulle sue applicazioni. Se hai domande, vuoi condividere feedback generali su suggerimenti in merito a contenuti futuri, contatta direttamente Tech Insiders, inviando un&#39;e-mail a **techinsiders@adobe.com**.

[Torna a tutti i moduli](../../../overview.md)
