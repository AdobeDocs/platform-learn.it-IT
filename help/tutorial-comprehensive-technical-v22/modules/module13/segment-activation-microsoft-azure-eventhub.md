---
title: Attivazione del segmento nell’hub eventi di Microsoft Azure
description: Attivazione del segmento nell’hub eventi di Microsoft Azure
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73c2576d-0a69-4d56-a671-9ae1f75580b9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---

# 13. Real-Time CDP: Attivazione del segmento nell’hub eventi di Microsoft Azure

**Autori: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo, configurerai una destinazione Microsoft Azure EventHub come destinazione in tempo reale per Adobe Experience Platform Real-time CDP. Puoi anche impostare e distribuire una funzione di Azure che verrà attivata in tempo reale ogni volta che Adobe Experience Platform consegna un payload di segmento alla destinazione Azure EventHub. La funzione di Azure che verrà attivata mostrerà il meccanismo delle funzionalità di attivazione di CDP in tempo reale di Adobe Experience Platform.

Come parte di questo modulo, avrai anche una comprensione di ciò che attiva Real-time CDP per distribuire effettivamente un payload a una destinazione specifica. Discuteremo anche dello stato della qualifica di un segmento e di come si relaziona all’attivazione.

Adobe Experience Platform Real-time CDP supporta l’attivazione dei dati per le destinazioni di archiviazione cloud in streaming, consentendo di esportare i dati e gli eventi del pubblico in tempo reale per queste destinazioni in formato JSON. Puoi quindi descrivere la logica di business sopra questi eventi nelle destinazioni

Microsoft Azure Event Hubs è un servizio di acquisizione dati in tempo reale, completamente gestito, semplice, affidabile e scalabile. Trasmetti milioni di eventi al secondo da qualsiasi origine per creare pipeline di dati dinamici e rispondere immediatamente alle sfide aziendali.

## Finalità di apprendimento

- Acquisisci familiarità con gli hub eventi di Microsoft Azure
- Impostare una destinazione RTCDP sul proprio hub eventi di Microsoft Azure
- Comprendere quando Real-time CDP si attiva e come si presenta il payload di attivazione
- Configurazione del codice di Visual Studio per sviluppare, testare e distribuire il progetto di Azure
- Creare e distribuire una funzione di Azure che consuma le qualifiche dei segmenti consegnate in tempo reale da RTCDP

## Prerequisiti

- Accesso a [Adobe Experience Platform](https://experience.adobe.com/platform)
- Familiarità con l&#39;ambiente del sito web AEP Demo
- Come definire, utilizzare e attivare i segmenti di streaming in Adobe Experience Platform

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem18.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--module18sandbox--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[13.0 Configurare l&#39;ambiente](./ex0.md)

In questo esercizio, configurerai l’ambiente Microsoft Azure.

[13.1 Configurare l’ambiente EventHub di Microsoft Azure](./ex1.md)

In questo esercizio verrà configurato l’ambiente EventHub di Microsoft Azure.

[13.2 Configurare la destinazione dell&#39;hub eventi di Azure in Adobe Experience Platform](./ex2.md)

In questo esercizio configurerai la connessione di destinazione Real-time CDP che fornirà i segmenti in tempo reale all’EventHub configurato nell’esercizio precedente.

[13.3 Creare un segmento](./ex3.md)

In questo esercizio creerai un segmento di streaming in Adobe Experience Platform

[13.4 Attivare il segmento](./ex4.md)

In questo esercizio attiverai il segmento di streaming nella tua destinazione Real-time CDP EventHub.

[13.5 Creare il progetto Microsoft Azure](./ex5.md)

In questo esercizio creerai una funzione di Azure che verrà attivata in tempo reale quando Adobe Experience Platform attiva le qualifiche dei segmenti nella destinazione corrispondente di Azure Event Hub.

[13.6 Scenario end-to-end](./ex6.md)

A questo punto, tutto è pronto. Ora puoi effettuare alcune ricerche sul sito web AEP Demo e ottenere le qualifiche dei segmenti consegnate alla funzione Trigger evento di Microsoft Azure.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)
