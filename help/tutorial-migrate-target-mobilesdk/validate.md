---
title: Convalidare e risolvere i problemi relativi all’implementazione di Offer Decisioning e Target
description: Scopri come convalidare e risolvere i problemi di un’implementazione Adobe Target per dispositivi mobili utilizzando l’estensione Offer Decisioning e Target.
exl-id: edc6e25a-58d7-4145-97c3-bf48e980914f
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Convalidare e risolvere i problemi relativi all’implementazione di Offer Decisioning e Target

Dopo aver migrato l’implementazione di Target dall’estensione Target all’estensione Offer Decisioning e Target, è importante verificare che tutto funzioni correttamente prima di pubblicare eventuali modifiche all’app di produzione. Adobe consiglia quanto segue, descritto in dettaglio in questa pagina:

* Esegui una convalida tecnica per verificare che l’implementazione di base e le richieste e risposte di Platform Mobile SDK siano corrette
* Assicurati che le attività Target siano consegnate e renderizzate correttamente
* Verifica che la generazione rapporti funzioni correttamente
* Rivedi tipi di pubblico e script di profilo per assicurarti che siano compatibili con Platform Mobile SDK e l’estensione Optimie
* Garantire il corretto funzionamento delle integrazioni con le applicazioni Adobe o di terze parti

Ogni implementazione di Target è diversa a seconda dell’architettura del sito e delle funzioni utilizzate. Puoi utilizzare le tabelle seguenti come punto di partenza e aggiungere qualsiasi elemento univoco alla tua implementazione.

## Convalida tecnica e risoluzione dei problemi

La convalida tecnica e la risoluzione dei problemi con Platform Mobile SDK e l’estensione Offer Decisioning e Target sono notevolmente migliorate con Assurance. Per informazioni su questo strumento essenziale, consulta le pagine seguenti della documentazione:

* [Configurazione dei plug-in Decisioning in Assurance](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/assurance-setup/){target=_blank}

* [Convalida dell&#39;installazione di SDK per l&#39;ottimizzazione](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/optimize-configuration-view/){target=_blank}

* [Rivedi le richieste e simula diverse esperienze](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/review-simulate/){target=_blank}

Dopo aver eseguito i passaggi di convalida descritti qui sopra, puoi essere certo che l’implementazione di Platform Mobile SDK con l’estensione Offer Decisioning e Target sia pronta per il passaggio alla produzione.

Congratulazioni, hai raggiunto la fine dell&#39;esercitazione. Buona fortuna per la migrazione della tua implementazione di Adobe Target all’estensione Offer Decisioning e Target.

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target per dispositivi mobili dall’estensione Target all’estensione Offer Decisioning e Target. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=it#M463).
