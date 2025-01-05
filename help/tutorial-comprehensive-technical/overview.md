---
title: Panoramica
description: Punto di partenza per Data Engineer, Data Analyst, Data Architect, Data Scientist, Orchestration Engineer e Marketing per comprendere appieno il valore aziendale di Adobe Experience Platform e di tutti i suoi servizi applicativi.
doc-type: multipage-overview
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: 21718a7c3a4df2793ae257a9b7cbe4466f1193f5
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 2%

---

# Tutorial tecnico completo per Adobe Experience Platform

## Panoramica

Questo tutorial è il punto di partenza ideale per Data Engineer, Data Analyst, Data Architect, Data Scientist, Orchestration Engineer e Marketing per comprendere appieno il valore aziendale di Adobe Experience Platform e di tutti i suoi servizi applicativi. Ogni lezione si concentra su una vera sfida che le aziende si trovano ad affrontare nel complesso ecosistema della personalizzazione di oggi e analizza come Experience Platform risolve tale sfida in vari esercizi pratici.

Questo tutorial è molto vario e offre informazioni chiare nelle seguenti applicazioni:

- Adobe Experience Platform
- Raccolta dati di Adobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

Questo tutorial non si concentra solo sulle applicazioni Adobe, ma tiene conto dell’ecosistema più ampio in cui operano i brand. Per farlo, in alcune lezioni è necessario concentrarsi sul modo in cui _applicazioni non Adobe_ si integrano con Adobe Experience Platform. In questo modo sarà possibile comprendere a fondo come funzioneranno le seguenti applicazioni insieme a Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: piattaforma Google Cloud, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Archiviazione BLOB di Azure
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

Dopo aver completato gli esercizi in questa esercitazione, sarai in grado di:

- Configurare schemi, gruppi di campi, set di dati e identità
- Configurare una proprietà di raccolta dati Adobe Experience Platform e impostare la nuova estensione Web SDK in Raccolta dati Adobe Experience Platform
- Trasmetti dati in Adobe Experience Platform in tempo reale utilizzando Raccolta dati di Adobe Experience Platform
- Acquisire in batch i dati in Adobe Experience Platform utilizzando un flusso di lavoro o un’applicazione ETL (Extract, Transform, Load)
- Visualizzare e utilizzare Real-time Customer Profile in Adobe Experience Platform
- Creare tipi di pubblico
- Utilizzo di diverse API Adobe Experience Platform
- Utilizzare SQL per eseguire query sui dati in Adobe Experience Platform
- Configurazione ed esecuzione di percorsi basati su trigger in tempo reale
- Utilizzare Real-time CDP per intervenire attivando un pubblico in varie destinazioni
- Utilizza Customer Journey Analytics per creare rapporti sui dati dei clienti omnicanale provenienti da varie origini, incluso Google BigQuery.

## Prerequisiti

Se desideri seguire questo tutorial utilizzando la tua istanza di Adobe Experience Platform, segui le istruzioni [qui](./setup.md) per preparare la tua organizzazione per il tutorial.

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso alla raccolta dati di Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/)
- Accesso al sistema demo: [https://dsn.adobe.com/](https://dsn.adobe.com/)

## Video

Puoi trovare molti video interessanti dai nostri webinar sulla Tech Academy, dai bootcamp e altro sul nostro [canale YouTube della community Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Completamento e certificazione

Questa esercitazione fa parte di un corso di certificazione Adobe. Per iscriverti al corso e seguire questa esercitazione, vai a [https://certification.adobe.com](https://certification.adobe.com).

Per ogni modulo completato tramite l&#39;esercitazione seguente, devi inviare una prova di completamento come indicato [qui](./completion.md).

## Contenuto

Per verificare lo stato del contenuto seguente, passare alla [pagina di stato](./status.md).

[0. Guida introduttiva](./modules/gettingstarted/gettingstarted/getting-started.md)

In questo modulo fondamentale, configurerai tutto in modo da poter accedere e utilizzare l’ambiente demo.

**Investimento nel tempo:** 30 minuti

### 1. Raccolta dei dati

[1.1 Foundation - Configurazione di Adobe Experience Platform Data Collection e Web SDK](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

In questo modulo fondamentale scoprirai le funzionalità di raccolta dati di Adobe Experience Platform e la nuova estensione Web SDK.

**Investimento nel tempo:** 30 minuti

[1.2 Foundation - Acquisizione dei dati](./modules/datacollection/module1.2/data-ingestion.md)

In questo modulo fondamentale, in Adobe Experience Platform verranno acquisiti dati da varie origini

**Investimento nel tempo:** 120 minuti

[1.3 Federated Audience Composition](./modules/datacollection/module1.3/fac.md)

In questo modulo imparerai a impostare un modello Federated Audiences e generare tipi di pubblico utilizzando dati federati.

**Investimento nel tempo:** 90 minuti

### 2. Real-Time CDP B2C

[2.1 Foundation - Profilo cliente in tempo reale](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

In questo modulo fondamentale, esplorerai il profilo cliente in tempo reale in Adobe Experience Platform utilizzando l’interfaccia utente e l’API.

**Investimento nel tempo:** 90 minuti

[2.2 Servizi intelligenti](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

In questo modulo imparerai a configurare, configurare e utilizzare Adobe Experience Platform Intelligent Services.

**Investimento nel tempo:** 60 minuti

[2.3 Real-Time CDP - Creare un pubblico e intervenire](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

In questo modulo, puoi configurare un pubblico e attivarlo in diverse destinazioni, tra cui Google DV360, Adobe Target e AWS S3.

**Investimento nel tempo:** 90 minuti

[2.4 Real-Time CDP: da Audience Activation a Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

In questo modulo verrà impostata una destinazione Microsoft Azure EventHub come destinazione in tempo reale per Adobe Experience Platform Real-time CDP. Puoi anche configurare e distribuire una funzione di Azure che verrà attivata in tempo reale ogni volta che Adobe Experience Platform distribuisce un payload di pubblico alla destinazione di Azure EventHub. La funzione di Azure che verrà attivata mostrerà il meccanismo delle funzionalità di attivazione di Adobe Experience Platform Real-time CDP.
Come parte di questo modulo, comprenderai anche cosa attiva Real-time CDP per consegnare effettivamente un payload a una destinazione specifica. Discuteremo anche dello stato di qualifica di un pubblico e di come si relaziona all’attivazione.

**Investimento nel tempo:** 90 minuti

[2.5 Connessioni Real-Time CDP: Inoltro eventi](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

In questo modulo utilizzerai i set di dati, gli schemi e le proprietà di raccolta dati di Adobe Experience Platform configurati in precedenza per raccogliere i dati e inoltrarli lato server a diversi endpoint, ad esempio Google Cloud Platform Pub/Sub e AWS Kinesis.

**Investimento nel tempo:** 90 minuti

[2.6 Trasmettere dati da Apache Kafka a Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

In questo modulo imparerai a configurare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e inviare dati in Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink per Kafka Connect.

**Investimento nel tempo:** 90 minuti

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orchestrazione](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

In questo modulo utilizzerai Adobe Journey Optimizer per creare un percorso basato su trigger.

**Investimento nel tempo:** 60 minuti

[3.2 Adobe Journey Optimizer: origini dati esterne e azioni personalizzate](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

In questo modulo, utilizzerai Adobe Journey Optimizer per ascoltare il comportamento dei clienti, online e offline, e rispondervi in modo intelligente, contestuale e in tempo reale su vari canali.

**Investimento nel tempo:** 90 minuti

[3.3 Adobe Journey Optimizer: Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

In questo modulo utilizzerai il servizio applicativo Adobe Experience Platform - Offerte/Decisioning in modo pratico per configurare offerte personalizzate e la tua attività di offerta.

**Investimento nel tempo:** 120 minuti

[3.4 Adobe Journey Optimizer: Percorsi basati su eventi](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

In questo modulo imparerai tutto quello che c’è da sapere su Journey Optimizer, che aiuta le aziende a progettare e fornire ai propri clienti esperienze connesse, contestuali e personalizzate.

**Investimento nel tempo:** 120 minuti

### 4. Adobe Customer Journey Analytics

[4.1 Customer Journey Analytics: creare una dashboard utilizzando Analysis Workspace su Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

In questo modulo, otterrai approfondimenti online e offline configurando una dashboard contenente dati omni-channel come interazioni con siti web, interazioni con app mobili, interazioni con call center, interazioni con in-store e molto altro.

**Investimento nel tempo:** 120 minuti

[4.2 Customer Journey Analytics: inserire e analizzare i dati Google Analytics in Adobe Experience Platform con il connettore Source BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

In questo modulo, configurerai la tua istanza di Google Cloud Platform, caricherai i dati demo in Google Cloud Platform e quindi utilizzerai il connettore BigQuery Source per acquisire tali dati da Google Cloud Platform in Adobe Experience Platform. Infine, utilizzerai il Customer Journey Analytics per visualizzare tali dati.

**Investimento nel tempo:** 120 minuti

### 5. Data Distiller

[5.1 Servizio query](./modules/datadistiller/module5.1/query-service.md)

In questo modulo imparerai a utilizzare Adobe Experience Platform Query Service.

**Investimento nel tempo:** 90 minuti
