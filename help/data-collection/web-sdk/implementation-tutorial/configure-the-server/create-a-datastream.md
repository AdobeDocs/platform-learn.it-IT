---
title: Creare un flusso di dati
description: Creare un flusso di dati
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Creare un flusso di dati

I dati inviati dal sito web raggiungono un set di server di Adobe denominati [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Questa rete è in grado di inviare i dati al [Set di dati Adobe Experience Platform creato in precedenza](create-a-schema.md) e altri prodotti in Adobe Experience Cloud. Questi prodotti di Adobe possono anche rispondere con i dati alla tua pagina web. Ad esempio, Edge Network può restituire contenuti di personalizzazione da Adobe Target.

Per configurare quali prodotti Adobe Edge Network esegue il shuttle dei dati da e verso, è necessario creare un datastream. Quando Edge Network riceve i dati dalla pagina web, consulta il datastream creato, legge la configurazione e invia i dati ai prodotti di Adobe appropriati.

Per creare un datastream, passa prima al [!UICONTROL Datastreams] visualizza in [!UICONTROL Raccolta dati]. Fai clic su [!UICONTROL Crea Datastream] nell&#39;angolo in alto a destra. Specifica un nome per il datastream.

![Nome e descrizione di Datastream](../../../assets/implementation-strategy/datastream-name-description.png)

La schermata successiva ti consente di configurare quali prodotti Adobe devono ricevere i dati inviati dal sito web. Ai fini di questa esercitazione, abilita solo Adobe Experience Platform, seleziona il set di dati creato in precedenza (che sarà nel valore predefinito [!UICONTROL Prod] sandbox) e fai clic su [!UICONTROL Salva].

![Configurazione del prodotto Datastream](../../../assets/implementation-strategy/datastream-product-configuration.png)

Il tuo datastream è stato creato.

## Ambienti Datastream

Le aziende solitamente hanno un percorso di promozione per qualsiasi aggiornamento del sito web. In genere, un addetto al marketing o un tecnico dell&#39;azienda (a seconda dei cambiamenti) verifica i propri cambiamenti in un ambiente di sviluppo utilizzato solo da tale persona. Una volta che si sentono a loro agio con le modifiche, queste vengono promosse a un ambiente di staging in cui ricevono ulteriori test. Infine, le modifiche vengono pubblicate sul sito web di produzione che gli utenti visualizzano. I datastreams supportano questo pattern di promozione.

Dopo aver fatto clic su [!UICONTROL Salva], dovresti notare che sono stati creati automaticamente tre ambienti di datastream: [!UICONTROL Ambiente di sviluppo], [!UICONTROL Ambiente di staging]e [!UICONTROL Ambiente di produzione].

![Ambienti Datastream](../../../assets/implementation-strategy/datastream-environments.png)

Se fai clic su ogni ambiente del datastream, noterai che a tutti è stata assegnata la stessa configurazione che hai fornito. Tuttavia, questi ambienti possono essere personalizzati individualmente.

Se hai già familiarità con Adobe Experience Platform Tags, potresti avere già familiarità con il concetto di ambiente di sviluppo, staging e produzione. Gli ambienti all’interno di Tag sono correlati agli ambienti all’interno di un datastream. Quando sposti una libreria di tag attraverso il flusso di lavoro di pubblicazione dei tag dallo sviluppo, alla gestione temporanea e alla produzione, anche l’ambiente del datastream utilizzato passerà automaticamente da [!UICONTROL Ambiente di sviluppo], a [!UICONTROL Ambiente di staging], a [!UICONTROL Ambiente di produzione]. Questo ti consente, ad esempio, di inviare dati in un set di dati mentre le modifiche sono in fase di sviluppo e di inviare dati a un set di dati diverso una volta che le modifiche sono in produzione. In questo modo i dati di produzione possono essere mantenuti liberi da qualsiasi dato di spazzatura generato durante il processo di sviluppo. In seguito, discuteremo degli ambienti di datastream durante la configurazione delle estensioni nella proprietà tag.

Il server è ora completamente configurato per ricevere dati dalla pagina web.
