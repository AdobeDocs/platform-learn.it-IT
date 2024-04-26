---
title: Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK
description: Scopri come implementare applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 4%

---

# Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK

Scopri come implementare applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.

Experienci Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire sia con le applicazioni Adobe che con i servizi di terze parti tramite l’Edge Network Adobe Experience Platform. Consulta [Panoramica di Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge/home) per informazioni più dettagliate.

![Architettura Experienci Platform Web SDK](assets/dc-websdk.png)

Questa esercitazione ti guida attraverso l’implementazione di Platform Web SDK su un sito web di esempio per la vendita al dettaglio denominato Luma. Il [Sito Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispone di un livello dati e funzionalità avanzati che consentono di realizzare un’implementazione realistica. Per questo tutorial:

* Crea una tua proprietà di tag, nel tuo account, con un’implementazione Platform Web SDK per il sito web Luma.
* Configura tutte le funzioni di raccolta dati per le implementazioni Web SDK, come stream di dati, schemi e spazi dei nomi di identità.
* Aggiungi le seguenti applicazioni Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (e applicazioni basate su Platform come Adobe Real-time Customer Data Platform, Adobe Journey Optimizer e Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implementa l’inoltro degli eventi per inviare i dati raccolti da Web SDK a destinazioni non Adobi.
* Convalida la tua implementazione di Platform Web SDK utilizzando Experienci Platform Debugger e Assurance.

Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le applicazioni di marketing tramite Platform Web SDK sul tuo sito Web.


>[!NOTE]
>
>Un tutorial simile per più soluzioni è disponibile per [SDK per dispositivi mobili](../tutorial-mobile-sdk/overview.md).

## Prerequisiti

Tutti i clienti Experience Cloud possono utilizzare Platform Web SDK. Non è necessario concedere in licenza a un’applicazione basata su Platform come Real-time Customer Data Platform o Journey Optimizer l’utilizzo di Web SDK.

In queste lezioni, si presume che tu abbia un account di Adobe e le autorizzazioni necessarie per completare le lezioni. In caso contrario, devi contattare un amministratore Experience Cloud della tua azienda per ottenere l’accesso.

* Per **Raccolta dati**, è necessario disporre di:
   * **[!UICONTROL Piattaforme]**—autorizzazione per **[!UICONTROL Web]** e, se autorizzato, **[!UICONTROL Bordo]**
   * **[!UICONTROL Diritti di proprietà]**—autorizzazione a **[!UICONTROL Approva]**, **[!UICONTROL Sviluppa]**, **[!UICONTROL Modifica proprietà]**, **[!UICONTROL Gestisci ambienti]**, **[!UICONTROL Gestire le estensioni]**, e **[!UICONTROL Pubblica]**,
   * **[!UICONTROL Diritti aziendali]**—autorizzazione a **[!UICONTROL Gestisci proprietà]**

     Per ulteriori informazioni sulle autorizzazioni tag, consulta [la documentazione](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions).

* Per **Experience Platform**, è necessario disporre di:

   * Accesso al **produzione predefinita**, **Prod** sandbox.
   * Accesso a **[!UICONTROL Gestire gli schemi]** e **[!UICONTROL Visualizzare gli schemi]** in **[!UICONTROL Modellazione dati]**.
   * Accesso a **[!UICONTROL Gestire gli spazi dei nomi delle identità]** e **[!UICONTROL Visualizzare gli spazi dei nomi delle identità]** in **[!UICONTROL Identity Management]**.
   * Accesso a **[!UICONTROL Gestire gli stream di dati]** e **[!UICONTROL Visualizzare gli stream di dati]** in **[!UICONTROL Raccolta dati]**.
   * Se sei cliente di un’applicazione basata su Platform e completerai il [Experience Platform configurazione](setup-experience-platform.md) lezione, dovresti anche avere:
      * Accesso a **sviluppo** sandbox.
      * Tutti gli elementi di autorizzazione in **[!UICONTROL Gestione dati]**, e **[!UICONTROL Gestione profilo]**:

     Le funzioni richieste devono essere disponibili per tutti i clienti di Experience Cloud, anche se non sei cliente di un’applicazione basata su Platform come Real-Time CDP.

     Per ulteriori informazioni sul controllo degli accessi alla piattaforma, consulta [la documentazione](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home).

* Per l&#39;opzione **Adobe Analytics** lezione, devi avere [accesso come amministratore alle impostazioni della suite di rapporti, alle regole di elaborazione e ad Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-console/home)

* Per l&#39;opzione **Adobe Target** lezione, devi avere [Editor o Approvatore](https://experienceleague.adobe.com/en/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80) accesso.

* Per l&#39;opzione **Audience Manager** lezione, devi avere accesso a creare, leggere e scrivere caratteristiche, segmenti e destinazioni. Per ulteriori informazioni, consulta l’esercitazione su [Controllo degli accessi basato sul ruolo di Audienci Manager](https://experienceleague.adobe.com/en/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).


>[!NOTE]
>
>Si presume che tu abbia familiarità con linguaggi di sviluppo front-end come HTML e JavaScript. Non devi essere un esperto in questi linguaggi, ma ottieni di più da questa esercitazione se sei in grado di leggere e comprendere il codice.

## Aggiornamenti

* 24 aprile 2024: aggiornamenti principali, tra cui l’aggiunta di Imposta variabile/aggiorna variabile, richieste di suddivisione personalizzazione e analisi, lezioni di Journey Optimizer

## Caricare il sito web Luma

Carica [Sito web Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} in una scheda del browser separata e aggiungilo ai segnalibri in modo da poterlo caricare facilmente quando necessario durante l&#39;esercitazione. Non hai bisogno di alcun accesso aggiuntivo a Luma, a parte la possibilità di caricare il nostro sito di produzione ospitato.

[![Sito web Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

Cominciamo.

[Successivo: ](configure-schemas.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
