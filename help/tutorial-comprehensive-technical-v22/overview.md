---
title: Panoramica
description: Punto di partenza per data engineer, Data Analysts, Data Architects, Data Scientists, Orchestration Engineers e Marketing per acquisire una piena comprensione del valore aziendale di Adobe Experience Platform e di tutti i suoi Application Services.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 1%

---

# Tutorial tecnico completo per Adobe Experience Platform

## Panoramica

Questa esercitazione è il punto di partenza ideale per data engineer, Data Analysts, Data Architects, Data Scientists, Orchestration Engineers e Marketing per acquisire una comprensione completa del valore aziendale di Adobe Experience Platform e di tutti i suoi servizi applicativi. Ogni lezione si concentra su una vera sfida che le aziende devono affrontare nel complesso ecosistema di personalizzazione di oggi e scompone il modo in cui l&#39;Experience Platform risolve quella sfida in diversi esercizi pratici. Guarda questo video per capire i problemi che Adobe Experience Platform ti aiuterà a risolvere.

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

Questa esercitazione è molto diversificata e offre informazioni chiare nelle seguenti applicazioni:

- Adobe Experience Platform
- Raccolta dati di Adobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics
- Offer Decisioning

Questa esercitazione non si concentra solo sulle applicazioni di Adobe, ma prende in considerazione l&#39;ecosistema più ampio in cui operano i marchi. Per fare questo, in alcune lezioni c&#39;è un&#39;attenzione su come _non Adobe_ le applicazioni si integrano con Adobe Experience Platform. Di conseguenza, potrai scoprire in modo approfondito come le seguenti applicazioni funzioneranno insieme a Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Piattaforma Google Cloud, BigQuery Google, Display&amp;Video Google 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Azure Blob Storage
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

Dopo aver completato questa esercitazione, sarai in grado di:

- Configurazione di schemi, mixer, set di dati e identità
- Configura una proprietà Adobe Experience Platform Data Collection e imposta la nuova estensione Web SDK nella raccolta dati di Adobe Experience Platform
- Trasmetti i dati in Adobe Experience Platform in tempo reale utilizzando Adobe Experience Platform Data Collection, Google Tag Manager o Amazon Alexa
- Acquisizione in batch di dati in Adobe Experience Platform utilizzando un flusso di lavoro o un’applicazione di estrazione, trasformazione, caricamento (ETL)
- Visualizzare e utilizzare il profilo cliente in tempo reale in Adobe Experience Platform
- Creare segmenti
- Utilizzare diverse API di Adobe Experience Platform
- Utilizzare SQL per eseguire query sui dati in Adobe Experience Platform
- Configurare, addestrare e valutare modelli di apprendimento automatico in Adobe Experience Platform
- Utilizza il Journey Orchestration per configurare percorsi basati su trigger in tempo reale
- Utilizzare Real-time CDP per intervenire attivando un segmento in varie destinazioni
- Utilizza il Customer Journey Analytics per creare rapporti sui dati dei clienti omnicanale da varie fonti, tra cui Google BigQuery

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso alla raccolta dati di Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accesso a Demo System: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Informazioni su questa esercitazione

In queste lezioni, implementerai Adobe Experience Platform e Application Services utilizzando un sito web demo che supporta più settori. Il sito web demo e l’app mobile dispongono di un livello dati e funzionalità avanzati che consentono di realizzare un’implementazione realistica. Consente l&#39;accesso a marchi demo come **Luma**, **Segnale Citi**, **Notizie EXP**, **MUTUAL365**, **Carvelo** e molti altri. Potrai creare la tua proprietà Adobe Experience Platform Data Collection Client nella tua organizzazione di Experience Cloud e mapparla sul tuo sito web dimostrativo. Questo genererà quindi i dati inviati nella tua istanza Adobe Experience Platform.

## Architettura

Prima di iniziare con gli esercizi pratici, consulta l’architettura alla base di questo tutorial. Come puoi vedere nella Panoramica di cui sopra, questa esercitazione approfondirà una serie di funzioni e funzionalità di Adobe Experience Platform, ma discuterà anche più integrazioni tra diverse origini e destinazioni. Per comprendere correttamente l’architettura alla base di questa esercitazione e il posizionamento complessivo di Adobe Experience Platform nell’ecosistema Enterprise, guarda innanzitutto il video e il diagramma dell’architettura.

Vai a [Architettura](./architecture.md).


## Video

![Videos](./assets/images/yt.jpeg)

Potete trovare un sacco di video interessanti dai nostri eventi di Tech Academy, da Bootcamp e altro ancora sul nostro [Canale YouTube della community Experience Maker](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

Sono stati creati diversi video che mostrano elementi dell’abilitazione e potenti integrazioni tra Adobe Experience Platform e applicazioni non Adobe. Fai clic sul collegamento seguente per trovare una panoramica di questi video.

Vai a [Video](./videos.md).



## Come viene misurato il completamento del tutorial tecnico completo per Adobe Experience Platform?

Se stai partecipando a questa esercitazione come partner di Adobe o dipendente di Adobe, devi inviare i tuoi progressi dopo aver completato ogni modulo di abilitazione.

Qui puoi trovare i requisiti e la procedura per l&#39;invio del completamento: [Misurazione del completamento](./completion.md)

## Contenuto

[0. Guida introduttiva](./modules/module0/getting-started.md)

- **Pubblico:** Tutti i partecipanti al tutorial tecnico completo per Adobe Experience Platform
- **Prerequisiti:** Accesso a Demo System Next, Adobe Experience Platform e Adobe Experience Platform Data Collection. Accedere all&#39;ID di configurazione predefinito dell&#39;ambiente Adobe Experience Platform.
- **Descrizione:** In questo modulo fondamentale, configurerai tutto in modo da poter accedere e utilizzare l&#39;ambiente demo.
- **Investimento nel tempo:** 30 minuti

[1. Foundation - Configurazione di Adobe Experience Platform Data Collection e Web SDK](./modules/module1/data-ingestion-launch-web-sdk.md)

- **Pubblico:** Data Engineer, Data Architect
- **Prerequisiti:** Accesso alla raccolta dati di Adobe Experience Platform e Adobe Experience Platform.
- **Descrizione:** In questo modulo fondamentale, scopri Adobe Experience Platform Data Collection e la nuova estensione Web SDK.
- **Investimento nel tempo:** 30 minuti

[2. Foundation - Acquisizione dei dati](./modules/module2/data-ingestion.md)

- **Pubblico:** Data Engineer, Data Architect
- **Prerequisiti:** Accesso alla raccolta dati di Adobe Experience Platform e Adobe Experience Platform.
- **Descrizione:** In questo modulo fondamentale, trasferirai dati dal sito web a Platform
- **Investimento nel tempo:** 120 minuti

[3. Struttura - Profilo cliente in tempo reale](./modules/module3/real-time-customer-profile.md)

- **Pubblico:** Data Engineer, Data Architect, addetto al marketing
- **Prerequisiti:** Accesso a Adobe Experience Platform e Postman
- **Descrizione:** In questo modulo fondamentale, esplorerai il Profilo del cliente in tempo reale in Adobe Experience Platform utilizzando l’interfaccia utente e l’API.
- **Investimento nel tempo:** 90 minuti
- **Scarica queste risorse**:
   - [Raccolte Postman](./assets/postman/postman_profile.zip)

[4. Servizio query](./modules/module4/query-service.md)

- **Pubblico:** Data Engineer, Data Architect, Data Analyst, BI Expert
- **Prerequisiti:** Accesso a Adobe Experience Platform, Query Service, Power BI o Tableau
- **Descrizione:** In questo modulo imparerai come utilizzare Adobe Experience Platform Query Service.
- **Investimento nel tempo:** 90 minuti
- **Scarica queste risorse**:
   - [JSON - Dati di esempio: Sistema demo - Set di dati evento per il sito web](./assets/json/ee.json)
   - [JSON - Dati di esempio: Sistema demo - Set di dati evento per Call Center](./assets/json/callcenter.json)
   - [JSON - Dati di esempio: Sistema demo - Set di dati profilo per fedeltà](./assets/json/loyalty.json)

[5. Servizi intelligenti](./modules/module5/intelligent-services.md)

- **Pubblico:** Data Engineer, Data Architect, Data Scientist
- **Prerequisiti:** Accesso a Adobe Experience Platform, servizi intelligenti
- **Descrizione:** Questo modulo illustra come configurare, configurare e utilizzare Adobe Experience Platform Intelligent Services.
- **Investimento nel tempo:** 60 minuti

[6. Real-Time CDP - Creazione di un segmento e azione](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **Pubblico:** Architetto dati, Ingegnere di orchestrazione, addetto al marketing
- **Prerequisiti:** Accesso a Adobe Experience Platform, Real-time CDP, Adobe Audience Manager, Adobe Target, AWS S3
- **Descrizione:** In questo modulo, configurerai un segmento, lo abiliterai per la segmentazione in streaming e attiverai il segmento in diverse destinazioni, tra cui Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target e destinazioni S3 come Salesforce Marketing Cloud.
- **Investimento nel tempo:** 90 minuti

[7. Adobe Journey Optimizer: Orchestrazione](./modules/module7/journey-orchestration-create-account.md)

- **Pubblico:** Ingegnere dati, architetto dati, ingegnere orchestrazione
- **Prerequisiti:** Accesso a Adobe Experience Platform e Adobe Journey Optimizer
- **Descrizione:** In questo modulo, utilizzerai Adobe Journey Optimizer per creare un percorso basato su trigger.
- **Investimento nel tempo:** 60 minuti

[8. Adobe Journey Optimizer: Origini dati esterne e azioni personalizzate](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **Pubblico:** Ingegnere dati, architetto dati, ingegnere orchestrazione, addetto al marketing
- **Prerequisiti:** Accesso a Adobe Experience Platform, Adobe Journey Optimizer, Open Weather API, Twilio
- **Descrizione:** In questo modulo, utilizzerai Adobe Journey Optimizer per ascoltare il comportamento dei clienti, sia online che offline, e rispondere ad esso in modo intelligente, contestuale e in tempo reale su vari canali.
- **Investimento nel tempo:** 90 minuti

[9. Adobe Journey Optimizer: offer decisioning](./modules/module9/offer-decisioning.md)

- **Pubblico:** Ingegnere dati, architetto dati, ingegnere orchestrazione, addetto al marketing
- **Prerequisiti:** Accesso a Adobe Experience Platform e Offer Decisioning
- **Descrizione:** In questo modulo, utilizzerai il servizio applicativo Adobe Experience Platform - Offerte/Decisioning in modo pratico per configurare offerte personalizzate e la tua attività di offerta.
- **Investimento nel tempo:** 120 minuti

[10. Adobe Journey Optimizer: Percorsi basati su eventi](./modules/module10/journeyoptimizer.md)

- **Pubblico:** Addetto al marketing e-mail, Specialista di orchestrazione, Ingegnere dati, Architetto dati, Analista dati
- **Prerequisiti:** Accesso a Adobe Experience Platform e Journey Optimizer
- **Descrizione:** In questo modulo imparerai tutto quello che c’è da sapere su Journey Optimizer, che aiuta le aziende a progettare e distribuire esperienze connesse, contestuali e personalizzate ai loro clienti.
- **Investimento nel tempo:** 120 minuti

[11. Customer Journey Analytics: Crea un dashboard utilizzando Analysis Workspace sopra Adobe Experience Platform](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **Pubblico:** Data Engineer, Data Architect, Data Analyst
- **Prerequisiti:** Accesso a Adobe Experience Platform e Customer Journey Analytics
- **Descrizione:** In questo modulo, puoi ottenere informazioni online su offline configurando un dashboard contenente dati omni-channel come Interazioni sito web, Interazioni app mobili, Interazioni call center, Interazioni in-store e molto altro.
- **Investimento nel tempo:** 120 minuti

[12. Customer Journey Analytics: Inserire e analizzare i dati delle Google Analytics in Adobe Experience Platform con il connettore sorgente BigQuery](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **Pubblico:** Data Engineer, Data Architect, Data Analyst
- **Prerequisiti:** Accesso a Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Descrizione:** In questo modulo, configurerai la tua istanza di Google Cloud Platform, caricherai i dati demo in Google Cloud Platform e quindi utilizzerai il Connettore origine BigQuery per acquisire i dati da Google Cloud Platform in Adobe Experience Platform. Infine, utilizzerai il Customer Journey Analytics per visualizzare tali dati.
- **Investimento nel tempo:** 120 minuti
- **Scarica queste risorse**:
   - [JSON - Dati di esempio: Demo - Dati fedeltà](./assets/json/bqLoyalty.json)

[13. Real-Time CDP: Attivazione del segmento nell’hub eventi di Microsoft Azure](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **Pubblico:** Data Engineer, Data Architect, Data Analyst
- **Prerequisiti:** Accesso a Adobe Experience Platform, Real-time CDP e Microsoft Azure
- **Descrizione:** In questo modulo, configurerai una destinazione Microsoft Azure EventHub come destinazione in tempo reale per Adobe Experience Platform Real-time CDP. Puoi anche impostare e distribuire una funzione di Azure che verrà attivata in tempo reale ogni volta che Adobe Experience Platform consegna un payload di segmento alla destinazione Azure EventHub. La funzione di Azure che verrà attivata mostrerà il meccanismo delle funzionalità di attivazione di CDP in tempo reale di Adobe Experience Platform.
Come parte di questo modulo, avrai anche una comprensione di ciò che attiva Real-time CDP per distribuire effettivamente un payload a una destinazione specifica. Discuteremo anche dello stato della qualifica di un segmento e di come si relaziona all’attivazione.
- **Investimento nel tempo:** 90 minuti

[14. Connessioni Real-Time CDP: Inoltro eventi](./modules/module14/aep-data-collection-ssf.md)

- **Pubblico:** Data Engineer, Data Architect, Data Analyst
- **Prerequisiti:** Accesso a connessioni Real-Time CDP, tag e proprietà di inoltro eventi
- **Descrizione:** In questo modulo, utilizzerai i set di dati, gli schemi e la proprietà di raccolta dati di Adobe Experience Platform configurati in precedenza per raccogliere i dati e quindi inoltrare tali dati lato server a un endpoint di scelta.
- **Investimento nel tempo:** 90 minuti

[15. Trasmetti i dati da Apache Kafka a Real-Time CDP](./modules/module15/aep-apache-kafka.md)

- **Pubblico:** Analista di dati, data engineer, Data Architect
- **Prerequisiti:** Accesso a Adobe Experience Platform
- **Descrizione:** In questo modulo imparerai come impostare il tuo cluster Apache Kafka, definire argomenti, produttori e consumatori e trasmettere dati in Adobe Experience Platform utilizzando il connettore Adobe Experience Platform Sink per Kafka Connect.
- **Investimento nel tempo:** 90 minuti

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.
