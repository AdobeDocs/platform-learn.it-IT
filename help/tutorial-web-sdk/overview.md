---
title: Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK
description: Scopri come implementare applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 11%

---

# Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK

>[!CAUTION]
>
>Prevediamo di pubblicare modifiche principali a questo tutorial venerdì 15 marzo 2024. Dopo questo punto molti esercizi cambieranno e potrebbe essere necessario riavviare l&#39;esercitazione dall&#39;inizio per completare tutte le lezioni.


Scopri come implementare applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.

Experienci Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire sia con le applicazioni Adobe che con i servizi di terze parti tramite la rete Edge di Adobe Experience Platform. Consulta [Panoramica di Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it) per informazioni più dettagliate.

Questa esercitazione ti guida attraverso l’implementazione di Platform Web SDK su un sito web di esempio per la vendita al dettaglio denominato Luma. Il [Sito Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispone di un livello dati e funzionalità avanzati che consentono di realizzare un’implementazione realistica. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le soluzioni di marketing tramite Platform Web SDK sul tuo sito Web.

[![Sito web Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## Obiettivi di apprendimento

Dopo aver completato l’esercitazione, sarai in grado di:

* Configurare i flussi di dati

* Creare schemi XDM

* Aggiungi le seguenti applicazioni Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (e applicazioni basate su Platform come Adobe Real-time Customer Data Platform, Adobe Journey Optimizer e Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* Creazione di regole di tag ed elementi dati di oggetti XDM per inviare dati ad applicazioni Adobe

* Convalidare l’implementazione utilizzando l’Adobe Experience Platform Debugger

* Acquisire il consenso degli utenti

* Inoltrare dati a terze parti con l’inoltro di eventi

>[!NOTE]
>
>Un tutorial simile per più soluzioni è disponibile per [SDK per dispositivi mobili](../tutorial-mobile-sdk/overview.md).

## Prerequisiti

Tutti i clienti Experience Cloud possono utilizzare Platform Web SDK. Non è necessario concedere in licenza a un’applicazione basata su Platform come Real-time Customer Data Platform o Journey Optimizer l’utilizzo di Web SDK.

In queste lezioni, si presume che tu abbia un account di Adobe e il [autorizzazioni richieste](configure-permissions.md) per completare le lezioni. In caso contrario, contatta l’amministratore di Experience Cloud per richiedere l’accesso.

Inoltre, si presume che tu abbia familiarità con linguaggi di sviluppo front-end come HTML e JavaScript. Non devi essere un esperto in questi linguaggi, ma ottieni di più da questa esercitazione se sei in grado di leggere e comprendere il codice.

Cominciamo.

[Successivo: ](configure-permissions.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
