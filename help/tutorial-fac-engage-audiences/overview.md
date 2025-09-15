---
title: Coinvolgi i tipi di pubblico utilizzando la composizione federata dei tipi di pubblico
description: Scopri la Federated Audience Composition (FAC) e come consente agli architetti di dati e ai data engineer di curare e attivare tipi di pubblico di alto valore direttamente dai data warehouse supportati.
breadcrumb-title: Panoramica
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: e7484bcb8fa643a5c86b7d97da8c45d333e2e0ae
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Coinvolgi i tipi di pubblico da Data Warehouse utilizzando la Federated Audience Composition

Federated Audience Composition (FAC) è un modulo per Adobe Real-Time Customer Data Platform (Real-Time CDP) e Adobe Journey Optimizer. È disponibile anche con Adobe Real-Time CDP Composable Audiences (una soluzione personalizzata per i clienti come CDP componibile). Consente agli architetti e ai data engineer di curare e attivare tipi di pubblico di alto valore direttamente dai [data warehouse aziendali supportati](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}, senza copiare o spostare i dati dei clienti in Adobe Experience Platform (AEP). Questo approccio CDP componibile (una soluzione personalizzata per i clienti) è in linea con le tendenze del settore, consentendo alle aziende di sfruttare la propria infrastruttura di dati per esperienze digitali personalizzate mantenendo al contempo la governance dei dati.

## Contesto aziendale

SecurFinancial è una società leader nel settore dei servizi finanziari. Sfrutta la ricchezza di dati dei clienti da diverse origini per personalizzare offerte e campagne per un gran numero di segmenti. Prevedono di utilizzare il modulo Federated Audience Composition di Adobe Real-Time CDP, che consente alle aziende di utilizzare il data warehouse per la gestione dei dati e al tempo stesso di utilizzare Experience Platform per fornire esperienze cliente personalizzate. I vantaggi principali includono:

- **Accesso ai dati warehouse**: crea tipi di pubblico di alto valore dai set di dati nei data warehouse supportati senza replica dei dati.
- **Spostamento dei dati ridotto al minimo**: esegui query sui dati direttamente nel data warehouse, senza duplicazione e senza gestione della governance dei dati.
- **Flussi di lavoro di esperienza unificati**: cura e attiva i tipi di pubblico in Adobe Experience Platform per i casi di utilizzo cross-channel.
- **Personalizzazione avanzata**: arricchisci profili e tipi di pubblico con attributi di magazzino per sviluppare esperienze attivate in tempo reale.

## Scenario aziendale

SecurFinancial desidera lanciare una campagna e-mail per il retargeting dei propri clienti che sono prequalificati per un prestito basato su un buon credito e non hanno un prestito attivo nel loro portafoglio SecurFinancial. Durante l’acquisizione di dati comportamentali online in tempo reale, si trovano ad affrontare difficoltà nell’identificazione della preselezione del cliente, in quanto non possono acquisire informazioni sul credito in AEP. Per qualificare i clienti pre-qualificati senza spostare dati limitati, utilizzeranno Federated Audience Composition per arricchire il loro pubblico comportamentale AEP.

## Guida

In questa guida viene illustrato il supporto dello scenario SecureFinancial Business. In particolare, illustra come esponiamo i tipi di pubblico ai sistemi che ne hanno bisogno, tra cui un account di archiviazione S3, un percorso in Journey Optimizer per promuovere una campagna e-mail e il retargeting on-site ai clienti che hanno ricevuto una pre-approvazione per un prestito.

I passaggi, includono:

1. Connettere Adobe Experience Platform a un data warehouse aziendale.
2. Crea un pubblico utilizzando Federated Audience Composition.
3. Mappa un pubblico federato su una destinazione esterna di Amazon S3.
4. Crea un percorso di clienti utilizzando i dati del pubblico federato.
5. Arricchire un pubblico con dati federati.
6. Promuovi la personalizzazione &quot;nel momento&quot; su Edge.

## Prerequisiti

Per eseguire attività simili nell’ambiente, assicurati di disporre di:

- Accesso a un account Adobe Experience Platform fornito con Real-Time CDP o Journey Optimizer.
- Autorizzazioni di amministratore di sistema o la possibilità di configurare le autorizzazioni.
- Familiarità con i concetti di Adobe Experience Platform, ad esempio schemi, set di dati e tipi di pubblico (consigliato: completare la [Introduzione alla playlist di Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} su Experience League).
- Accesso a un data warehouse aziendale [supportato](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}.
- Conoscenza di base di SQL per l&#39;esecuzione di query nei data warehouse.
- **Ambienti sandbox**: crea una sandbox nell&#39;istanza della tua organizzazione per fare esperimenti in sicurezza senza influire sui dati di produzione.
- **Connessione Data Warehouse**: questa esercitazione utilizza una connessione Snowflake, ma è possibile utilizzare qualsiasi [data warehouse supportato](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Analizziamo innanzitutto l&#39;[architettura di alto livello e flusso per la composizione federata del pubblico](fac-architecture-and-flow.md).
