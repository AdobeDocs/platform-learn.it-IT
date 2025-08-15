---
title: Federated Audience Composition Architettura e flusso di alto livello
seo-title: Federated Audience Composition high-level architecture & flow | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Architettura e flusso di alto livello di Federated Audience Composition
description: Panoramica dell’architettura di alto livello e del flusso di Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-high-level-architecture.jpg
exl-id: 4cb0b730-4206-476b-93d9-776dfbd464ff
source-git-commit: 0564f516cfba7ea09ac9da19d94f46d984e9e00a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Architettura e flusso di alto livello di Federated Audience Composition

Prima di approfondire i passaggi per il supporto dello scenario aziendale per SecurFinancial, esamineremo l&#39;architettura di alto livello e il flusso per questo approccio CDP componibile.

Il modulo Federated Audience Composition in Adobe Experience Platform estende l’accesso ai set di dati del data warehouse senza copiare i dati sottostanti, riducendo al minimo lo spostamento e la duplicazione dei dati.

Questo fornisce anche alle organizzazioni l&#39;architettura componibile richiesta, che hanno già completato il lavoro di gestione dei dati richiesto nel loro magazzino e desiderano utilizzare un modello a copia zero in cui Adobe Experience Platform diventa il motore del coinvolgimento.

Consente alle aziende di elaborare rapidamente le informazioni archiviate in uno o più data warehouse. Elimina la necessità di acquisire dati in Adobe Experience. Inoltre, consente di accedere a nuovi set di dati che risiedono nei data warehouse aziendali ma che fino ad ora sono stati inaccessibili per i flussi di lavoro dell’esperienza del cliente. Alcuni esempi possono includere transazioni storiche o dati personali che saranno utili a livello di pubblico aggregato per il coinvolgimento del cliente.

![fac-architecture](assets/fac-architecture.png)

Ora passeremo alla creazione di una [connessione Data Warehouse](data-warehouse-connection.md).
