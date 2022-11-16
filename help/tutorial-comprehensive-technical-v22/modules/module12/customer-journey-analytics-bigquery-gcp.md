---
title: Inserire e analizzare i dati delle Google Analytics in Adobe Experience Platform con il connettore sorgente BigQuery
description: Inserire e analizzare i dati delle Google Analytics in Adobe Experience Platform con il connettore sorgente BigQuery
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 3%

---

# 12. Acquisire e analizzare i dati delle Google Analytics in Adobe Experience Platform con il connettore sorgente BigQuery

**Autori: [Victor de la Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo, configurerai la tua istanza di Google Cloud Platform, caricherai i dati di esempio in Google Cloud Platform e quindi utilizzerai il Connettore origine BigQuery per acquisire i dati da Google Cloud Platform in Adobe Experience Platform. Infine, utilizzerai il Customer Journey Analytics per visualizzare tali dati.

I connettori sorgente in Adobe Experience Platform semplificano il processo di inserimento dei dati in Adobe Experience Platform. Google BigQuery è uno dei connettori già disponibili. Grazie a Adobe Experience Platform e al connettore sorgente BigQuery ora possiamo inserire dati Google Analytics in Analysis Workspace in Customer Journey Analytics.

Inoltre, possiamo arricchire i dati Google Analytics unendoli ad altre origini dati come CRM, Call Center o i dati fedeltà all’interno del Customer Journey Analytics.

## Finalità di apprendimento

- Acquisisci familiarità con la piattaforma Google Cloud Platform e l’interfaccia utente BigQuery
- Acquisire dati Google Analytics in Adobe Experience Platform
- Utilizzare il Customer Journey Analytics per eseguire l&#39;analisi dei dati Google Analytics
- Arricchire i dati delle Google Analytics con i dati offline

## Prerequisiti

- Una certa familiarità con il Customer Journey Analytics è preferita, ma non richiesta
- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso a Customer Journey Analytics
- Accesso a Google Cloud Platform e Google BigQuery
- **Scarica queste risorse**:
   - [JSON - Dati di esempio: Dati fedeltà](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem16.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--aepSandboxId--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[12.1 Creare l’account Google Cloud Platform](./ex1.md)

Crea il tuo account Google Cloud Platform.

[12.2 Crea la tua prima query in BigQuery](./ex2.md)

Scopri come utilizzare BigQuery per preparare i dati da caricare in Platform.

[12.3 Collegare GCP e BigQuery a Adobe Experience Platform](./ex3.md)

Scopri come impostare il connettore sorgente in Adobe Experience Platform.

[12.4 Caricare dati da BigQuery in Adobe Experience Platform](./ex4.md)

Scopri come configurare il connettore di origine BigQuery in Adobe Experience Platform per l’acquisizione dei dati Google Analytics.

[12.5 Analizzare i dati delle Google Analytics utilizzando il Customer Journey Analytics](./ex5.md)

Scopri come analizzare i dati delle Google Analytics nel Customer Journey Analytics e combinarli con i dati relativi alla fedeltà.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)
