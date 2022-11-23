---
title: Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK
description: Scopri come implementare le applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 6488faee86a53585bdbf03e069c4d6cf7e81d096
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 26%

---

# Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK

Scopri come implementare le applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.

Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire sia con le applicazioni di Adobe che con i servizi di terze parti tramite Adobe Experience Platform Edge Network. Vedi [Panoramica dell’SDK per web Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it) per informazioni più dettagliate.

Questa esercitazione guida l’utente nell’implementazione di Platform Web SDK in un sito web retail di esempio denominato Luma. Il sito [](https://luma.enablementadobe.com/content/luma/us/en.html)Luma dispone di un livello dati e funzionalità avanzati che consentono di realizzare un’implementazione realistica. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le soluzioni di marketing tramite Platform Web SDK sul tuo sito web.

[![Sito web Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## Finalità di apprendimento

Dopo aver completato l’esercitazione, sarai in grado di:

* Configurare i flussi di dati

* Creare schemi XDM

* Aggiungi le seguenti applicazioni Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (e applicazioni basate su Platform come Adobe Real-time Customer Data Platform, Adobe Journey Optimizer e Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* Creare regole di tag ed elementi dati oggetto XDM per inviare dati alle applicazioni Adobe

* Convalidare l’implementazione utilizzando Adobe Experience Platform Debugger

* Acquisire il consenso degli utenti

* Inoltrare dati a terze parti con inoltro eventi

>[!NOTE]
>
>È disponibile un tutorial simile per più soluzioni per [SDK per dispositivi mobili](../tutorial-mobile-sdk/overview.md).

## Prerequisiti

Tutti i clienti di Experience Cloud possono utilizzare Platform Web SDK. Non è necessario concedere in licenza a un&#39;applicazione basata su Platform come Real-time Customer Data Platform o Journey Optimizer per utilizzare l&#39;SDK web.

In queste lezioni, si presume che tu abbia un account Adobe e il [autorizzazioni necessarie](configure-permissions.md) per completare le lezioni. In caso contrario, è necessario contattare l’amministratore di Experience Cloud per richiedere l’accesso.

Inoltre, si presume che tu abbia familiarità con linguaggi di sviluppo front-end come HTML e JavaScript. Non devi essere un esperto in queste lingue, ma puoi imparare di più da questa esercitazione se sei in grado di leggere e comprendere il codice.

Cominciamo.

[Avanti: ](configure-permissions.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nel conoscere Adobe Experience Platform Web SDK. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
