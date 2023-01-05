---
title: Introduzione | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come migrare un’implementazione Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK. Gli argomenti includono il caricamento della libreria JavaScript, l'invio di parametri, attività di rendering e altri callout degni di nota.
recommendations: catalog,noDisplay
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 5%

---

# Migrare Target da at.js 2.x a Platform Web SDK

Questa guida è destinata agli implementatori Adobe Target esperti che devono imparare a migrare un’implementazione at.js in Adobe Experience Platform Web SDK.

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti Adobe Experience Cloud di interagire con i servizi di Experience Cloud tramite Adobe Experience Platform Edge Network. Questa nuova libreria combina le funzionalità delle librerie di applicazioni Adobe separate in un unico pacchetto leggero che può sfruttare appieno le nuove funzionalità di Adobe Experience Platform.

## Vantaggi chiave

Alcuni dei vantaggi dell’SDK per web di Platform rispetto alla libreria at.js standalone includono:

* Condivisione più rapida dei tipi di pubblico da [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=it)
* Integrazione di Target con Journey Optimizer per supportare [Consegna di Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Possibilità di utilizzo [id di prime parti](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=it) per generare l’ECID per l’identificazione dei visitatori a più lungo termine
* Consolidamento delle chiamate di rete nelle applicazioni Adobe
* Un ingombro ridotto per migliorare le metriche di velocità della pagina
* Un’integrazione più stretta con Adobe Analytics che non si basa sull’unione di informazioni da chiamate di rete separate
* Maggiore flessibilità di implementazione per gli sviluppatori

Probabilmente, il vantaggio più grande della migrazione è per i clienti di Real-time Customer Data Platform. Real-Time CDP offre straordinarie funzionalità per la creazione di un pubblico, basate sull’intera gamma di dati acquisiti in Experience Platform e sulla sua funzionalità Profilo cliente in tempo reale. Un framework integrato per la governance dei dati automatizza l’utilizzo responsabile di tali dati. Customer AI consente di utilizzare facilmente i modelli di apprendimento automatico per creare modelli di propensione e abbandono il cui output può essere condiviso nuovamente in Adobe Target. Infine, i clienti degli addons opzionali Healthcare e Privacy &amp; Security Shield possono utilizzare la funzione di imposizione del consenso per applicare facilmente le preferenze di consenso dei singoli clienti. Platform Web SDK è un requisito per utilizzare queste funzioni RTCDP nel tuo canale web.

## Finalità di apprendimento

Al termine dell&#39;esercitazione, saprai:

* Comprendere le differenze di implementazione di Target tra at.js e Platform Web SDK
* Impostare la configurazione iniziale per la funzionalità di Target
* Aggiornare la libreria at.js all’SDK per web di Platform
* Rendering delle attività del compositore esperienza visivo e basato su moduli
* Trasmettere parametri a Target
* Tracciare gli eventi di conversione
* Abilitare il supporto tra più domini
* Aggiornare tipi di pubblico e script di profilo
* Convalida l&#39;implementazione
* Debug della consegna delle esperienze Target


## Prerequisiti

Per completare questa esercitazione, devi prima:

* Comprendere a livello tecnico l’implementazione at.js di Target corrente
* Assicurati di disporre di un [Ruolo Editor o Editore](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) per la tua istanza di Target in modo da poter provare gli esempi da solo
* Installa il [Estensione Adobe Experience Cloud Visual Editing Helper per il browser](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) per Google Chrome
* Scopri come configurare le attività in Adobe Target. Se hai bisogno di un aggiornamento, le seguenti esercitazioni e guide sono utili per questa lezione:
   * [Utilizzare il Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Utilizzare il Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Creare attività di targeting delle esperienze](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Quando sei pronto, il primo passaggio per una migrazione di successo è: [informazioni sul processo di migrazione](migration-overview.md) e le differenze tra at.js e Platform Web SDK.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).