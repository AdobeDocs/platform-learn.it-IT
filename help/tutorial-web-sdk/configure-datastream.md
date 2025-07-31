---
title: Configurare uno stream di dati per Platform Web SDK
description: Scopri come abilitare uno stream di dati e configurare le soluzioni Experience Cloud. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Datastreams
jira: KT-15399
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 8%

---

# Configurare uno stream di dati

Scopri come configurare uno stream di dati per Adobe Experience Platform Web SDK.

[Datastream](https://experienceleague.adobe.com/it/docs/experience-platform/datastreams/overview) indica ad Adobe Experience Platform Edge Network dove inviare i dati raccolti da Platform Web SDK. Nella configurazione dei flussi di dati, abilita le applicazioni Experience Cloud, l’account Experience Platform e l’inoltro di eventi.

![SDK Web, flussi di dati e diagramma di Edge Network](assets/dc-websdk-datastreams.png)

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Creare un flusso di dati
* Introduzione alle sostituzioni dello stream di dati

## Prerequisiti

Prima di configurare lo stream di dati, è necessario aver già completato le lezioni seguenti:

* [Configurare uno schema](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)

## Creare un flusso di dati

Ora è possibile creare un flusso di dati per indicare a Platform Edge Network dove inviare i dati raccolti da Web SDK.

**Per creare uno stream di dati:**

1. Apri l&#39;interfaccia di [Data Collection](https://experience.adobe.com/data-collection/){target="_blank"}
1. Assicurati di trovarti nella sandbox corretta

   >[!NOTE]
   >
   >Se sei il cliente di un’applicazione basata su Platform come Real-Time CDP o Journey Optimizer, per questa esercitazione ti consigliamo di utilizzare una sandbox di sviluppo. In caso contrario, utilizza la sandbox **[!UICONTROL Prod]**.

1. Vai a **[!UICONTROL Datastreams]** nel menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Nuovo flusso di dati]**
1. Immetti `Luma Web SDK: Development Environment` come **[!UICONTROL Nome]**. Questo nome viene utilizzato successivamente quando configuri l’estensione Web SDK nella proprietà tag.
1. Seleziona **[!UICONTROL Salva]**

   ![Crea lo stream di dati](assets/datastream-create-new-datastream.png)

   >[!NOTE]
   >
   >Non è necessario selezionare uno schema. La selezione dello schema è necessaria solo se si utilizza la funzionalità [Preparazione dati per raccolta dati](/help/data-collection/edge/data-prep.md).

Nella schermata successiva, è possibile aggiungere al flusso di dati servizi come applicazioni Adobe, ma al momento non è possibile aggiungere alcun servizio. Lo farai in seguito nelle lezioni [Configurazione di Experience Platform](setup-experience-platform.md), [Configurazione di Analytics](setup-analytics.md), [Configurazione di Audience Manager](setup-audience-manager.md), [Configurazione di Target](setup-target.md) o [Inoltro eventi](setup-event-forwarding.md).

>[!NOTE]
>
>Quando implementi Platform Web SDK sul tuo sito web, devi creare tre flussi di dati da mappare ai tre ambienti di tag (sviluppo, stage e produzione). Se utilizzi Platform Web SDK con applicazioni basate su Platform, ad esempio Adobe Real-Time Customer Data Platform o Adobe Journey Optimizer, assicurati di creare tali flussi di dati nelle sandbox di Platform appropriate.

## Sostituire uno stream di dati

Le [sostituzioni dello stream di dati](https://experienceleague.adobe.com/it/docs/experience-platform/datastreams/overrides) consentono di definire configurazioni aggiuntive per lo stream di dati e quindi di ignorare la configurazione predefinita in determinate condizioni.

La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, puoi definire le sostituzioni dello stream di dati nella configurazione del servizio dello stream di dati. Ad esempio, puoi definire suite di rapporti di Analytics alternative, aree di lavoro di Target o set di dati di Platform da utilizzare come sostituzioni.
1. Quindi, invii le sostituzioni ad Edge Network tramite un’azione Invia evento di Web SDK oppure tramite una configurazione nell’estensione tag Web SDK.

Nella lezione [Configurare Adobe Analytics](setup-analytics.md) è possibile ignorare la suite di rapporti per una pagina utilizzando l&#39;azione Invia evento di Platform Web SDK.

Ora puoi installare l’estensione Platform Web SDK nella proprietà tag.

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
