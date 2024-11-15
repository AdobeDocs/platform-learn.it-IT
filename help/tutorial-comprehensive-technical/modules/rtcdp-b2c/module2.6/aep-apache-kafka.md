---
title: Trasmettere dati da Apache Kafka a Adobe Experience Platform
description: In questo modulo imparerai a configurare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e inviare dati in Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink per Kafka Connect.
kt: 5342
doc-type: tutorial
exl-id: 2b7010f3-ab31-4099-aecd-fd4e73b7e96e
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# 2.6 Trasmettere dati da Apache Kafka a Adobe Experience Platform

**Autori: [Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/), [Nipun Nair](https://www.linkedin.com/in/nipunnair/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo imparerai a configurare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e inviare dati in Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink tramite Kafka Connect.

## Finalità di apprendimento

- Eseguire una configurazione di base di un cluster Kafka locale
- Creare un argomento Kafka, utilizzare un produttore Kafka e un consumatore Kafka
- Configurare Kafka Connect e il connettore Adobe Experience Platform Sink
- Genera manualmente gli eventi e visualizza quelli che vengono acquisiti in Adobe Experience Platform
- Utilizza una libreria di produttori di Twitter esistente da Kafka Connect per inviare dati di Twitter a Adobe Experience Platform

## Prerequisiti

- Java JDK11 o versione successiva deve essere installato sul computer. È possibile scaricarlo qui: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Accesso a Adobe Experience Platform

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l&#39;estensione Chrome come indicato in [Installare l&#39;estensione Chrome per la documentazione di Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Esercizi

[2.6.1 Introduzione ad Apache Kafka](./ex1.md)

In questo esercizio imparerai le nozioni di base di Apache Kafka

[2.6.2 Installare e configurare il cluster Kafka](./ex2.md)

In questo esercizio scaricherai, installerai e configurerai il cluster Apache Kafka di base.

[2.6.3 Configurare l’endpoint di streaming API HTTP in Adobe Experience Platform](./ex3.md)

In questo esercizio configurerai un connettore Source API HTTP in Adobe Experience Platform.

[2.6.4 Installare e configurare Kafka Connect e il connettore Adobe Experience Platform Sink](./ex4.md)

In questo esercizio utilizzerai Kafka Connect per installare e utilizzare il connettore Adobe Experience Platform Sink e invierai gli eventi a Adobe Experience Platform manualmente.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all&#39;apprendimento di tutto ciò che c&#39;è da sapere su Adobe Experience Platform e sulle sue applicazioni. Se hai domande, vuoi condividere feedback generali su suggerimenti in merito a contenuti futuri, contatta direttamente Tech Insiders, inviando un&#39;e-mail a **techinsiders@adobe.com**.

[Torna a tutti i moduli](../../../overview.md)
