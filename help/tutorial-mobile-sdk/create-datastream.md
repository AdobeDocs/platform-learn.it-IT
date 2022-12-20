---
title: Configurare un datastream
description: Scopri come creare un datastream in Experience Platform.
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 6%

---

# Creare un flusso di dati

Scopri come creare un datastream in Experience Platform.

Un datastream è una configurazione lato server su Platform Edge Network.  Il datastream assicura che i dati in arrivo su Platform Edge Network vengano indirizzati in modo appropriato alle applicazioni e ai servizi Adobe Experience Cloud. Per ulteriori informazioni, consulta la sezione [documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it) o [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=it).

## Prerequisiti

Per creare un datastream, è necessario eseguire il provisioning per questa funzione nell’interfaccia di raccolta dati (in precedenza [!UICONTROL Launch]) e devi disporre delle autorizzazioni utente per [!UICONTROL Experience Platform] > [!UICONTROL Raccolta dati] > **[!UICONTROL Gestire i flussi di dati]** e **[!UICONTROL Visualizza i reami di dati]**.

## Finalità di apprendimento

In questa lezione:

* Sapere quando utilizzare un datastream.
* Creare un flusso di dati.
* Configura un datastream.

## Creare un flusso di dati

I Datastreams possono essere creati nella [!UICONTROL Raccolta dati] l&#39;interfaccia [!UICONTROL Datastream] strumento di configurazione. Per creare un datastream:

1. Assicurati di essere nella sandbox Platform corretta.
1. Seleziona **[!UICONTROL Nuovo Datastream]**.

   ![home di datastreams](assets/mobile-datastream-new.png)

1. Specifica un nome, ad esempio `Luma App`.
1. Seleziona lo schema creato nella lezione precedente.
1. Seleziona **[!UICONTROL Salva]**.

   ![nuovi datastreams](assets/mobile-datastream-name.png)


## Aggiungi servizi

Successivamente è possibile collegare i servizi Experience Cloud al datastream. Quando l’SDK di Platform Mobile invia dati a Edge Network, il datastream invia i dati a questi servizi:

1. Aggiungi **[!UICONTROL Adobe Analytics]** e fornire una suite di rapporti.

1. Abilita **[!UICONTROL Adobe Audience Manager]** (facoltativo).

1. Abilita **[!UICONTROL Adobe Experience Platform]** e forniscono **[!UICONTROL set di dati]** (facoltativo).
   * Se non hai già creato un set di dati, segui le istruzioni [qui](platform.md).

1. La configurazione finale dovrebbe essere simile a questa.
   ![impostazioni di datastream](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>L’abilitazione di ciascuno dei servizi utilizzati dalla tua organizzazione assicura che i dati raccolti nell’app mobile possano essere utilizzati ovunque. Per ulteriori informazioni sulle impostazioni di datastream, consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Quando implementi l’SDK di Platform Mobile sul tuo sito web, devi creare tre datastreams da mappare ai tuoi tre ambienti di tag (sviluppo, stage e produzione). Se utilizzi Platform Mobile SDK con applicazioni basate su Platform come Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, assicurati di creare tali datastreams nelle sandbox Platform appropriate.

Avanti: **[Configurare i tag](configure-tags.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
