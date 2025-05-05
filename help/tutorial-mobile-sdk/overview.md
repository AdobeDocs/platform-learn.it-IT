---
title: Panoramica tutorial sull’implementazione di Adobe Experience Cloud nelle app per dispositivi mobili
description: Scopri come implementare le app mobili Adobe Experience Cloud. Questa esercitazione ti guida attraverso un’implementazione delle applicazioni Experience Cloud in un’app Swift di esempio.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: c08671ae28955ff090baa7aa5a47246b2196ba20
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 4%

---

# Tutorial sull’implementazione di Adobe Experience Cloud nelle app per dispositivi mobili

Scopri come implementare le applicazioni Adobe Experience Cloud nella tua app mobile utilizzando Adobe Experience Platform Mobile SDK.

Experience Platform Mobile SDK è un SDK lato client che consente ai clienti di Adobe Experience Cloud di interagire sia con le applicazioni Adobe che con i servizi di terze parti tramite Adobe Experience Platform Edge Network. Per informazioni più dettagliate, consulta la [documentazione di Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/).

![Architettura](assets/architecture.png)


Questa esercitazione ti guida attraverso l’implementazione di Platform Mobile SDK in un’app di esempio per la vendita al dettaglio chiamata Luma. L&#39;app [Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) dispone di funzionalità che consentono di creare un&#39;implementazione realistica. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le soluzioni di marketing tramite Experience Platform Mobile SDK nelle tue app mobili.

Le lezioni sono progettate per iOS e scritte in Swift/SwiftUI, ma molti dei concetti si applicano anche ad Android™.

Dopo aver completato questa esercitazione, sarai in grado di:

* Crea uno schema utilizzando gruppi di campi standard e personalizzati.
* Imposta un flusso di dati.
* Configura una proprietà tag mobile.
* Configurare un set di dati di Experience Platform (facoltativo).
* Installa e implementa le estensioni tag in un’app.
* Trasmettere correttamente i parametri Experience Cloud a una [visualizzazione Web](web-views.md).
* Convalida l&#39;implementazione tramite [Adobe Experience Platform Assurance](assurance.md).
* Aggiungi le seguenti applicazioni/estensioni Adobe Experience Cloud:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Raccolta dati del ciclo di vita](lifecycle-data.md)
   * [Consenso](consent.md)
   * [Identità](identity.md)
   * [Profilo](profile.md)
   * [Places](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [Messaggistica push con Journey Optimizer](journey-optimizer-push.md)
   * [Messaggistica in-app con Journey Optimizer](journey-optimizer-inapp.md)
   * [Gestione delle decisioni con Journey Optimizer](journey-optimizer-offers.md)
   * [Target](target.md)


>[!NOTE]
>
>Un tutorial simile per più soluzioni è disponibile per [Web SDK](../tutorial-web-sdk/overview.md).

## Autorizzazioni

In queste lezioni, si presume che tu sia in possesso di un Adobe Id e delle autorizzazioni a livello di utente necessarie per completare gli esercizi. In caso contrario, contatta il tuo amministratore Adobe per richiedere l’accesso.

* In Raccolta dati, è necessario disporre di:
   * **[!UICONTROL Piattaforme]**—elemento di autorizzazione **[!UICONTROL Dispositivi mobili]**
   * **[!UICONTROL Diritti proprietà]**—elementi di autorizzazione per **[!UICONTROL Sviluppa]**, **[!UICONTROL Approva]**, **[!UICONTROL Pubblica]**, **[!UICONTROL Gestisci estensioni]** e **[!UICONTROL Gestisci ambienti]**.
   * **[!UICONTROL Diritti azienda]**—autorizzazioni per **[!UICONTROL Gestione proprietà]**

     Per ulteriori informazioni sulle autorizzazioni dei tag, vedere [Autorizzazioni utente per i tag](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=it){target="_blank"} nella documentazione del prodotto.
* In Experience Platform, devi disporre di:
   * **[!UICONTROL Modellazione dati]**: elementi di autorizzazione per gestire e visualizzare gli schemi.
   * **[!UICONTROL Identity Management]**: elementi di autorizzazione per gestire e visualizzare gli spazi dei nomi delle identità.
   * **[!UICONTROL Raccolta dati]**: elementi di autorizzazione per gestire e visualizzare gli stream di dati.

   * Se sei cliente di un’applicazione basata su Platform come Real-Time CDP, Journey Optimizer o Customer Journey Analytics e desideri seguire le relative lezioni, dovresti anche:
      * **[!UICONTROL Gestione dati]**: elementi di autorizzazione per gestire e visualizzare i set di dati.
      * Una **sandbox** di sviluppo che puoi utilizzare per questa esercitazione.

   * Per le lezioni di Journey Optimizer, è necessario disporre delle autorizzazioni per configurare il **servizio di notifica push** e per creare una **superficie app**, un **percorso**, un **messaggio** e **predefiniti messaggio**. Per la gestione delle decisioni, è necessario disporre delle autorizzazioni appropriate per **gestire le offerte** e **le decisioni** come descritto [qui](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=it#decisions-permissions).

* Con Adobe Analytics, devi sapere quali **suite di rapporti** puoi utilizzare per completare questa esercitazione.

* Per Adobe Target, devi disporre dell&#39;autorizzazione per creare e attivare attività.


>[!NOTE]
>
>Come parte di questa esercitazione, puoi creare schemi, set di dati, identità e così via. Se più persone stanno seguendo questa esercitazione in una singola sandbox, puoi aggiungere o anteporre un’identificazione come parte delle convenzioni di denominazione durante la creazione di questi oggetti. Aggiungere ad esempio ` - <your name or initials>` al nome dell&#39;oggetto che si desidera creare.

## Cronologia versioni

* 29 novembre 2023: revisione importante con una nuova app di esempio e nuove lezioni per la messaggistica in-app, la gestione delle decisioni e Adobe Target.
* 9 marzo 2022: prima pubblicazione

## Scaricare l’app Luma

Sono disponibili per il download due versioni dell’app di esempio. Entrambe le versioni possono essere scaricate o clonate da [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Sono disponibili due cartelle:


1. [Inizio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: un progetto senza codice o con codice segnaposto per la maggior parte del codice SDK di Experience Platform Mobile che è necessario utilizzare per completare gli esercizi pratici in questa esercitazione.
1. [Fine](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: una versione con l&#39;implementazione completa come riferimento.

>[!NOTE]
>
>Si utilizza iOS come piattaforma, [!DNL Swift] come linguaggio di programmazione, [!DNL SwiftUI] come framework dell&#39;interfaccia utente e [!DNL Xcode] come ambiente di sviluppo integrato (IDE). Tuttavia, molti dei concetti di implementazione illustrati sono simili per altre piattaforme di sviluppo. Molti hanno già completato correttamente questa esercitazione con poca o nessuna esperienza precedente di iOS/Swift(UI). Non devi essere un esperto per completare le lezioni, ma puoi ottenere di più dalle lezioni se sei in grado di leggere e comprendere il codice senza difficoltà.


Puoi scaricare la versione finale prodotta dell’app da App Store.

[![Scarica](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)


Cominciamo.

>[!SUCCESS]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Creare uno schema XDM](create-schema.md)**
