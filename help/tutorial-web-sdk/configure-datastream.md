---
title: Configurare un datastream
description: Scopri come abilitare un datastream e configurare le soluzioni Experience Cloud. Questa lezione fa parte dell’esercitazione Implementa Adobe Experience Cloud con SDK per web.
feature: Datastreams
exl-id: ca28374a-9fe0-44de-a7ac-0aa046712515
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 6%

---

# Configurare un datastream

Scopri come abilitare un datastream e configurare le soluzioni Experience Cloud.

I Datastreams indicano a Adobe Experience Platform Edge Network dove inviare i dati raccolti dall’SDK per web di Platform. Nella configurazione dei datastreams, abilita le applicazioni Experience Cloud, l&#39;account Experience Platform e l&#39;inoltro degli eventi. Consulta la sezione [Nozioni di base sulla configurazione di un Datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en) per informazioni più dettagliate.

## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Creare un flusso di dati
* Abilitare le applicazioni Experience Cloud
* Abilita Experience Platform

## Prerequisiti

Prima di configurare il datastream, devi aver già completato le lezioni seguenti:

* [Configurare le autorizzazioni](configure-permissions.md)
* [Configurare uno schema](configure-schemas.md)
* [Configurare uno spazio dei nomi di identità](configure-identities.md)

## Creare un flusso di dati

Ora puoi creare un datastream per indicare a Platform Edge Network dove inviare i dati raccolti dall’SDK per web.

**Per creare un datastream:**

1. Apri [Interfaccia di raccolta dati](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Assicurati di essere nella sandbox corretta

   >[!NOTE]
   >
   >Se sei cliente di un’applicazione basata su Platform come Real-Time CDP, ti consigliamo di utilizzare una sandbox di sviluppo per questa esercitazione. In caso contrario, utilizza il **[!UICONTROL Prod]** sandbox.

1. Vai a **[!UICONTROL Datastreams]** nella navigazione a sinistra
1. Seleziona **[!UICONTROL Nuovo Datastream]** sul lato destro dello schermo.
1. Inserisci `Luma Web SDK` come **[!UICONTROL Nome]**. In seguito, quando configuri l’estensione Web SDK nella proprietà tag, viene fatto riferimento a questo nome.
1. Seleziona la tua `Luma Web Event Data` come **[!UICONTROL Schema evento]**
1. Seleziona **[!UICONTROL Salva]**

   ![Creare il datastream](assets/datastream-create-datastream.png)

   >[!AVAILABILITY]
   >
   >La funzione di mappatura verrà integrata in questa esercitazione in una data successiva.




Nella schermata successiva, puoi aggiungere servizi come applicazioni di Adobe al datastream, ma a questo punto non aggiungerai alcun servizio nell’esercitazione. Lo farai più tardi nelle lezioni [Imposta Experience Platform](setup-experience-platform.md), [Configurazione di Analytics](setup-analytics.md), [Imposta Audience Manager](setup-audience-manager.md), [Configurazione di Target](setup-target.md)oppure [Inoltro eventi](setup-event-forwarding.md).

>[!NOTE]
>
>Quando implementi Platform Web SDK sul tuo sito web, devi creare tre datastreams da mappare ai tuoi tre ambienti di tag (sviluppo, stage e produzione). Se utilizzi Platform Web SDK con applicazioni basate su Platform come Adobe Real-time Customer Data Platform o Adobe Journey Optimizer, assicurati di creare tali datastreams nelle sandbox Platform appropriate.

È ora possibile installare l’estensione Platform Web SDK nella proprietà tag.

[Avanti: ](install-web-sdk.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nel conoscere Adobe Experience Platform Web SDK. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
