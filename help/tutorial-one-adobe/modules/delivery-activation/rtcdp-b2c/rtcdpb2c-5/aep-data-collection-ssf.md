---
title: Raccolta dati di Adobe Experience Platform e inoltro lato server in tempo reale
description: In questo modulo utilizzerai i set di dati, gli schemi e le proprietà del server di raccolta dati di Adobe Experience Platform configurati in precedenza per raccogliere i dati, quindi inoltrarli lato server a un endpoint scelto.
kt: 5342
doc-type: tutorial
exl-id: dbf5e995-9c2e-4f72-b336-e942cb22cde5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 2.5 Connessioni Real-Time CDP: Inoltro eventi

In questo modulo utilizzerai i set di dati, gli schemi e le proprietà client di raccolta dati di Adobe Experience Platform configurati in precedenza per raccogliere i dati, quindi inoltrarli lato server a un endpoint di scelta.

In questo modulo:

- Creare una proprietà di Adobe Experience Platform Data Collection Server
- Installare e utilizzare l’estensione Adobe Cloud Connector in raccolta dati Adobe Experience Platform
- Creare un endpoint di funzione Google e inviare ad esso i dati
- Creare un endpoint AWS e trasmettervi dati

## Finalità di apprendimento

- Acquisisci familiarità con le proprietà del server di raccolta dati di Adobe Experience Platform e la nuova estensione Adobe Cloud Connector
- Come riutilizzare i dati di Adobe Experience Platform Web SDK in soluzioni di terze parti come Google e AWS
- Scopri l’architettura alla base della raccolta dati di Adobe Experience Platform e dell’inoltro lato server.

## Prerequisiti

- Accesso alla raccolta dati di Adobe Experience Platform e Adobe Experience Platform
- Informazioni sui set di dati Adobe Experience Platform e XDM

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l&#39;estensione Chrome come indicato in [Installare l&#39;estensione Chrome per la documentazione di Experience League](../../../getting-started/gettingstarted/ex1.md)

## Esercizi

[2.5.1 Creare una proprietà di inoltro degli eventi di raccolta dati](./ex1.md)

In questo esercizio creerai la tua proprietà Adobe Experience Platform Data Collection Event Forwarding.

[2.5.2 Aggiorna lo stream di dati per rendere i dati disponibili per la proprietà Data Collection Event Forwarding](./ex2.md)

In questo esercizio aggiornerai lo stream di dati esistente per rendere disponibili alla proprietà Server di raccolta dati di Adobe Experience Platform i dati raccolti dalla proprietà Client di raccolta dati di Adobe Experience Platform.

[2.5.3 Creare e configurare un webhook personalizzato](./ex3.md)

In questo esercizio verrà creato e configurato un webhook personalizzato e inizierai a inoltrare i dati raccolti da Web SDK a tale webhook personalizzato.

[2.5.4 Inoltra gli eventi a GCP Pub/Sub](./ex4.md)

In questo esercizio creerai e configurerai una funzione cloud di Google e inizierai a inoltrare a Google i dati raccolti da Web SDK.

[2.5.5 Inoltrare gli eventi ad AWS Kinesis e AWS S3](./ex5.md)

In questo esercizio configurerai l’ambiente AWS utilizzando AWS IAM, AWS Kinesis, AWS Firehose e AWS S3, dopodiché inizierai a inoltrare i dati evento raccolti da Web SDK.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

![Informazioni tecniche](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all&#39;apprendimento di tutto ciò che c&#39;è da sapere su Adobe Experience Platform e sulle sue applicazioni. Se hai domande, vuoi condividere feedback generali su suggerimenti in merito a contenuti futuri, contatta direttamente Tech Insiders, inviando un&#39;e-mail a **techinsiders@adobe.com**.

[Torna a tutti i moduli](./../../../../overview.md)
