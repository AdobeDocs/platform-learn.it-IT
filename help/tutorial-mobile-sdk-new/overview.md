---
title: Panoramica tutorial sull’implementazione di Adobe Experience Cloud nelle app per dispositivi mobili
description: Scopri come implementare le app mobili Adobe Experience Cloud. Questa esercitazione ti guida attraverso un’implementazione di applicazioni Experience Cloud in un’app Swift di esempio.
recommendations: noDisplay,catalog
hide: true
exl-id: 378bdf5d-c3ce-4a4c-b188-ab9e8265627f
source-git-commit: 8810829ec80b38afafbd4384005f5e145c5b5999
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 6%

---

# Tutorial sull’implementazione di Adobe Experience Cloud nelle app per dispositivi mobili

Scopri come implementare le applicazioni Adobe Experience Cloud nella tua app mobile utilizzando Adobe Experience Platform Mobile SDK.

Experienci Platform Mobile SDK è un SDK lato client che consente ai clienti di Adobe Experience Cloud di interagire sia con le applicazioni Adobe che con i servizi di terze parti tramite la rete Edge di Adobe Experience Platform. Consulta la [Documentazione di Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) per informazioni più dettagliate.

![Architettura](assets/architecture.png)


Questa esercitazione ti guida attraverso l’implementazione dell’SDK di Platform Mobile in un’app di esempio per la vendita al dettaglio denominata Luma. Il [App Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) dispone di funzionalità che consentono di realizzare un’implementazione realistica. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le soluzioni di marketing tramite l’SDK di Experienci Platform Mobile nelle tue app mobili.

Le lezioni sono progettate per iOS e scritte in Swift/SwiftUI, ma molti dei concetti si applicano anche ad Android™.

Dopo aver completato questa esercitazione, sarai in grado di:

* Crea uno schema utilizzando gruppi di campi standard e personalizzati.
* Configurare un flusso di dati.
* Configura una proprietà tag mobile.
* Imposta un set di dati di Experience Platform (facoltativo).
* Installa e implementa le estensioni tag in un’app.
* Trasmettere correttamente i parametri di Experience Cloud a una [webview](web-views.md).
* Convalidare l’implementazione utilizzando [Adobe Experience Platform Assurance](assurance.md).
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
>Un tutorial simile per più soluzioni è disponibile per [SDK per web](../tutorial-web-sdk/overview.md).

## Prerequisiti

In queste lezioni, si presume che tu abbia un ID Adobe e le autorizzazioni a livello di utente necessarie per completare gli esercizi. In caso contrario, contatta l’amministratore di Adobe per richiedere l’accesso.

* In Raccolta dati, è necessario disporre di:
   * **[!UICONTROL Piattaforme]**- elemento autorizzazione **[!UICONTROL Dispositivi mobili]**
   * **[!UICONTROL Diritti di proprietà]**- elementi di autorizzazione per **[!UICONTROL Sviluppa]**, **[!UICONTROL Approva]**, **[!UICONTROL Pubblica]**, **[!UICONTROL Gestire le estensioni]**, e **[!UICONTROL Gestisci ambienti]**.
   * **[!UICONTROL Diritti aziendali]**- elementi di autorizzazione per **[!UICONTROL Gestisci proprietà]** e, se completi la lezione opzionale di messaggistica push, **[!UICONTROL Gestione configurazioni app]**

     Per ulteriori informazioni sulle autorizzazioni per i tag, consulta [Autorizzazioni utente per i tag](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=it){target="_blank"} nella documentazione del prodotto.
* Ad Experience Platform, devi disporre di:
   * **[!UICONTROL Modellazione dati]**- autorizzazioni per gestire e visualizzare gli schemi.
   * **[!UICONTROL Identity Management]**: elementi di autorizzazione per gestire e visualizzare gli spazi dei nomi delle identità.
   * **[!UICONTROL Raccolta dati]**: elementi di autorizzazione per gestire e visualizzare gli stream di dati.

   * Se sei cliente di un’applicazione basata su Platform come Real-Time CDP, Journey Optimizer o Customer Journey Analytics e desideri seguire le relative lezioni, dovresti anche:
      * **[!UICONTROL Gestione dati]**: elementi di autorizzazione per gestire e visualizzare i set di dati.
      * Uno sviluppo **sandbox** che puoi utilizzare per questa esercitazione.

   * Per le lezioni di Journey Optimizer, è necessario disporre delle autorizzazioni per configurare **servizio di notifica push** e per creare un’ **superficie dell&#39;app**, a **percorso**, a **messaggio**, e **predefiniti per messaggi**. Per la gestione delle decisioni, è necessario disporre delle autorizzazioni appropriate per **gestire le offerte** e **decisioni** come descritto [qui](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

* Per Adobe Analytics, è necessario sapere quale **suite di rapporti** puoi utilizzare per completare questa esercitazione.

* Per Adobe Target, devi disporre dell&#39;autorizzazione per creare e attivare attività.


>[!NOTE]
>
>Come parte di questa esercitazione, puoi creare schemi, set di dati, identità e così via. Se più persone stanno seguendo questa esercitazione in una singola sandbox, puoi aggiungere o anteporre un’identificazione come parte delle convenzioni di denominazione durante la creazione di questi oggetti. Ad esempio, aggiungi ` - <your name or initials>` al nome dell&#39;oggetto che si desidera creare.

>[!NOTE]
>
>Utilizzi iOS come piattaforma, [!DNL Swift] come linguaggio di programmazione, [!DNL SwiftUI] come framework dell’interfaccia utente [!DNL Xcode] come ambiente di sviluppo integrato (IDE). Tuttavia, molti dei concetti di implementazione illustrati sono simili per altre piattaforme di sviluppo. Molti hanno già completato correttamente questa esercitazione con poca o nessuna esperienza precedente di iOS/Swift(UI). Non devi essere un esperto per completare le lezioni, ma puoi ottenere di più dalle lezioni se sei in grado di leggere e comprendere il codice senza difficoltà.


## Scaricare l’app Luma

Sono disponibili per il download due versioni dell’app di esempio. Entrambe le versioni possono essere scaricate/clonate da [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Sono disponibili due cartelle:


1. [Inizio](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: progetto senza codice o con codice segnaposto per la maggior parte del codice SDK di Mobile di Experience Platform da utilizzare per completare gli esercizi pratici in questa esercitazione.
1. [Fine](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: una versione con l’implementazione completa come riferimento.

Se desideri semplicemente provare l’app finale, puoi anche scaricarla direttamente dall’App Store di Apple.

[<img src="assets/download-app.svg">](https://apps.apple.com/us/app/luma-app/id6466588487)

Cominciamo.

>[!SUCCESS]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Creare uno schema XDM](create-schema.md)**
