---
title: Installare e configurare l’estensione tag Adobe Experience Platform Web SDK
description: Scopri come installare e configurare l’estensione tag SDK per web Platform nell’interfaccia di raccolta dati. Questa lezione fa parte dell’esercitazione Implementa Adobe Experience Cloud con SDK per web.
feature: Web SDK
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 13%

---

# Installare l’estensione tag Adobe Experience Platform Web SDK

Scopri come installare e configurare l’estensione tag SDK per web Platform nell’interfaccia di raccolta dati. Questa estensione di tag è _Solo estensione tag_ necessari per inviare dati a _tutte le applicazioni Adobe Experience Cloud_, tra cui [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-time Customer Data Platform e Journey Optimizer!

## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Creare una proprietà tag nell’interfaccia Raccolta dati
* Installare l’estensione tag SDK per web di Platform
* Mappa il datastream creato in precedenza sull&#39;estensione

## Prerequisiti

Devi aver completato le lezioni precedenti in questa esercitazione:

* [Configurare le autorizzazioni](configure-permissions.md)
* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi di identità](configure-identities.md)
* [Configurare un datastream](configure-datastream.md)

## Installare l’estensione Experience Platform Web SDK

### Aggiungi una proprietà

Innanzitutto devi disporre di una proprietà tag . Una proprietà è un contenitore per tutti i JavaScript, le regole e altre funzionalità necessarie per raccogliere i dettagli da una pagina web e inviarli a varie posizioni.

Crea una nuova proprietà tag per l’esercitazione:

1. Apri [Interfaccia di raccolta dati](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Seleziona **[!UICONTROL Tag]** nella navigazione a sinistra
1. Seleziona il pulsante **[!UICONTROL Nuova proprietà]**
   ![Aggiungi una nuova proprietà](assets/websdk-property-addNewProperty.png)
1. Come **[!UICONTROL Nome]**, inserisci `Web SDK Course` (aggiungi il tuo nome alla fine, se più persone della tua azienda stanno seguendo questa esercitazione)
1. Come **[!UICONTROL Domini]**, inserisci `enablementadobe.com` (spiegato più avanti)
1. Seleziona **[!UICONTROL Salva]**
   ![Dettagli proprietà](assets/websdk-property-propertyDetails.png)

## Aggiungere l’estensione SDK per web

Con lo schema, il datastream e la proprietà tag XDM ora creati, puoi installare l’estensione Platform Web SDK:

1. Apri la nuova proprietà tag
1. Vai a **[!UICONTROL Estensioni]** > **[!UICONTROL Catalogo]**
1. Cerca `Adobe Experience Platform Web SDK`
1. Seleziona **[!UICONTROL Installa]**

   ![Installa estensione SDK per web](assets/extension-platform-web-sdk.jpg)


## Collegare l’SDK web di Platform al tuo datastream

Lascia la maggior parte delle impostazioni predefinite e aggiornale in un secondo momento, in base alle esigenze. L&#39;unica cosa che devi fare ora è collegare l&#39;estensione al tuo datastream:

1. Sotto **[!UICONTROL Datastreams]**, seleziona **[!UICONTROL Scegli dall’elenco]** metodo di input
1. Seleziona il datastream creato in precedenza, `Luma Web SDK`
1. Seleziona **[!UICONTROL Salva]**
   >[!NOTE]
   >
   > Se non riesci a trovare il tuo datastream, vai al [Configurare un datastream](configure-datastream.md) e segui i passaggi per crearne una

   ![Selezione di Datastream](assets/extension-luma-web-sdk-datastream-extension.png)

Dopo aver installato Platform Web SDK e averlo associato al datastream, puoi iniziare a mappare gli elementi dati a un oggetto XDM con lo schema creato.

>[!NOTE]
>
>Durante questa esercitazione, configuri un solo datastream e lo associ a tutti gli ambienti di tag (sviluppo, stage e produzione). Quando implementi Platform Web SDK sul tuo sito web, devi configurare un datastream separato per ogni ambiente e mapparlo agli ambienti di tag utilizzando **[!UICONTROL Metodo di input]** > **[!UICONTROL Immetti i valori]**
>
>![Selezione di Datastream](assets/extension-luma-web-sdk-datastream-extension-enterValues.png)

>[!NOTE]
>
>Non hai configurato un CNAME nel [!UICONTROL Dominio Edge] in questa lezione, Adobe consiglia di utilizzare un CNAME per implementare Platform Web SDK sul sito web. Nonostante un’implementazione CNAME non offra vantaggi in termini di durata dei cookie, potrebbero esserci altri vantaggi. Questi vantaggi includono ad blocker e browser meno comuni che impediscono l’invio dei dati ai domini classificati come tracciatori. In questi casi, l’utilizzo di un CNAME potrebbe agevolare la raccolta di dati relativi agli utenti che utilizzano tali strumenti.

Per ulteriori informazioni su ciascuna sezione dell&#39;estensione, vedi [Configurare l’estensione Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html)



[Avanti: ](create-data-elements.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nel conoscere Adobe Experience Platform Web SDK. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
