---
title: Foundation - Acquisizione dei dati
description: Foundation - Acquisizione dei dati
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# 2. Foundation - Acquisizione dei dati

**Autore: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo, l’obiettivo è quello di imparare tutto sull’inserimento dei dati. Scoprirai come acquisire i dati in Streaming e Batch. Implementerai l’acquisizione di dati in streaming utilizzando Launch, in modo che il comportamento del cliente sul sito web Hands-On Lab venga trasmesso in streaming a Adobe Experience Platform in tempo reale. Per informazioni sull’acquisizione di dati in batch, utilizza un flusso di lavoro Adobe Experience Platform per prendere un file CSV, mapparlo su uno schema XDM e quindi trasferirlo in Adobe Experience Platform.

## Finalità di apprendimento

- Scopri come creare uno schema XDM in Adobe Experience Platform
- Scopri come creare set di dati in Adobe Experience Platform
- Scopri come creare un endpoint di streaming e configurare l’estensione Adobe Experience Platform in Launch
- Scopri come creare regole in Launch per inviare dati in streaming a Adobe Experience Platform
- Scopri come integrare Adobe Experience Platform Launch in una pagina web
- Scopri come utilizzare un flusso di lavoro Adobe Experience Platform per acquisire un file CSV in Adobe Experience Platform

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso ad Adobe Experience Platform Launch: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accesso a [https://public.aepdemo.net](https://public.aepdemo.net)
- Accesso a Postman

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem2.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--module2sandbox--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[2.1 Esplora il sito web](./ex1.md)

In questo esercizio esplorerai il sito web che utilizzerai come parte di questa abilitazione.

[2.2 Configurare gli schemi e impostare gli identificatori](./ex2.md)

In questo esercizio, configurerai gli schemi XDM richiesti per acquisire informazioni sul profilo e il comportamento del cliente. In ogni schema XDM, dovrai anche configurare un identificatore principale per collegare tutte le informazioni a.

[2.3 Configurare i set di dati](./ex3.md)

In questo esercizio, recupererai i set di dati necessari per acquisire e memorizzare le informazioni sul profilo e il comportamento del cliente.

[2.4 Acquisizione dati da fonti offline](./ex4.md)

In questo esercizio, accederai al sito web e all’app mobile e ti comporti come un cliente, trasferendo i dati in streaming a Platform.

[2.5 Data Landing Zone](./ex5.md)

Imposta il connettore Origine area di destinazione dati con l’archiviazione BLOB di Azure.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)
