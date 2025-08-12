---
title: Sblocca le informazioni cross-channel con Federated Audience Composition
description: La Federated Audience Composition è una funzione potente che consente agli architetti e agli ingegneri di dati di creare e arricchire tipi di pubblico direttamente dai data warehouse di terze parti.
breadcrumb-title: Panoramica
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Panoramica

Federated Audience Composition è una potente funzione disponibile per gli ambienti Adobe Real-Time Customer Data Platform (Real-Time CDP) e Adobe Journey Optimizer. Consente agli architetti di dati e ai data engineer di generare e arricchire tipi di pubblico direttamente da data warehouse di [terze parti supportati](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} senza replicare i dati in Adobe Experience Platform. Questa esercitazione fornisce indicazioni pratiche agli utenti tecnici per collegare data warehouse aziendali, creare e arricchire tipi di pubblico e attivarli per esperienze di marketing personalizzate.

## Finalità di apprendimento

Completando questa esercitazione:

- Informazioni su come collegare Adobe Experience Platform a un data warehouse aziendale.
- Scopri come creare e gestire i tipi di pubblico utilizzando Federated Audience Composition.
- Scopri come arricchire i tipi di pubblico esistenti con i dati di magazzino.
- Mappa i tipi di pubblico federati su destinazioni esterne come Amazon S3.
- Crea percorsi di clienti utilizzando i dati del pubblico federato.
- Convalidare dati e processi tramite esercitazioni pratiche e demo.

Questo tutorial è progettato per architetti e ingegneri di dati che lavorano con Real-Time CDP o Journey Optimizer. È necessario acquisire familiarità con i concetti di Adobe Experience Platform e data warehouse di base.

## Contesto di business

SecurFinancial è una società leader nel settore dei servizi finanziari. Sfrutta la ricchezza di dati dei clienti da diverse origini per personalizzare offerte e campagne per un gran numero di segmenti. Pianificano di utilizzare la funzione Federated Audience Composition di Adobe per Real-Time CDP, che consente alle aziende di utilizzare il data warehouse esistente e al tempo stesso di utilizzare le applicazioni di Adobe Experience Platform per fornire esperienze cliente personalizzate. I vantaggi principali includono:

- **Accesso ai dati warehouse**: crea tipi di pubblico di alto valore dai set di dati nei data warehouse supportati senza replica dei dati.
- **Spostamento dei dati ridotto al minimo**: esegui query sui dati direttamente nel data warehouse, riducendo la duplicazione e mantenendo la governance dei dati.
- **Flussi di lavoro di esperienza unificati**: cura e attiva i tipi di pubblico in Adobe Experience Platform per i casi di utilizzo cross-channel.
- **Personalizzazione avanzata**: arricchisci profili e tipi di pubblico con attributi di magazzino per sviluppare esperienze attivate in tempo reale.

## Scenario di business

SecurFinancial desidera lanciare una campagna e-mail per il retargeting dei propri clienti che sono prequalificati per un prestito basato su un buon credito e non hanno un prestito attivo nel loro portafoglio SecurFinancial. Mentre acquisiscono dati comportamentali online in tempo reale, devono affrontare problemi nell’identificazione della prequalificazione del cliente, in quanto non possono acquisire informazioni sul credito in AEP. Per qualificare i clienti prequalificati senza spostare dati soggetti a restrizioni, utilizzeranno Federated Audience Composition per arricchire il loro pubblico comportamentale di AEP.



## Prerequisiti

Per seguire questa esercitazione, assicurati di disporre di:

- Accesso a un account Adobe Experience Platform fornito con Real-Time CDP o Journey Optimizer.
- Autorizzazioni di amministratore di sistema o la possibilità di configurare le autorizzazioni.
- Familiarità con i concetti di Adobe Experience Platform, ad esempio schemi, set di dati e tipi di pubblico (consigliato: completare la [Introduzione alla playlist di Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} su Experience League).
- Accesso a un data warehouse aziendale supportato (ad esempio, Amazon Redshift, Azure Synapse Analytics, Snowflake o Google BigQuery).
- Conoscenza di base di SQL per l&#39;esecuzione di query nei data warehouse.

## Utilizzo di questo tutorial

Questo tutorial è strutturato per gli utenti tecnici. Le lezioni si basano l’una sull’altra, quindi completale in ordine, se non diversamente indicato.

## Note tecniche

- **Ambienti sandbox**: crea una sandbox nell&#39;istanza Real-Time CDP della tua organizzazione per fare delle prove in sicurezza senza influire sui dati di produzione.
- **Connessione Data Warehouse**: questa esercitazione utilizza una connessione Snowflake, ma è possibile utilizzare qualsiasi [data warehouse cloud supportato](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Inizia con la lezione [Connessione Data Warehouse](data-warehouse-connection.md) per iniziare a configurare l&#39;ambiente.
