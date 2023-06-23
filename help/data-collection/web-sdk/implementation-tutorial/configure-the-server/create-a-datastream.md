---
title: Creare un flusso di dati
description: Creare un flusso di dati
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 52378f63-8a6d-49ed-a21a-65b74fe1ddc4
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Creare un flusso di dati

I dati inviati dal sito Web raggiungono un set di server di Adobe denominati [Adobe Experience Platform Edge](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Questa rete è in grado di inviare i tuoi dati al [Set di dati Adobe Experience Platform creato in precedenza](create-a-schema.md) e altri prodotti in Adobe Experience Cloud. Questi prodotti di Adobe possono anche rispondere con i dati alla tua pagina web. Edge Network, ad esempio, può restituire contenuti di personalizzazione da Adobe Target.

Per configurare quali prodotti Adobe Edge Network archivia i dati da e verso, è necessario creare un flusso di dati. Quando Edge Network riceve i dati dalla pagina web, consulta il flusso di dati creato, ne legge la configurazione e inoltra i dati ai prodotti di Adobe appropriati.

Per creare un flusso di dati, passa innanzitutto a [!UICONTROL Flussi di dati] visualizza in [!UICONTROL Raccolta dati]. Clic [!UICONTROL Crea stream di dati] in alto a destra. Immetti un nome per lo stream di dati.

![Nome e descrizione dello stream di dati](../../../assets/implementation-strategy/datastream-name-description.png)

La schermata successiva consente di configurare quali prodotti Adobe devono ricevere i dati inviati dal sito Web. Ai fini di questa esercitazione, abilita solo Adobe Experience Platform, seleziona il set di dati creato in precedenza (che sarà l’impostazione predefinita [!UICONTROL Prod] sandbox) e fai clic su [!UICONTROL Salva].

![Configurazione del prodotto Datastream](../../../assets/implementation-strategy/datastream-product-configuration.png)

Lo stream di dati è stato creato.

## Ambienti stream di dati

In genere, le aziende dispongono di un percorso di promozione per qualsiasi aggiornamento del sito web. In genere, un addetto al marketing o un ingegnere dell’azienda verifica le modifiche in un ambiente di sviluppo utilizzato solo da quell’utente. Una volta apportate le modifiche, queste vengono promosse in un ambiente di staging in cui vengono sottoposte a ulteriori test. Infine, le modifiche vengono pubblicate nel sito web di produzione visualizzato dagli utenti. Gli stream di dati supportano questo pattern di promozione.

Dopo aver fatto clic su [!UICONTROL Salva], dovresti aver notato che sono stati creati automaticamente tre ambienti di stream di dati: [!UICONTROL Ambiente di sviluppo], [!UICONTROL Ambiente di staging], e [!UICONTROL Ambiente di produzione].

![Ambienti stream di dati](../../../assets/implementation-strategy/datastream-environments.png)

Se fai clic su ogni ambiente di flusso di dati, noterai che a tutti è stata assegnata la stessa configurazione fornita. Tuttavia, questi ambienti possono essere personalizzati individualmente.

Se conosci i Tag Adobe Experience Platform, potresti avere già familiarità con il concetto di ambiente di sviluppo, staging e produzione. Gli ambienti all’interno dei tag sono relativi agli ambienti all’interno di un flusso di dati. Quando si sposta una libreria di tag attraverso il flusso di lavoro di pubblicazione dei tag da sviluppo, staging, produzione, anche l’ambiente dello stream di dati utilizzato passa automaticamente da [!UICONTROL Ambiente di sviluppo], a [!UICONTROL Ambiente di staging], a [!UICONTROL Ambiente di produzione]. Ciò ti consente, ad esempio, di inviare dati in un set di dati mentre le modifiche sono in fase di sviluppo e di inviare dati a un set di dati diverso una volta che le modifiche sono in produzione. In questo modo i dati di produzione possono essere mantenuti liberi da eventuali dati di Garbage durante il processo di sviluppo. Gli ambienti dello stream di dati verranno discussi in seguito durante la configurazione delle estensioni nella proprietà tag.

Il server è ora completamente configurato per ricevere i dati dalla pagina web.
