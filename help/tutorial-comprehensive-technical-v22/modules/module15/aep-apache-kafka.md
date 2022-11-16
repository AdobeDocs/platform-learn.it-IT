---
title: Trasmetti dati da Apache Kafka a Adobe Experience Platform
description: In questo modulo imparerai come impostare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e trasmettere dati in Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink per Kafka Connect.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: e1e283b1-93b7-4d06-b9ed-beac48a99c3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# 15. Trasmetti i dati da Apache Kafka a Adobe Experience Platform

**Autori: [Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/), [Nipun](https://www.linkedin.com/in/nipunnair/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo imparerai come impostare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e trasmettere dati in Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink tramite Kafka Connect.

## Finalità di apprendimento

- Eseguire una configurazione di base di un cluster Kafka locale
- Crea un argomento Kafka, utilizza un produttore Kafka e un consumatore Kafka
- Configurare Kafka Connect e Adobe Experience Platform Sink Connector
- Produrre manualmente eventi e vedere come vengono acquisiti gli eventi in Adobe Experience Platform
- Utilizzare una libreria di produttori Twitter esistente da Kafka Connect per lo streaming dei dati Twitter in Adobe Experience Platform

## Prerequisiti

- Java JDK11 o versione successiva deve essere installato sul tuo computer, puoi scaricare tale JDK qui: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Accesso a Adobe Experience Platform

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem24.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[15.1 Introduzione ad Apache Kafka](./ex1.md)

In questo esercizio imparerai le basi di Apache Kafka

[15.2 Installare e configurare il cluster Kafka](./ex2.md)

In questo esercizio, scaricerai, installerai e configurerai il tuo cluster Apache Kafka di base.

[15.3 Configurare l&#39;endpoint di streaming API HTTP in Adobe Experience Platform](./ex3.md)

In questo esercizio, configurerai un connettore di origine API HTTP in Adobe Experience Platform.

[15.4 Installare e configurare Kafka Connect e il connettore Sink Adobe Experience Platform](./ex4.md)

In questo esercizio, utilizzerai Kafka Connect per installare e utilizzare il connettore Sink Adobe Experience Platform e invierai manualmente gli eventi in Adobe Experience Platform.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)
