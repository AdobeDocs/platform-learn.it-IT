---
title: Attivazione dei segmenti in Microsoft Azure Event Hub - Configurare l’hub eventi in Azure
description: Attivazione dei segmenti in Microsoft Azure Event Hub - Configurare l’hub eventi in Azure
kt: 5342
doc-type: tutorial
exl-id: 5c77d09f-18c8-4e29-9392-3f6f8004fa7c
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# 2.4.2 Configurare l’ambiente Microsoft Azure EventHub

Azure Event Hubs è un servizio di sottoscrizione pubblicazione altamente scalabile che può acquisire milioni di eventi al secondo e inviarli in streaming a più applicazioni. Questo consente di elaborare e analizzare le enormi quantità di dati prodotti dai dispositivi e dalle applicazioni collegati.

## Cos’è Azure Event Hub?

Azure Event Hubs è una piattaforma di streaming di big data e un servizio di acquisizione di eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/archiviazione.

Event Hubs rappresenta la **porta principale** di una pipeline di eventi, spesso denominata &quot;event ingestor&quot; nelle architetture della soluzione. Un’acquisizione di eventi è un componente o un servizio che si colloca tra gli editori di eventi (come Adobe Experience Platform RTCDP) e i consumatori di eventi per separare la produzione di un flusso di eventi dal consumo di tali eventi. Event Hubs fornisce una piattaforma di streaming unificata con un buffer di conservazione del tempo, separando i produttori di eventi dai consumatori di eventi.

## Creare uno spazio dei nomi degli hub eventi

Vai a [https://portal.azure.com/#home](https://portal.azure.com/#home) e seleziona **Crea una risorsa**.

![1-01-open-azure-portal.png](./images/101openazureportal.png)

Nella schermata delle risorse, immetti **Evento** nella barra di ricerca. Trova la scheda **Hub eventi**, fai clic su **Crea**, quindi su **Hub eventi**.

![1-02-search-event-hubs.png](./images/102searcheventhubs.png)

Se questa è la prima volta che crei una risorsa in Azure, dovrai creare un nuovo **gruppo di risorse**. Se disponi già di un gruppo di risorse, puoi selezionarlo (o crearne uno nuovo).

Fai clic su **Crea nuovo** e assegna un nome al gruppo `--aepUserLdap---aep-enablement`, quindi fai clic su **OK**.

![1-04-create-resource-group.png](./images/104createresourcegroup.png)

Compila gli altri campi come indicato:

- Spazio dei nomi : Definisci lo spazio dei nomi, deve essere univoco, utilizza il seguente pattern `--aepUserLdap---aep-enablement`
- Ubicazione: scegli una posizione
- Piano tariffario: **Base**
- Unità di velocità effettiva: **1**

Fai clic su **Rivedi + crea**.

![1-05-create-namespace.png](./images/105createnamespace.png)

Fai clic su **Crea**.

![1-07-namespace-create.png](./images/107namespacecreate.png)

L’implementazione del gruppo di risorse può richiedere 1-2 minuti; una volta completata, viene visualizzata la seguente schermata:

![1-08-namespace-deploy.png](./images/108namespacedeploy.png)

## Configurare l’hub eventi in Azure

Vai a [https://portal.azure.com/#home](https://portal.azure.com/#home) e seleziona **Tutte le risorse**.

![1-09-all-resources.png](./images/109allresources.png)

Nell&#39;elenco delle risorse, fare clic sullo spazio dei nomi degli hub eventi `--aepUserLdap---aep-enablement`:

![1-10-list-resources.png](./images/110listresources.png)

Nella schermata dei dettagli di `--aepUserLdap---aep-enablement`, vai a **Entità** e fai clic su **Hub eventi**:

![1-11-eventub-namespace.png](./images/111eventhubnamespace.png)

Fare clic su **+ Hub eventi**.

![1-12-add-event-hub.png](./images/112addeventhub.png)

Utilizza `--aepUserLdap---aep-enablement-event-hub` come nome e fai clic su **Rivedi + Crea**.

![1-13-create-event-hub.png](./images/113createeventhub.png)

Fai clic su **Crea**.

![1-13-create-event-hub.png](./images/113createeventhub1.png)

In **Hub eventi** nello spazio dei nomi dell&#39;hub eventi, il **Hub eventi** verrà visualizzato nell&#39;elenco.

![1-14-event-hub-list.png](./images/114eventhublist.png)

## Configurare l’account di archiviazione Azure

Per eseguire il debug della funzione dell&#39;hub eventi di Azure negli esercizi successivi, è necessario fornire un account di archiviazione di Azure come parte della configurazione del progetto di codice di Visual Studio. Ora creerai l’account di archiviazione Azure.

Vai a [https://portal.azure.com/#home](https://portal.azure.com/#home) e seleziona **Crea una risorsa**.

![1-15-event-hub-storage.png](./images/115eventhubstorage.png)

Immettere **account di archiviazione** nella ricerca, trovare la scheda per **account di archiviazione** e fare clic su **account di archiviazione**.

![1-16-event-hub-search-storage.png](./images/116eventhubsearchstorage.png)

Specifica il **gruppo di risorse** (creato all&#39;inizio di questo esercizio), utilizza `--aepUserLdap--aepstorage` come nome dell&#39;account di archiviazione e seleziona **Archiviazione localmente ridondante (LRS)**, quindi fai clic su **Rivedi + crea**.

![1-18-event-hub-create-review-storage.png](./images/118eventhubcreatereviewstorage.png)

Fai clic su **Crea**.

![1-19-event-hub-submit-storage.png](./images/119eventhubsubmitstorage.png)

La creazione del nostro account di archiviazione richiederà un paio di secondi:

![1-20-event-hub-deploy-storage.png](./images/120eventhubdeploystorage.png)

Al termine della schermata verrà visualizzato il pulsante **Vai alla risorsa**.

Fare clic su **Home**.

![1-21-event-hub-deploy-ready-storage.png](./images/121eventhubdeployreadystorage.png)

L&#39;account di archiviazione è ora visibile in **Risorse recenti**.

![1-22-event-hub-deploy-resources-list.png](./images/122eventhubdeployresourceslist.png)

## Passaggi successivi

Vai a [2.4.3 Configurare la destinazione dell&#39;hub eventi di Azure in Adobe Experience Platform](./ex3.md){target="_blank"}

Torna a [Real-Time CDP: da Audience Activation a Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
