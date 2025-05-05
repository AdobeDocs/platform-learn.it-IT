---
title: Migrare la tua app mobile da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning
description: Scopri come migrare l’implementazione della tua app mobile da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---

# Migrare la tua app mobile da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning

Questa guida è rivolta agli utenti con esperienza che implementano Adobe Target, per scoprire come migrare le implementazioni esistenti di Adobe Experience Platform dalle implementazioni di Mobile SDK dall’estensione Adobe Target all’estensione Adobe Journey Optimizer - Decisioning.

Adobe Experience Platform Mobile SDK potenzia il coinvolgimento end-to-end nelle applicazioni mobili. L&#39;estensione Target si basa su Mobile SDK per aiutarti a personalizzare le esperienze dell&#39;app con Adobe Target. L’estensione Decisioning è un approccio più recente per implementare Adobe Target nelle app per dispositivi mobili che utilizza le funzionalità di Adobe Experience Platform Edge Network che consentono di integrare Target con app basate su piattaforma, come Real-Time CDP e Journey Optimizer.

![Diagramma che mostra la connessione di Mobile SDK a Target tramite Edge Network con l&#39;estensione Decisioning](assets/datacollection.png)

## Vantaggi chiave

Alcuni dei vantaggi dell’estensione Adobe Journey Optimizer Decisioning rispetto all’estensione Target includono:

* Condivisione più rapida dei tipi di pubblico da [Real-Time Customer Data Platform](https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)
* Integrazione di Target con Journey Optimizer per supportare la [consegna Offer Decisioning](https://experienceleague.adobe.com/it/docs/target/using/integrate/ajo/offer-decision)
* Un’integrazione più stretta con Adobe Analytics che non si basa sull’unione delle informazioni da chiamate di rete separate
* Maggiore flessibilità di implementazione per gli sviluppatori

Probabilmente, il vantaggio più grande per i clienti di Target della migrazione è l&#39;integrazione con Real-Time Customer Data Platform. Real-Time CDP offre straordinarie funzionalità per la creazione di tipi di pubblico in base alla gamma completa di dati acquisiti in Experience Platform e alla sua funzionalità Profilo cliente in tempo reale. Un framework integrato di governance dei dati automatizza l’uso responsabile di tali dati. IA per l’analisi dei clienti consente di utilizzare facilmente i modelli di apprendimento automatico per creare modelli di propensione e abbandono il cui output può essere condiviso su Adobe Target. Infine, i clienti dei componenti aggiuntivi opzionali di Healthcare and Privacy &amp; Security Shield possono utilizzare la funzione di applicazione del consenso per applicare le preferenze di consenso dei singoli clienti. Platform Mobile SDK e l’estensione Decisioning sono requisiti necessari per utilizzare queste funzioni Real-Time CDP nel canale mobile.

## Passaggi di migrazione

Il livello di impegno per la migrazione dall’estensione Target all’estensione Decisioning dipende dalla complessità dell’implementazione corrente e delle funzioni di Target utilizzate.

Indipendentemente dalla semplicità o dalla complessità dell’implementazione, è importante comprendere appieno lo stato corrente prima di eseguire la migrazione. Questa guida ti aiuta a suddividere i componenti dell’implementazione corrente e a sviluppare un piano gestibile per migrare ogni elemento.

Il processo di migrazione prevede i seguenti passaggi chiave:

1. Valuta l’implementazione corrente, tra cui:
   1. Tutte le API SDK di Target utilizzate
   1. Modifiche alle impostazioni globali di Target
   1. Integrazione con Adobe Analytics
   1. Utilizzo di parametri mbox, di profilo ed entità
   1. Utilizzo di script di profilo e pubblico
   1. Codice personalizzato univoco per l’implementazione
1. Configurare i componenti iniziali per la connessione a Adobe Experience Platform Edge Network
1. Aggiorna l’implementazione fondamentale per sostituire l’estensione Target con l’estensione Decisioning
1. Migliora l’implementazione Ottimizza SDK per casi d’uso specifici. Questo può comportare il passaggio di parametri aggiuntivi, l’utilizzo di token di risposta e altro ancora.
1. Aggiornare oggetti nell’interfaccia di Target, ad esempio script di profilo, attività e definizioni di pubblico
1. Convalida l’implementazione finale prima di effettuare il passaggio nell’app di produzione


>[!INFO]
>
>Nell’ecosistema di Adobe Experience Platform Mobile SDK, le estensioni vengono implementate dagli SDK importati nelle applicazioni che possono avere nomi diversi:
>
> * **Target SDK** implementa l&#39;estensione **Adobe Target**
> * **Ottimizza SDK** implementa l&#39;estensione **Adobe Journey Optimizer - Decisioning**

Rivedi quindi il confronto dettagliato [tra l&#39;estensione Target e l&#39;estensione Decisioning](comparison.md) per comprendere meglio le differenze tecniche e identificare le aree che richiedono un&#39;attenzione aggiuntiva.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
