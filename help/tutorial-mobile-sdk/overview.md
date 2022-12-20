---
title: Panoramica dell’esercitazione sull’implementazione di Adobe Experience Cloud nelle app per dispositivi mobili
description: Scopri come implementare le applicazioni mobili Adobe Experience Cloud. Questa esercitazione ti guida attraverso un’implementazione di applicazioni Experience Cloud in un’app Swift di esempio.
recommendation: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 10%

---

# Tutorial sull’implementazione di Adobe Experience Cloud nelle app per dispositivi mobili

Scopri come implementare le applicazioni Adobe Experience Cloud nella tua app mobile utilizzando Adobe Experience Platform Mobile SDK.

Experience Platform Mobile SDK è un SDK lato client che consente ai clienti di Adobe Experience Cloud di interagire sia con le applicazioni di Adobe che con i servizi di terze parti tramite Adobe Experience Platform Edge Network. Consulta la sezione [Documentazione di Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/) per informazioni più dettagliate.

![impostazioni di compilazione](assets/data-collection-mobile-sdk.png)


Questa esercitazione ti guida attraverso l’implementazione dell’SDK di Platform Mobile in un’app retail di esempio denominata Luma. La [App Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) dispone di funzionalità che ti consentono di creare un’implementazione realistica. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le soluzioni di marketing tramite l’SDK di Platform Mobile nelle tue app mobili.

Le lezioni sono progettate per iOS e scritte in Swift, ma molti dei concetti sono validi anche per Android™.

Dopo aver completato questa esercitazione, sarai in grado di:

* Creare uno schema utilizzando gruppi di campi standard e personalizzati.
* Imposta un datastream.
* Configura una proprietà tag mobile.
* Imposta un set di dati di Experience Platform (facoltativo).
* Installa e implementa estensioni di tag in un’app.
* Aggiungi le seguenti applicazioni/estensioni Adobe Experience Cloud:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Raccolta dati del ciclo di vita](lifecycle-data.md)
   * [Adobe Analytics tramite XDM](analytics.md)
   * [Consenso](consent.md)
   * [Identità](identity.md)
   * [Profilo](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [Messaggi push con Journey Optimizer](journey-optimizer-push.md)
* Trasmettere correttamente i parametri di Experience Cloud a un [webview](web-views.md).
* Convalida l’implementazione utilizzando [Adobe Experience Platform Assurance](assurance.md).

>[!NOTE]
>
>È disponibile un tutorial simile per più soluzioni per [SDK per web](../tutorial-web-sdk/overview.md).

## Prerequisiti

In queste lezioni, si presume che tu sia in possesso di un Adobe ID e delle autorizzazioni necessarie per completare gli esercizi. In caso contrario, contatta l’amministratore di Adobe per richiedere l’accesso.

* Nella raccolta dati devi disporre di:
   * **[!UICONTROL Piattaforme]**—voce di autorizzazione **[!UICONTROL Mobile]**
   * **[!UICONTROL Diritti di proprietà]**—voci di autorizzazione a **[!UICONTROL Sviluppa]**, **[!UICONTROL Approva]**, **[!UICONTROL Pubblica]**, **[!UICONTROL Gestire le estensioni]** e **[!UICONTROL Gestire gli ambienti]**.
   * **[!UICONTROL Diritti aziendali]**—voci di autorizzazione a **[!UICONTROL Gestisci proprietà]** e, se completi la lezione opzionale sui messaggi push, **[!UICONTROL Gestire le configurazioni dell’app]**

      Per ulteriori informazioni sulle autorizzazioni dei tag, consulta [Autorizzazioni utente per i tag](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=it){target=&quot;_blank&quot;} nella documentazione del prodotto.
* Ad Experience Platform, devi disporre di:
   * **[!UICONTROL Modellazione dati]**- elementi di autorizzazione per gestire e visualizzare gli schemi.
   * **[!UICONTROL Identity Management]**: elementi di autorizzazione per gestire e visualizzare i namespace di identità.
   * **[!UICONTROL Raccolta dati]**- elementi di autorizzazione per gestire e visualizzare i datastreams.

   * Se sei cliente di un’applicazione basata su Platform come Real-Time CDP, Journey Optimizer o Customer Journey Analytics, devi anche disporre di:
      * **[!UICONTROL Gestione dati]**: elementi di autorizzazione per gestire e visualizzare i set di dati per completare _esercitazioni opzionali della piattaforma_ (richiede una licenza per un&#39;applicazione basata su Platform ).
      * Uno sviluppo **sandbox** che puoi utilizzare per questa esercitazione.
* Per Adobe Analytics, devi sapere quale **suite di rapporti** puoi utilizzare per completare questa esercitazione.

Tutti i clienti di Experience Cloud devono avere accesso alle funzioni necessarie per implementare l’SDK di Mobile.

Inoltre, si presume che tu abbia familiarità con [!DNL Swift]. Non devi essere un esperto per completare le lezioni, ma ti saranno più utili se sei in grado di leggere e comprendere il codice senza difficoltà.

## Scaricare l’app Luma

Sono disponibili due versioni dell’app di esempio per il download.

1. [Vuoto](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} - versione senza codice Experience Cloud per completare gli esercizi pratici in questa esercitazione
1. [Completamente implementato](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} - versione con implementazione Experience Cloud completa per riferimento.

Cominciamo.


Avanti: **[Creare uno schema XDM](create-schema.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)