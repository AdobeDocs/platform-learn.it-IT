---
title: Configurare uno stream di dati
description: Scopri come abilitare un flusso di dati e configurare le soluzioni Experience Cloud. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Datastreams
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: d81e7df36807778967bc0350735aec008fb1a55e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 4%

---

# Configurare uno stream di dati

Scopri come abilitare uno stream di dati e configurare le applicazioni Experience Cloud.

Gli stream di dati indicano all’Edge Network di Adobe Experience Platform dove inviare i dati raccolti da Platform Web SDK. Nella configurazione dei flussi di dati, abilita le applicazioni di Experience Cloud, l’account di Experience Platform e l’inoltro di eventi. Consulta la [Nozioni di base sulla configurazione di uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it) per informazioni più dettagliate.


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
1. Seleziona **[!UICONTROL Nuovo flusso di dati]** sul lato destro dello schermo.
1. Invio `Luma Web SDK: Development Environment` come **[!UICONTROL Nome]**. Questo nome viene utilizzato successivamente quando configuri l’estensione Web SDK nella proprietà tag.
1. Seleziona il `Luma Web Event Data` come **[!UICONTROL Schema Evento]**
1. Seleziona **[!UICONTROL Salva]**

   ![Creare lo stream di dati](assets/datastream-create-new-datastream.png)

Nella schermata successiva è possibile aggiungere al flusso di dati servizi quali applicazioni Adobe, ma a questo punto dell’esercitazione non verrà aggiunto alcun servizio. Lo farai più avanti nelle lezioni [Experience Platform configurazione](setup-experience-platform.md), [Configurare Analytics](setup-analytics.md), [Audience Manager configurazione](setup-audience-manager.md), [Imposta Target](setup-target.md), o [Inoltro eventi](setup-event-forwarding.md).

>[!NOTE]
>
>Quando implementi Platform Web SDK sul tuo sito web, devi creare tre flussi di dati da mappare ai tre ambienti di tag (sviluppo, stage e produzione). Se utilizzi Platform Web SDK con applicazioni basate su Platform, ad esempio Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, assicurati di creare tali flussi di dati nelle sandbox di Platform appropriate.

## Sostituire uno stream di dati

Le sostituzioni dello stream di dati consentono di definire configurazioni aggiuntive per gli stream di dati e quindi di ignorare la configurazione predefinita in determinate condizioni dall’implementazione.


La sostituzione della configurazione dello stream di dati è un processo in due fasi:

1. Innanzitutto, definisci le sostituzioni dello stream di dati nella configurazione dello stream di dati. Questa operazione deve essere eseguita per ogni applicazione di Adobe che si desidera sostituire.
1. Quindi, invii le sostituzioni all’Edge Network tramite un’azione Invia evento SDK per web o tramite una configurazione nell’estensione tag SDK per web.

In [Configurare Adobe Analytics](setup-analytics.md) lezione si sostituisce la suite di rapporti per una pagina utilizzando l’azione Invia evento di Platform Web SDK.

Consulta la [documentazione sulle sostituzioni della configurazione dello stream di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overrides.html?lang=en) per istruzioni dettagliate su come ignorare le configurazioni dello stream di dati.

Ora puoi installare l’estensione Platform Web SDK nella tua proprietà tag.

[Successivo: ](install-web-sdk.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
