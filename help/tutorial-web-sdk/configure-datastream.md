---
title: Configurare uno stream di dati per Platform Web SDK
description: Scopri come abilitare un flusso di dati e configurare le soluzioni Experience Cloud. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Datastreams
jira: KT-15399
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 4%

---

# Configurare uno stream di dati

Scopri come configurare uno stream di dati per Adobe Experience Platform Web SDK.

[Flussi di dati](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) indica a un Edge Network di Adobe Experience Platform dove inviare i dati raccolti da Platform Web SDK. Nella configurazione dei flussi di dati, abilita le applicazioni di Experience Cloud, l’account di Experience Platform e l’inoltro di eventi.

![SDK per web, flussi di dati e diagramma di Edge Network](assets/dc-websdk-datastreams.png)

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Creare un flusso di dati
* Introduzione alle sostituzioni dello stream di dati

## Prerequisiti

Prima di configurare lo stream di dati, è necessario aver già completato le lezioni seguenti:

* [Configurare uno schema](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)

## Creare un flusso di dati

Ora puoi creare un flusso di dati per indicare all’Edge Network di Platform dove inviare i dati raccolti dall’SDK per web.

**Per creare uno stream di dati:**

1. Apri [Interfaccia di Data Collection](https://launch.adobe.com/){target="_blank"}
1. Assicurati di trovarti nella sandbox corretta

   >[!NOTE]
   >
   >Se sei il cliente di un’applicazione basata su Platform come Real-Time CDP o Journey Optimizer, per questa esercitazione ti consigliamo di utilizzare una sandbox di sviluppo. In caso contrario, utilizza **[!UICONTROL Prod]** sandbox.

1. Vai a **[!UICONTROL Flussi di dati]** nel menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Nuovo flusso di dati]**
1. Invio `Luma Web SDK: Development Environment` come **[!UICONTROL Nome]**. Questo nome viene utilizzato successivamente quando configuri l’estensione Web SDK nella proprietà tag.
1. Seleziona **[!UICONTROL Salva]**

   ![Creare lo stream di dati](assets/datastream-create-new-datastream.png)

   >[!NOTE]
   >
   >È necessario selezionare uno schema solo se si utilizza [Preparazione per la raccolta dati](/help/data-collection/edge/data-prep.md) funzionalità.

Nella schermata successiva è possibile aggiungere al flusso di dati servizi quali applicazioni Adobe, ma a questo punto dell’esercitazione non verrà aggiunto alcun servizio. Lo farai più avanti nelle lezioni [Experience Platform configurazione](setup-experience-platform.md), [Configurare Analytics](setup-analytics.md), [Audience Manager configurazione](setup-audience-manager.md), [Imposta Target](setup-target.md), o [Inoltro eventi](setup-event-forwarding.md).

>[!NOTE]
>
>Quando implementi Platform Web SDK sul tuo sito web, devi creare tre flussi di dati da mappare ai tre ambienti di tag (sviluppo, stage e produzione). Se utilizzi Platform Web SDK con applicazioni basate su Platform, ad esempio Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, assicurati di creare tali flussi di dati nelle sandbox di Platform appropriate.

## Sostituire uno stream di dati

[Override dello stream di dati](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides) consente di definire configurazioni aggiuntive per lo stream di dati e quindi di ignorare la configurazione predefinita in determinate condizioni.

La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, puoi definire le sostituzioni dello stream di dati nella configurazione del servizio dello stream di dati. Ad esempio, puoi definire suite di rapporti di Analytics alternative, aree di lavoro di Target o set di dati di Platform da utilizzare come sostituzioni.
1. Quindi, invii le sostituzioni all’Edge Network tramite un’azione Invia evento SDK per web o tramite una configurazione nell’estensione tag SDK per web.

In [Configurare Adobe Analytics](setup-analytics.md) Nella lezione, sostituisci la suite di rapporti per una pagina utilizzando l’azione Invia evento di Platform Web SDK.

Ora puoi installare l’estensione Platform Web SDK nella tua proprietà tag.

[Successivo: ](install-web-sdk.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
