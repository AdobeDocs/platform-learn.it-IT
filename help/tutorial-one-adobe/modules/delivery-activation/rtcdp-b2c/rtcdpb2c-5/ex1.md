---
title: 'Raccolta dati Adobe Experience Platform e inoltro lato evento in tempo reale: creazione di una proprietà di inoltro degli eventi di raccolta dati Adobe Experience Platform'
description: Creare una proprietà Inoltro eventi raccolta dati di Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: ac6d09dd-ae8f-4b8a-b543-e4b96aed2c38
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 2%

---

# 2.5.1 Creare una proprietà Inoltro eventi raccolta dati di Adobe Experience Platform

## Cos’è una proprietà di inoltro degli eventi di raccolta dati di Adobe Experience Platform?

In genere, quando i dati vengono raccolti utilizzando Raccolta dati di Adobe Experience Platform, vengono raccolti sul **lato client**. **lato client** è un ambiente come un sito Web o un&#39;app mobile. In Guida introduttiva e Raccolta dati, la configurazione di una proprietà del client di raccolta dati di Adobe Experience Platform è stata discussa in modo approfondito e hai implementato tale proprietà del client di raccolta dati di Adobe Experience Platform sul tuo sito web e sulla tua app mobile, in modo che i dati possano essere raccolti lì quando un cliente interagisce con il sito web e l’app mobile.

Quando i dati di interazione vengono raccolti dalla proprietà Client di raccolta dati di Adobe Experience Platform, il sito web o l’app mobile invia una richiesta all’Edge di Adobe. Edge è l’ambiente di raccolta dati di Adobe ed è il punto di ingresso per i dati di click-stream nell’ecosistema Adobe. Da Edge, i dati raccolti vengono quindi inviati ad applicazioni come Adobe Experience Platform, Adobe Analytics, Adobe Audience Manager o Adobe Target.

Con l’aggiunta di una proprietà Adobe Experience Platform Data Collection Event Forwarding, ora è possibile configurare una proprietà Adobe Experience Platform Data Collection che ascolta i dati in arrivo su Edge. Quando la proprietà Inoltro eventi raccolta dati di Adobe Experience Platform in esecuzione su Edge vede i dati in arrivo, può utilizzarli e inoltrarli a un’altra posizione. Che da qualche altra parte ora può essere anche un webhook esterno non Adobe, il che rende possibile inviare tali dati ad esempio al tuo data lake di scelta, a un’applicazione decisionale o a qualsiasi altra applicazione che ha la capacità di aprire un webhook.

La configurazione di una proprietà di Inoltro eventi raccolta dati di Adobe Experience Platform ha un aspetto familiare con una proprietà lato client, con la possibilità di configurare elementi dati e regole come in passato con le proprietà del client raccolta dati di Adobe Experience Platform. Tuttavia, il modo in cui i dati saranno accessibili e utilizzati sarà leggermente diverso, a seconda del caso d’uso.

Iniziamo creando la proprietà Inoltro eventi raccolta dati di Adobe Experience Platform.

## Creare una proprietà Inoltro eventi raccolta dati di Adobe Experience Platform

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/). Nel menu a sinistra, fai clic su **Inoltro eventi**. Viene quindi visualizzata una panoramica di tutte le proprietà di inoltro degli eventi di raccolta dati di Adobe Experience Platform disponibili. Fare clic sul pulsante **Crea proprietà**.

![SSF raccolta dati Adobe Experience Platform](./images/launchhome.png)

In alternativa, se sono già state create altre proprietà di Inoltro eventi, l’interfaccia utente sarà leggermente diversa. In tal caso, fare clic su **Nuova proprietà**.

![SSF raccolta dati Adobe Experience Platform](./images/launchhomea.png)

È ora necessario immettere un nome per la proprietà Inoltro eventi raccolta dati di Adobe Experience Platform. Come convenzione di denominazione, utilizzare `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. In questo esempio, il nome è **vangeluw - Demo System (22/02/2022) (Edge)**. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/ssf1.png)

Tornerai quindi all’elenco delle proprietà di Inoltro eventi raccolta dati di Adobe Experience Platform. Fai clic su per aprire la proprietà appena creata.

![SSF raccolta dati Adobe Experience Platform](./images/ssf2.png)

## Configurare l’estensione Adobe Cloud Connector

Nel menu a sinistra, vai a **Estensioni**. L&#39;estensione **Core** è già configurata.

![SSF raccolta dati Adobe Experience Platform](./images/ssf3.png)

Vai a **Catalogo**. Vedrai l&#39;estensione **Adobe Cloud Connector**, insieme a molti altri. Fai clic su **Installa** per installarlo.

![SSF raccolta dati Adobe Experience Platform](./images/ssf4.png)

L’estensione verrà quindi aggiunta. Nessuna configurazione da eseguire in questo passaggio. Ti verrà inviata nuovamente la panoramica delle estensioni installate.

![SSF raccolta dati Adobe Experience Platform](./images/ssf5.png)

## Distribuire la proprietà Inoltro eventi raccolta dati di Adobe Experience Platform

Nel menu a sinistra, vai a **Flusso di pubblicazione**. Fare clic su **Aggiungi libreria**.

![SSF raccolta dati Adobe Experience Platform](./images/ssf6.png)

Immetti il nome **Principale**, seleziona l&#39;ambiente **Sviluppo (sviluppo)** e fai clic su **+ Aggiungi tutte le risorse modificate**.

![SSF raccolta dati Adobe Experience Platform](./images/ssf7.png)

Poi vedrai questo. Fai clic su **Salva e genera per sviluppo**.

![SSF raccolta dati Adobe Experience Platform](./images/ssf8.png)

La libreria verrà quindi generata e potrebbe richiedere 1-2 minuti.

![SSF raccolta dati Adobe Experience Platform](./images/ssf10.png)

## Passaggi successivi

Vai a [2.5.2 Aggiorna lo stream di dati per rendere disponibili i dati per la proprietà Inoltro eventi raccolta dati](./ex2.md){target="_blank"}

Torna a [Connessioni Real-Time CDP: Inoltro eventi](./aep-data-collection-ssf.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
