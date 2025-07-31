---
title: Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK
description: Scopri come implementare le applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 7%

---

# Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK

Scopri come implementare le applicazioni Experience Cloud utilizzando Adobe Experience Platform Web SDK.

Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire sia con le applicazioni Adobe che con i servizi di terze parti tramite Adobe Experience Platform Edge Network. Per ulteriori informazioni, vedere [Panoramica di Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge/home).

![Architettura di Experience Platform Web SDK](assets/dc-websdk.png)

Questa esercitazione ti guida attraverso l’implementazione di Platform Web SDK su un sito web di esempio per la vendita al dettaglio denominato Luma. Il [sito Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispone di un livello dati e funzionalità avanzati che consentono di creare un&#39;implementazione realistica. Per questo tutorial:

* Crea una tua proprietà di tag nel tuo account con un’implementazione di Platform Web SDK per il sito web Luma.
* Configura tutte le funzioni di raccolta dati per le implementazioni di Web SDK, come stream di dati, schemi e spazi dei nomi di identità.
* Aggiungi le seguenti applicazioni Adobe Experience Cloud:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (e applicazioni integrate in Platform come Adobe Real-Time Customer Data Platform, Adobe Journey Optimizer e Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implementa l’inoltro degli eventi per inviare i dati raccolti da Web SDK a destinazioni non Adobe.
* Convalida l’implementazione di Platform Web SDK utilizzando Experience Platform Debugger e Assurance.

Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le applicazioni di marketing tramite Platform Web SDK sul tuo sito Web.


>[!NOTE]
>
>Un tutorial simile per più soluzioni è disponibile per [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Prerequisiti

Tutti i clienti Experience Cloud possono utilizzare Platform Web SDK. Non è necessario concedere in licenza un’applicazione basata su Platform come Real-Time Customer Data Platform o Journey Optimizer per l’utilizzo di Web SDK.

In queste lezioni, si presume che tu abbia un account Adobe e le autorizzazioni necessarie per completare le lezioni. In caso contrario, devi contattare un amministratore Experience Cloud della tua azienda per ottenere l’accesso.

* Per **Raccolta dati**, è necessario disporre di:
   * **[!UICONTROL Piattaforme]**—autorizzazione per **[!UICONTROL Web]** e, se concessi in licenza, **[!UICONTROL Edge]**
   * **[!UICONTROL Diritti proprietà]**—autorizzazione per **[!UICONTROL Approva]**, **[!UICONTROL Sviluppa]**, **[!UICONTROL Modifica proprietà]**, **[!UICONTROL Gestisci ambienti]**, **[!UICONTROL Gestisci estensioni]** e **[!UICONTROL Pubblica]**,
   * **[!UICONTROL Diritti azienda]**—autorizzazione per **[!UICONTROL Gestione proprietà]**

     Per ulteriori informazioni sulle autorizzazioni dei tag, consulta [la documentazione](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions).

* Per **Experience Platform**, è necessario disporre di:

   * Accesso alla sandbox **default production**, **&quot;Prod&quot;**.
   * Accesso a **[!UICONTROL Gestisci schemi]** e **[!UICONTROL Visualizza schemi]** in **[!UICONTROL Modellazione dati]**.
   * Accesso a **[!UICONTROL Gestisci spazi dei nomi identità]** e **[!UICONTROL Visualizza spazi dei nomi identità]** in **[!UICONTROL Identity Management]**.
   * Accesso a **[!UICONTROL Gestisci flussi di dati]** e **[!UICONTROL Visualizza flussi di dati]** in **[!UICONTROL Raccolta dati]**.
   * Se sei un cliente di un&#39;applicazione basata su Platform e completerai la lezione [Configurazione di Experience Platform](setup-experience-platform.md), dovresti anche disporre di:
      * Accesso a una sandbox di **sviluppo**.
      * Tutti gli elementi di autorizzazione in **[!UICONTROL Gestione dati]** e **[!UICONTROL Gestione profili]**:

     Le funzioni richieste devono essere disponibili per tutti i clienti di Experience Cloud, anche se non sei cliente di un’applicazione basata su piattaforma come Real-Time CDP.

     Per ulteriori informazioni sul controllo degli accessi alla piattaforma, consulta [la documentazione](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home).

* Per la lezione facoltativa di **Adobe Analytics**, è necessario disporre dell&#39;accesso di [amministratore alle impostazioni della suite di rapporti, alle regole di elaborazione e ad Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-console/home)

* Per la lezione facoltativa **Adobe Target**, è necessario disporre dell&#39;accesso [Editor o Approvatore](https://experienceleague.adobe.com/en/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80).

* Per la lezione opzionale **Audience Manager**, è necessario disporre dell&#39;accesso per creare, leggere e scrivere caratteristiche, segmenti e destinazioni. Per ulteriori informazioni, fare riferimento al tutorial sul [Controllo dell&#39;accesso basato sul ruolo di Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).


>[!NOTE]
>
>Si presume che tu abbia familiarità con linguaggi di sviluppo front-end come HTML e JavaScript. Non devi essere un esperto in questi linguaggi, ma ottieni di più da questa esercitazione se sei in grado di leggere e comprendere il codice.

## Aggiornamenti

* 24 aprile 2024: aggiornamenti principali, tra cui l’aggiunta di Imposta variabile/aggiorna variabile, richieste di suddivisione personalizzazione e analisi, lezioni di Journey Optimizer

## Caricare il sito web Luma

Carica il [sito Web Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} in una scheda del browser separata e aggiungi un segnalibro per poterlo caricare facilmente quando necessario durante l&#39;esercitazione. Non hai bisogno di alcun accesso aggiuntivo a Luma, a parte la possibilità di caricare il nostro sito di produzione ospitato.

[![Sito Web Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

Cominciamo.

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
