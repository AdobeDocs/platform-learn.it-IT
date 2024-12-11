---
title: Migrare Target da at.js 2.x a Web SDK
description: Scopri come migrare un’implementazione di Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK. Gli argomenti includono il caricamento della libreria JavaScript, l’invio di parametri, le attività di rendering e altri callout rilevanti.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: 485e79e3569052184475fbc49ab5f43cebcac9a6
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 4%

---

# Migrare Target da at.js 2.x a Platform Web SDK

Questa guida è rivolta agli implementatori esperti di Adobe Target per scoprire come migrare un’implementazione at.js a Adobe Experience Platform Web SDK.

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti Adobe Experience Cloud di interagire con i servizi Experience Cloud tramite l’Edge Network Adobe Experience Platform. Questa nuova libreria combina le funzionalità delle librerie di applicazioni Adobe separate in un unico pacchetto leggero in grado di sfruttare appieno le nuove funzioni di Adobe Experience Platform.

## Vantaggi chiave

Alcuni dei vantaggi di Platform Web SDK rispetto alla libreria at.js indipendente includono:

* Condivisione più rapida dei tipi di pubblico da [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=it)
* Integrazione di Target con Journey Optimizer per supportare [la consegna di Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Possibilità di utilizzare [ID di prime parti](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=it) per generare l&#39;ECID per l&#39;identificazione dei visitatori di durata maggiore
* Ingombro ridotto per metriche di velocità di pagina migliorate
* Maggiore flessibilità di implementazione per gli sviluppatori

Probabilmente, il vantaggio più grande per i clienti di Target della migrazione è l&#39;integrazione con Real-time Customer Data Platform. Real-Time CDP offre straordinarie funzionalità per la creazione di tipi di pubblico, basate sulla gamma completa di dati acquisiti in Experience Platform e sulla sua funzionalità Profilo cliente in tempo reale. Un framework integrato di governance dei dati automatizza l’utilizzo responsabile di tali dati. IA per l’analisi dei clienti consente di utilizzare facilmente i modelli di apprendimento automatico per creare modelli di propensione e abbandono il cui output può essere condiviso su Adobe Target. Infine, i clienti dei componenti aggiuntivi opzionali Healthcare e Privacy &amp; Security Shield possono utilizzare la funzione di applicazione del consenso per applicare facilmente le preferenze di consenso dei singoli clienti. Platform Web SDK è un requisito necessario per utilizzare queste funzioni di Real-Time CDP nel canale web.

## Obiettivi di apprendimento

Al termine dell&#39;esercitazione, saprai:

* Comprendere le differenze di implementazione di Target tra at.js e Platform Web SDK
* Configurare la configurazione iniziale per la funzionalità di Target
* Aggiornare la libreria at.js a Platform Web SDK
* Attività del compositore esperienza visivo e basato su moduli
* Trasmettere i parametri a Target
* Tracciare gli eventi di conversione
* Abilita supporto tra più domini
* Aggiornare tipi di pubblico e script di profilo
* Convalida l&#39;implementazione
* Debug della consegna delle esperienze Target


## Prerequisiti

Per completare questa esercitazione, devi prima:

* Avere una conoscenza tecnica dell’attuale implementazione di Target at.js
* Assicurati di avere un [ruolo Editor o Editore](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) per l&#39;istanza di Target in modo da poter provare gli esempi autonomamente
* Scopri come impostare le attività in Adobe Target. Se hai bisogno di un aggiornamento, i seguenti tutorial e guide sono utili per questa lezione:
   * [Utilizzare il Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Utilizzare il Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Crea attività di targeting esperienze](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Quando sei pronto, il primo passaggio per una migrazione corretta è [scoprire il processo di migrazione](migration-overview.md) e le differenze tra at.js e Platform Web SDK.

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
