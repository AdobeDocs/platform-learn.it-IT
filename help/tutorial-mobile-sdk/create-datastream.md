---
title: Configurare uno stream di dati
description: Scopri come creare uno stream di dati in Experience Platform.
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 6%

---

# Creare un flusso di dati

Scopri come creare uno stream di dati in Experience Platform.

Un flusso di dati è una configurazione lato server in Platform Edge Network.  Lo stream di dati garantisce che i dati in arrivo nella rete Edge di Platform vengano instradati in modo appropriato alle applicazioni e ai servizi Adobe Experience Cloud. Per ulteriori informazioni, vedere [documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it) o questo [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=it).

## Prerequisiti

Per creare un flusso di dati, è necessario eseguire il provisioning della tua organizzazione per questa funzione nell’interfaccia di Data Collection (precedentemente [!UICONTROL Launch]) e devi disporre delle autorizzazioni utente per [!UICONTROL Experience Platform] > [!UICONTROL Raccolta dati] > **[!UICONTROL Gestire gli stream di dati]** e **[!UICONTROL Visualizzare gli stream di dati]**.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Sapere quando utilizzare un flusso di dati.
* Creare un flusso di dati.
* Configurare un flusso di dati.

## Creare un flusso di dati

Gli stream di dati possono essere creati in [!UICONTROL Raccolta dati] tramite l&#39;interfaccia [!UICONTROL Datastream] di configurazione. Per creare uno stream di dati:

1. Assicurati di trovarti nella sandbox Platform corretta.
1. Seleziona **[!UICONTROL Nuovo flusso di dati]**.

   ![home stream di dati](assets/mobile-datastream-new.png)

1. Specifica un nome, ad esempio `Luma App`.
1. Seleziona lo schema creato nella lezione precedente.
1. Seleziona **[!UICONTROL Salva]**.

   ![nuovi flussi di dati](assets/mobile-datastream-name.png)


## Aggiungi servizi

Ora puoi collegare i servizi Experience Cloud allo stream di dati. Quando Platform Mobile SDK invia i dati a Edge Network, lo stream di dati li invia a questi servizi:

1. Aggiungi **[!UICONTROL Adobe Analytics]** e fornisci una suite di rapporti.

1. Abilita **[!UICONTROL Adobe Audience Manager]** (facoltativo).

1. Abilita **[!UICONTROL Adobe Experience Platform]** e fornire un **[!UICONTROL set di dati]** (facoltativo).
   * Se non hai già creato un set di dati, segui le istruzioni [qui](platform.md).

1. La configurazione finale sarà simile alla seguente.
   ![impostazioni dello stream di dati](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>L’abilitazione di ciascuno dei servizi utilizzati dalla tua organizzazione garantisce che i dati raccolti nell’app mobile possano essere utilizzati ovunque. Ulteriori informazioni sulle impostazioni dello stream di dati consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Quando implementi l’SDK di Platform Mobile sul tuo sito web, devi creare tre flussi di dati da mappare ai tre ambienti di tag (sviluppo, stage e produzione). Se utilizzi l’SDK di Platform Mobile con applicazioni basate su Platform, ad esempio Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, assicurati di creare tali flussi di dati nelle sandbox di Platform appropriate.

Successivo: **[Configurare i tag](configure-tags.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
