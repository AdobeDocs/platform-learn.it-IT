---
title: Raccolta dati - Composizione federata del pubblico
description: Raccolta dati - Composizione federata del pubblico
kt: 5342
doc-type: tutorial
exl-id: 44660f3e-0594-4578-9531-1c918992aa9d
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 1.3 Federated Audience Composition

**Autore: [Ludovic Latapie](https://www.linkedin.com/in/ludoviclatapie/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo, l’obiettivo è quello di imparare tutto quello che c’è da sapere sulla creazione di tipi di pubblico utilizzando la Federated Audience Composition.

La Federated Audience Composition (FAC) in Experience Platform consente di accedere e creare tipi di pubblico con gli attributi di alto valore corrispondenti dai data warehouse aziendali, che arricchiscono e integrano il profilo cliente in tempo reale e i tipi di pubblico in Experience Platform per migliorare la segmentazione, il targeting, l’attivazione e la consegna di esperienze cliente significative. Utilizzando Federated Audience Composition, viene creato un database virtuale collegando i database remoti tramite i metadati. Questo approccio semplifica l&#39;accesso, riduce la duplicazione e migliora l&#39;esperienza dell&#39;utente finale. Ai team viene concessa la flessibilità di acquisire i set di dati direttamente in set di dati di Experience Platform o di accesso che risiedono in data warehouse durante l’assemblaggio dei tipi di pubblico per i flussi di lavoro di coinvolgimento. Questo approccio sfrutta gli investimenti e le risorse di data warehouse per integrare Real-Time CDP e Journey Optimizer. Federated Audience Composition consente ai clienti di utilizzare e combinare funzionalità batch e in tempo reale in nuovi modelli di utilizzo critici:

- Segmentazione federata del pubblico: un team può creare un pubblico utilizzando l’interfaccia utente di composizione del pubblico con funzionalità di trascinamento intuitiva in Real-Time CDP e Journey Optimizer, ma con una query inviata al data warehouse, che lascia i dati sottostanti sensibili nel warehouse senza duplicazioni e fornisce un accesso flessibile ai set di dati essenziali.
- Arricchimento del pubblico: i tipi di pubblico incorporati in Real-Time CDP e Journey Optimizer possono essere arricchiti con dati aziendali aggiuntivi per migliorare il targeting e la personalizzazione con set di dati aggiuntivi basati su profili e non basati su profili che non persisteranno in Adobe Experience Platform. Ad esempio, un marchio di commercio al dettaglio può integrare un pubblico di recenti acquirenti online con un elenco di luoghi principali per creare un pubblico per una promozione cross-channel online e in-store.
- Arricchimento del profilo: i team possono selezionare dal data warehouse gli attributi del profilo che sono fondamentali per le esperienze nel momento da mantenere nei profili cliente fruibili residenti in Real-Time CDP e a cui si accede tramite Journey Optimizer. Questi punti di dati aggiuntivi sono quindi disponibili per la segmentazione a valle e la personalizzazione attivata da comportamenti evento a seconda dell’azione dell’utente e del caso di utilizzo del cliente. Questo consentirà agli attributi portati con tipi di pubblico federati di essere disponibili per la segmentazione e la personalizzazione nel momento, insieme ad altri attributi e segnali comportamentali mantenuti in un profilo cliente.

La Federated Audience Composition offre ai clienti di Real-Time CDP e Journey Optimizer la flessibilità di decidere quali dati utilizzare quando e aiuta a evitare set di dati o modelli di integrazione inutilmente duplicati. Ciò rappresenta una combinazione unica di un approccio federato all’utilizzo di dati aziendali per la cura di tipi di pubblico e attributi di alto valore, combinata con un sistema ottimizzato per un coinvolgimento immediato su più canali. Questo offre meno spostamento dei dati, ma anche nuove opportunità per utilizzare tipi di pubblico e attributi di alto valore per un’attivazione coerente a bassa latenza tra i canali.

## Finalità di apprendimento

- Scopri come collegare il Snowflake con Adobe Experience Platform
- Scopri come creare un modello dati per i dati federati in Adobe Experience Platform
- Scopri come creare composizioni di pubblico federato in Adobe Experience Platform

## Prerequisiti

- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accesso a un data warehouse di Snowflake

## Esercizi

[1.3.1 Configurare l’account di Snowflake](./ex1.md)

In questo esercizio, configurerai l’account di prova di Snowflake e lo connetterai a Adobe Experience Platform

[1.3.2 Creare schemi, modelli di dati e collegamenti](./ex2.md)

In questo esercizio configurerai il modello dati in AEP per i dati federati.

[1.3.3 Creare una composizione federata](./ex3.md)

In questo esercizio configurerai il modello dati in AEP per i dati federati.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all&#39;apprendimento di tutto ciò che c&#39;è da sapere su Adobe Experience Platform e sulle sue applicazioni. Se hai domande, vuoi condividere feedback generali su suggerimenti in merito a contenuti futuri, contatta direttamente Tech Insiders, inviando un&#39;e-mail a **techinsiders@adobe.com**.

[Torna a tutti i moduli](../../../overview.md)
