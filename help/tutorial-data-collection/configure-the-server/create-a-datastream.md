---
title: Creare un flusso di dati
description: Creare un flusso di dati
exl-id: 4a33a7f3-8bd8-4d28-9ae4-a0609444485f
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Creare un flusso di dati

I dati inviati dal sito web con Platform Web SDK raggiungono un set di server di Adobe denominati [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Questa rete può inviare i tuoi dati a [Set di dati Adobe Experience Platform creato in precedenza](create-a-schema.md) e altri prodotti in Adobe Experience Cloud. Questi prodotti di Adobe possono anche rispondere con i dati alla tua pagina web. Ad esempio, Edge Network può restituire contenuti di personalizzazione da Adobe Target.

Per configurare quali prodotti Adobe Edge Network esegue il shuttle dei dati da e verso, è necessario creare un datastream. Quando Edge Network riceve i dati dalla pagina web, consulta il datastream creato, legge la configurazione e invia i dati ai prodotti di Adobe appropriati.

![Configurazione del prodotto Datastream](../assets/datastream-diagram.png)

1. Per creare un datastream, devi prima passare all’interfaccia utente Raccolta dati . Nell’angolo in alto a destra di Platform, fai clic su **[!UICONTROL Selettore applicazioni]** e seleziona **[!UICONTROL Raccolta dati]** dal menu a discesa.
   ![Menu di raccolta dati](../assets/data-collection-menu.png)
1. Una volta visualizzata l’interfaccia di raccolta dati, seleziona **[!UICONTROL Datastreams]** nella navigazione a sinistra e quindi il **[!UICONTROL Nuovo Datastream]** nell&#39;angolo in alto a destra.
1. Specifica un nome per il datastream, seleziona [lo schema creato in precedenza](create-a-schema.md) come **[!UICONTROL Set di dati evento]**, quindi seleziona **[!UICONTROL Salva]** (la mappatura è trattata più avanti).
   ![Nome e descrizione di Datastream](../assets/datastream-name-description.png)

## Aggiungi servizio a datastream

La schermata successiva ti consente di aggiungere quali prodotti e servizi di Adobe devono ricevere i dati inviati dal tuo sito web.

1. Seleziona la **[!UICONTROL Aggiungi servizio]** comando. Ai fini di questa esercitazione, abilita solo Adobe Experience Platform, seleziona [il set di dati creato in precedenza](create-a-dataset.md) e seleziona **[!UICONTROL Salva]** nell&#39;angolo in alto a destra. Il tuo datastream è stato creato.
   ![Configurazione del prodotto Datastream](../assets/datastream-product-configuration.png)

## Ambienti Datastream

Le aziende solitamente hanno un percorso di promozione per qualsiasi aggiornamento del sito web. In genere, un addetto al marketing o un tecnico dell&#39;azienda (a seconda dei cambiamenti) verifica i propri cambiamenti in un ambiente di sviluppo utilizzato solo da tale persona. Una volta che si sentono a loro agio con le modifiche, queste vengono promosse a un ambiente di staging in cui ricevono ulteriori test. Infine, le modifiche vengono pubblicate sul sito web di produzione che gli utenti visualizzano. I datastreams supportano questo pattern di promozione.

Se supporti applicazioni basate su Platform come Real-Time CDP, Journey Optimizer o Customer Journey Analytics, è necessario creare altri datastreams nelle sandbox di Platform separate che corrispondono a questi ambienti.

Se non sei un cliente Platform, puoi creare più datastreams in un’unica sandbox e utilizzare la funzione di copia del datastream per duplicare le impostazioni.

Il server è ora completamente configurato per ricevere dati dalla pagina web.

[Avanti: ](../configure-the-client/whats-a-data-layer.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
