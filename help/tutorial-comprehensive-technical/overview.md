---
title: Panoramica
description: Punto di partenza per Data Engineer, Data Analyst, Data Architect, Data Scientist, Orchestration Engineer e Marketing per comprendere appieno il valore aziendale di Adobe Experience Platform e di tutti i suoi servizi applicativi.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: b46c753a8d854b5a448d10d30c7a5701900a35b8
workflow-type: tm+mt
source-wordcount: '1524'
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
- Configurare una proprietà di Raccolta dati Adobe Experience Platform e impostare la nuova estensione Web SDK in Raccolta dati Adobe Experience Platform
- Trasmetti dati in Adobe Experience Platform in tempo reale utilizzando Raccolta dati di Adobe Experience Platform
- Acquisire in batch i dati in Adobe Experience Platform utilizzando un flusso di lavoro o un’applicazione ETL (Extract, Transform, Load)
- Visualizzare e utilizzare Real-time Customer Profile in Adobe Experience Platform
- Creare segmenti
- Utilizzo di diverse API Adobe Experience Platform
- Utilizzare SQL per eseguire query sui dati in Adobe Experience Platform
- Configurazione ed esecuzione di percorsi basati su trigger in tempo reale
- Utilizza Real-time CDP per intervenire attivando un segmento in varie destinazioni
- Utilizza Customer Journey Analytics per creare rapporti sui dati dei clienti omnicanale provenienti da varie origini, incluso Google BigQuery.

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso alla raccolta dati di Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/)
- Accesso al sistema demo: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

## Video

Puoi trovare molti video interessanti dai nostri eventi Tech Academy, da Bootcamps e altri sul nostro [canale YouTube della community Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Contenuto

[0. Guida introduttiva](./modules/gettingstarted/gettingstarted/getting-started.md)

- **Pubblico:** Tutti i partecipanti al tutorial tecnico completo per Adobe Experience Platform
- **Prerequisiti:** Accesso a Demo System Next, Adobe Experience Platform e raccolta dati Adobe Experience Platform.
- **Descrizione:** In questo modulo di base, configurerai tutto in modo da poter accedere e utilizzare l&#39;ambiente demo.
- **Investimento nel tempo:** 30 minuti

### 1. Raccolta dei dati

[1.1 Foundation - Configurazione di Adobe Experience Platform Data Collection e Web SDK](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

- **Pubblico:** Ingegnere dati, Architetto dati
- **Prerequisiti:** accesso alla raccolta dati di Adobe Experience Platform e Adobe Experience Platform.
- **Descrizione:** In questo modulo fondamentale scoprirai le funzionalità di raccolta dati di Adobe Experience Platform e la nuova estensione Web SDK.
- **Investimento nel tempo:** 30 minuti

[1.2 Foundation - Acquisizione dei dati](./modules/datacollection/module1.2/data-ingestion.md)

- **Pubblico:** Ingegnere dati, Architetto dati
- **Prerequisiti:** accesso alla raccolta dati di Adobe Experience Platform e Adobe Experience Platform.
- **Descrizione:** In questo modulo fondamentale, acquisirai dati dal sito Web in Platform
- **Investimento nel tempo:** 120 minuti

[1.3 Federated Audience Composition](./modules/datacollection/module1.3/fac.md)

- **Pubblico:** Analista dati, Ingegnere dati, Architetto dati
- **Prerequisiti:** accesso a Adobe Experience Platform
- **Descrizione:** In questo modulo imparerai a configurare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e inviare dati in streaming a Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink per Kafka Connect.
- **Investimento nel tempo:** 90 minuti

### 2. Real-Time CDP B2C

[2.1 Foundation - Profilo cliente in tempo reale](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Addetto marketing
- **Prerequisiti:** accesso a Adobe Experience Platform e Postman
- **Descrizione:** In questo modulo fondamentale, esplorerai il Profilo cliente in tempo reale in Adobe Experience Platform utilizzando l&#39;interfaccia utente e l&#39;API.
- **Investimento nel tempo:** 90 minuti
- **Scarica queste risorse**:
   - [Raccolte Postman](./assets/postman/postman_profile.zip)

[2.2 Servizi intelligenti](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Scienziato dati
- **Prerequisiti:** accesso a Adobe Experience Platform, Intelligent Services
- **Descrizione:** In questo modulo imparerai a configurare, configurare e utilizzare Adobe Experience Platform Intelligent Services.
- **Investimento nel tempo:** 60 minuti

[2.3 Real-Time CDP - Creare un segmento e intervenire](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

- **Pubblico:** Architetto di dati, Ingegnere di orchestrazione, Addetto marketing
- **Prerequisiti:** accesso a Adobe Experience Platform, Real-time CDP, Adobe Audience Manager, Adobe Target, AWS S3
- **Descrizione:** In questo modulo configurerai un segmento, attivalo per la segmentazione in streaming e attiverai il segmento in diverse destinazioni, tra cui Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target e destinazioni S3 come Salesforce Marketing Cloud.
- **Investimento nel tempo:** 90 minuti

[2.4 Real-Time CDP: attivazione dei segmenti in Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Analista dati
- **Prerequisiti:** accesso a Adobe Experience Platform, Real-time CDP e Microsoft Azure
- **Descrizione:** In questo modulo verrà impostata una destinazione EventHub di Microsoft Azure come destinazione in tempo reale per Adobe Experience Platform Real-time CDP. Puoi anche configurare e distribuire una funzione di Azure che verrà attivata in tempo reale ogni volta che Adobe Experience Platform distribuisce un payload di segmento alla destinazione di Azure EventHub. La funzione di Azure che verrà attivata mostrerà il meccanismo delle funzionalità di attivazione di Adobe Experience Platform Real-time CDP.
Come parte di questo modulo, comprenderai anche cosa attiva Real-time CDP per consegnare effettivamente un payload a una destinazione specifica. Vengono inoltre illustrati lo stato di qualificazione di un segmento e il modo in cui si relaziona all’attivazione.
- **Investimento nel tempo:** 90 minuti

[2.5 Connessioni Real-Time CDP: Inoltro eventi](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Analista dati
- **Prerequisiti:** accesso alle proprietà di connessioni, tag e inoltro eventi di Real-Time CDP
- **Descrizione:** In questo modulo verranno utilizzati i set di dati, gli schemi e le proprietà Raccolta dati di Adobe Experience Platform configurati in precedenza per raccogliere i dati e quindi inoltrarli lato server a un endpoint di scelta.
- **Investimento nel tempo:** 90 minuti

[2.6 Trasmettere dati da Apache Kafka a Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

- **Pubblico:** Analista dati, Ingegnere dati, Architetto dati
- **Prerequisiti:** accesso a Adobe Experience Platform
- **Descrizione:** In questo modulo imparerai a configurare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e inviare dati in streaming a Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink per Kafka Connect.
- **Investimento nel tempo:** 90 minuti

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orchestrazione](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Ingegnere orchestrazione
- **Prerequisiti:** accesso a Adobe Experience Platform e Adobe Journey Optimizer
- **Descrizione:** In questo modulo utilizzerai Adobe Journey Optimizer per creare un percorso basato su trigger.
- **Investimento nel tempo:** 60 minuti

[3.2 Adobe Journey Optimizer: origini dati esterne e azioni personalizzate](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Ingegnere orchestrazione, Addetto marketing
- **Prerequisiti:** Accesso a Adobe Experience Platform, Adobe Journey Optimizer, API Open Weather, Twilio
- **Descrizione:** In questo modulo utilizzerai Adobe Journey Optimizer per ascoltare il comportamento del cliente, online e offline, e per rispondervi in modo intelligente, contestuale e in tempo reale su vari canali.
- **Investimento nel tempo:** 90 minuti

[3.3 Adobe Journey Optimizer: Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Ingegnere orchestrazione, Addetto marketing
- **Prerequisiti:** Accesso a Adobe Experience Platform e Offer Decisioning
- **Descrizione:** In questo modulo utilizzerai il servizio applicativo Adobe Experience Platform - Offerte/Decisioning direttamente per configurare le offerte personalizzate e la tua attività di offerta.
- **Investimento nel tempo:** 120 minuti

[3.4 Adobe Journey Optimizer: Percorsi basati su eventi](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

- **Pubblico:** E-mail addetto al marketing, Specialista in orchestrazione, Ingegnere dati, Architetto dati, Analista dati
- **Prerequisiti:** accesso a Adobe Experience Platform e Journey Optimizer
- **Descrizione:** In questo modulo imparerai tutto ciò che c&#39;è da sapere su Journey Optimizer, il che aiuta le aziende a progettare e fornire ai propri clienti esperienze connesse, contestuali e personalizzate.
- **Investimento nel tempo:** 120 minuti

### 4. Adobe Customer Journey Analytics

[4.1 Customer Journey Analytics: creare una dashboard utilizzando Analysis Workspace su Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Analista dati
- **Prerequisiti:** Accesso a Adobe Experience Platform e Customer Journey Analytics
- **Descrizione:** In questo modulo, potrai accedere agli approfondimenti offline configurando un dashboard contenente dati omni-channel come interazioni con siti web, interazioni con app mobili, interazioni con call center, interazioni con in-store e molto altro.
- **Investimento nel tempo:** 120 minuti

[4.2 Customer Journey Analytics: inserire e analizzare i dati Google Analytics in Adobe Experience Platform con il connettore Source BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Analista dati
- **Prerequisiti:** accesso a Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Descrizione:** In questo modulo, configurerai la tua istanza di Google Cloud Platform, carica i dati demo in Google Cloud Platform e quindi utilizzerai il connettore BigQuery Source per acquisire tali dati da Google Cloud Platform in Adobe Experience Platform. Infine, utilizzerai il Customer Journey Analytics per visualizzare tali dati.
- **Investimento nel tempo:** 120 minuti
- **Scarica queste risorse**:
   - [JSON - Dati di esempio: demo - Dati fedeltà](./assets/json/bqLoyalty.json)

### 5. Data Distiller

[5.1 Servizio query](./modules/datadistiller/module5.1/query-service.md)

- **Pubblico:** Ingegnere dati, Architetto dati, Analista dati, Esperto BI
- **Prerequisiti:** accesso a Adobe Experience Platform, Query Service, Power BI o Tableau
- **Descrizione:** In questo modulo imparerai a utilizzare Adobe Experience Platform Query Service.
- **Investimento nel tempo:** 90 minuti
- **Scarica queste risorse**:
   - [JSON - Dati di esempio: Demo System - Set di dati evento per il sito web](./assets/json/ee.json)
   - [JSON - Dati di esempio: sistema demo - set di dati evento per call center](./assets/json/callcenter.json)
   - [JSON - Dati di esempio: Demo System - Set di dati profilo per fedeltà](./assets/json/loyalty.json)





