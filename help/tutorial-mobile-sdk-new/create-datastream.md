---
title: Configurare uno stream di dati
description: Scopri come creare uno stream di dati in Experience Platform.
feature: Mobile SDK,Datastreams
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# Creare un flusso di dati

Scopri come creare uno stream di dati in Experience Platform.

Un flusso di dati è una configurazione lato server in Platform Edge Network. Lo stream di dati garantisce che i dati in arrivo nella rete Edge di Platform vengano instradati in modo appropriato alle applicazioni e ai servizi Adobe Experience Cloud. Per ulteriori informazioni, vedere [documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it) o questo [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=it).

## Prerequisiti

Per creare un flusso di dati, è necessario eseguire il provisioning della tua organizzazione per questa funzione nell’interfaccia di Data Collection (precedentemente [!UICONTROL Launch]) e devi disporre delle autorizzazioni utente per [!UICONTROL Experience Platform] > [!UICONTROL Raccolta dati] > **[!UICONTROL Gestire gli stream di dati]** e **[!UICONTROL Visualizzare gli stream di dati]**.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Sapere quando utilizzare un flusso di dati.
* Creare un flusso di dati.
* Configurare un flusso di dati.

## Creare un flusso di dati

Gli stream di dati possono essere creati in [!UICONTROL Raccolta dati] tramite l&#39;interfaccia [!UICONTROL Datastream] di configurazione. Per creare uno stream di dati:

1. Assicurati di trovarti nella sandbox di Experience Platform corretta, in quanto gli stream di dati sono definiti a livello di sandbox.
1. Seleziona **[!UICONTROL Flussi di dati]** nella barra a sinistra.
1. Seleziona **[!UICONTROL Nuovo flusso di dati]**.

   ![home stream di dati](assets/datastream-new.png)

1. Fornisci un **[!UICONTROL Nome]**, ad esempio `Luma Mobile App` e un **[!UICONTROL Descrizione]**, ad esempio `Datastream for Luma Mobile App`.
1. Seleziona lo schema creato nella lezione precedente da **Schema Evento** un elenco.
1. Seleziona **[!UICONTROL Salva]**.

   ![nuovi flussi di dati](assets/datastream-name.png)


## Aggiungi servizi

Quindi, connetti i servizi Experience Cloud allo stream di dati. Quando Platform Mobile SDK invia i dati a Edge Network, lo stream di dati li invia a questi servizi:

1. Seleziona **[!UICONTROL Aggiungi servizio]**.

1. Aggiungi **[!UICONTROL Adobe Analytics]** dal [!UICONTROL Servizio] elenco,

1. Immettere il nome del sito del report che si desidera utilizzare in **[!UICONTROL ID suite di rapporti]**.

1. Attiva il servizio cambiando **[!UICONTROL Abilitato]** su.

1. Seleziona **[!UICONTROL Salva]**.

   ![Aggiungere Adobe Analytics come servizio Datastream](assets/datastream-service-aa.png)

È inoltre possibile abilitare il servizio Adobe Experience Platform.

>[!IMPORTANT]
>
>Puoi abilitare il servizio Adobe Experience Platform solo dopo aver creato un set di dati evento. Se non hai già creato un set di dati evento, segui le istruzioni [qui](platform.md).

1. Clic ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi servizio]** per aggiungere un altro servizio.

1. Seleziona **[!UICONTROL Adobe Experience Platform]** dal [!UICONTROL Servizio] elenco.

1. Attiva il servizio cambiando **[!UICONTROL Abilitato]** su.

1. Seleziona la **[!UICONTROL Set di dati evento]** che hai creato come parte del [Creare un set di dati](platform.md#create-a-dataset) istruzioni, ad esempio **Set di dati evento app mobile Luma**

1. Seleziona **[!UICONTROL Salva]**.

   ![Aggiungere Adobe Experience Platform come servizio Datastream](assets/datastream-service-aep.png)
1. La configurazione finale sarà simile alla seguente.

   ![impostazioni dello stream di dati](assets/datastream-settings.png)


>[!NOTE]
>
>L’abilitazione di ciascuno dei servizi utilizzati dalla tua organizzazione garantisce che i dati raccolti nell’app mobile possano essere utilizzati ovunque. Per ulteriori informazioni sulle impostazioni dello stream di dati, consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Quando implementi l’SDK di Platform Mobile nella tua app, devi creare tre flussi di dati da mappare ai tre ambienti di tag (sviluppo, stage e produzione). Se utilizzi l’SDK di Platform Mobile con applicazioni basate su Platform, ad esempio Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, assicurati di creare tali flussi di dati nelle sandbox di Platform appropriate.

>[!SUCCESS]
>
>Ora disponi di un flusso di dati da utilizzare per il resto dell’esercitazione.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Configurare i tag](configure-tags.md)**
