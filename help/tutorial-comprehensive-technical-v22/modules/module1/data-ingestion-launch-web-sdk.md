---
title: 1. Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell'estensione Web SDK
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 86da7132-cb06-4be3-b6b8-ea3ab937e6dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 1. Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK

**Autore: [Matthew Joseph Woolley](https://www.linkedin.com/in/matthewjwoolley/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Questo modulo fondamentale introduce la visione della raccolta dati di Adobe e spiega come ottenere dati da un sito web e da un’applicazione mobile in Adobe Experience Platform e altre applicazioni tramite Adobe Experience Platform Data Collection, gli SDK Adobe Experience Platform e Adobe Experience Platform Edge Network. Questo modulo introduce alcuni concetti e tecnologie che hanno un impatto oltre l’ambito di un’esercitazione tecnica Adobe Experience Platform. Dovrebbe essere chiaro quali parti di questi esercizi sono fondamentali per il resto dell’esercitazione completa, che offre ulteriori informazioni su Experience Edge e sulle sue funzionalità e dove andare per ulteriori informazioni ed esercitazioni.

## Finalità di apprendimento

- Scopri come un marchio utilizza Adobe Experience Platform Data Collection come sistema Tag Management (TMS).
- Scopri i flussi di dati utilizzati da un marchio per acquisire dati sui prodotti di Adobe.
- Scopri come inviare dati a Adobe Experience Platform e ad altri prodotti tramite Adobe Experience Platform Edge Network.
- Scopri come creare elementi dati e regole che raccolgono dati da Web e dispositivi mobili.
- Scopri gli eventi di tracciamento dell’SDK per web e come eseguirne il debug.
- Scopri cos’è un livello di dati e cosa consiglia l’Adobe durante l’implementazione di un livello.
- Scopri i passaggi necessari per implementare l’SDK per web da zero.
- Scopri la differenza tra un’implementazione web e mobile.

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso alla raccolta dati di Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accesso al sito web demo

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem1.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[1.1 Informazioni sulla raccolta dati di Adobe Experience Platform](./ex1.md)

In questo esercizio, esplora l’interfaccia utente di raccolta dati di Adobe Experience Platform e scopri le sue funzionalità.

[1.2 Rete Edge, Datastreams e raccolta dati lato server](./ex2.md)

In questo esercizio imparerai a inoltrare i dati ai prodotti Adobe nell’interfaccia di raccolta dati di Adobe Experience Platform e a scoprire i flussi di dati utilizzati dal sito web dimostrativo.

[1.3 Introduzione alla raccolta dati di Adobe Experience Platform](./ex3.md)

In questo esercizio imparerai a configurare un’estensione, creare elementi dati e regole e a pubblicarli sul web.

[1.4 Raccolta dati web lato client](./ex4.md)

In questo esercizio, esegui il debug dell’SDK web installato per comprendere come funziona e quali dati verranno utilizzati negli esercizi futuri.

[1.5 Implementare Adobe Analytics e Adobe Audience Manager](./ex5.md)

In questo esercizio, consulta e utilizza i dati web raccolti con l’SDK per web in Adobe Analytics e Adobe Audience Manager.

[1.6 Implementare Adobe Target](./ex6.md)

In questo esercizio, configura un’attività in Adobe Target, implementata tramite l’SDK per web.

[Requisiti dello schema XDM 1.7 in Adobe Experience Platform](./ex7.md)

Per garantire che l’SDK web e alloy.js siano in grado di acquisire dati in Adobe Experience Platform, è necessario che un determinato mixin XDM faccia parte dello schema XDM in Adobe Experience Platform.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)
