---
title: Installare e configurare l’estensione tag di Adobe Experience Platform Web SDK
description: Scopri come installare e configurare l’estensione tag Platform Web SDK nell’interfaccia di Data Collection. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK, Tags
jira: KT-15404
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 9%

---

# Installare l’estensione tag Adobe Experience Platform Web SDK

Scopri come installare e configurare l’estensione tag Adobe Experience Platform Web SDK. Il modo più semplice per implementare Web SDK è utilizzare i tag di Adobe Tag Manager (precedentemente noti come Launch). L’estensione tag Platform Web SDK è _Solo estensione tag_ necessario per inviare dati a _tutte le applicazioni Adobe Experience Cloud_, tra cui [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), REAL-TIME CUSTOMER DATA PLATFORM e [Journey Optimizer](setup-web-channel.md)!

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Creare una proprietà tag nell’interfaccia di Data Collection
* Installare l’estensione tag Platform Web SDK
* Mappa lo stream di dati creato in precedenza sull’estensione

## Prerequisiti

Devi aver completato le lezioni precedenti in questa esercitazione:

* [Configurare uno stream di dati](configure-datastream.md)

### Aggiungi una proprietà tag

Innanzitutto devi avere una proprietà tag. Una proprietà è un contenitore per tutti i JavaScript, le regole e le altre funzioni necessarie per raccogliere i dettagli da una pagina web e inviarla a varie posizioni.

Crea una nuova proprietà tag per l’esercitazione:

1. Apri [Interfaccia di Data Collection](https://launch.adobe.com/){target="_blank"}
1. Seleziona **[!UICONTROL Tag]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Nuova proprietà]** pulsante
   ![Aggiungi una nuova proprietà](assets/websdk-property-addNewProperty.png)
1. Come **[!UICONTROL Nome]**, immetti `Web SDK Course` (aggiungi il tuo nome alla fine, se più persone della tua azienda stanno seguendo questo tutorial)
1. Come **[!UICONTROL Domini]**, immetti `enablementadobe.com` (spiegato in seguito)
1. Seleziona **[!UICONTROL Salva]**
   ![Dettagli proprietà](assets/websdk-property-propertyDetails.png)

## Aggiungere l’estensione Web SDK

Una volta create le proprietà dello schema XDM, dello stream di dati e dei tag, puoi installare l’estensione Platform Web SDK:

1. Apri la nuova proprietà tag
1. Vai a **[!UICONTROL Estensioni]** > **[!UICONTROL Catalogo]**
1. Cerca `Adobe Experience Platform Web SDK`
1. Seleziona **[!UICONTROL Installa]**

   ![Installare l’estensione Web SDK](assets/extension-platform-web-sdk.png)


## Collegare l’estensione allo stream di dati

Lascia la maggior parte delle impostazioni predefinite e aggiornale in un secondo momento, in base alle esigenze. L’unica cosa da fare ora è collegare l’estensione allo stream di dati:

1. Sotto **[!UICONTROL Flussi di dati]**, seleziona la **[!UICONTROL Scegli dall’elenco]** metodo di input
1. Seleziona lo stream di dati creato in precedenza, `Luma Web SDK`
1. Seleziona **[!UICONTROL Salva]**

   >[!NOTE]
   >
   > Se non riesci a trovare il flusso di dati, vai al [Configurare uno stream di dati](configure-datastream.md) lezione e segui i passaggi per crearne uno

   ![Selezione dello stream di dati](assets/extension-luma-web-sdk-datastream-extension.png)

Per ulteriori informazioni su ciascuna sezione dell&#39;estensione, vedi [Configurare l’estensione Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).

>[!NOTE]
>
>Anche se non hai configurato un CNAME in [!UICONTROL Dominio Edge] In questa lezione, l’Adobe consiglia di utilizzare un CNAME quando si implementa Platform Web SDK sul proprio sito web. Nonostante un’implementazione CNAME non offra vantaggi in termini di durata dei cookie, potrebbero esserci altri vantaggi. Questi vantaggi includono ad blocker e browser meno comuni che impediscono l’invio dei dati a domini classificati come tracciatori. In questi casi, l’utilizzo di un CNAME potrebbe agevolare la raccolta di dati relativi agli utenti che utilizzano tali strumenti.

>[!NOTE]
>
>Durante questa esercitazione, puoi configurare un solo stream di dati e associarlo a tutti gli ambienti di tag (sviluppo, stage e produzione). Quando implementi Platform Web SDK sul tuo sito web, devi configurare un flusso di dati separato per ogni ambiente e mapparlo di conseguenza nella configurazione dell’estensione.

Ora che hai installato Platform Web SDK e lo hai associato allo stream di dati, puoi iniziare a raccogliere dati.

[Successivo: ](create-data-elements.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
