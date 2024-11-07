---
title: Attivazione dei segmenti in Microsoft Azure Event Hub - Configurare l’hub eventi in Azure
description: Attivazione dei segmenti in Microsoft Azure Event Hub - Configurare l’hub eventi in Azure
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# 2.4.1 Configurare l’ambiente Microsoft Azure EventHub

Azure Event Hubs è un servizio di sottoscrizione pubblicazione altamente scalabile che può acquisire milioni di eventi al secondo e inviarli in streaming a più applicazioni. Questo consente di elaborare e analizzare le enormi quantità di dati prodotti dai dispositivi e dalle applicazioni collegati.

## 2.4.1.1 Cos’è Azure Event Hub?

Azure Event Hubs è una piattaforma di streaming di big data e un servizio di acquisizione di eventi. Può ricevere ed elaborare milioni di eventi al secondo. I dati inviati a un hub eventi possono essere trasformati e memorizzati utilizzando qualsiasi provider di analisi in tempo reale o adattatori di batch/archiviazione.

Event Hubs rappresenta la **porta principale** di una pipeline di eventi, spesso denominata &quot;event ingestor&quot; nelle architetture della soluzione. Un’acquisizione di eventi è un componente o un servizio che si colloca tra gli editori di eventi (come Adobe Experience Platform RTCDP) e i consumatori di eventi per separare la produzione di un flusso di eventi dal consumo di tali eventi. Event Hubs fornisce una piattaforma di streaming unificata con un buffer di conservazione del tempo, separando i produttori di eventi dai consumatori di eventi.

## 2.4.1.2 Creare uno spazio dei nomi degli hub eventi

Vai a [https://portal.azure.com/#home](https://portal.azure.com/#home) e seleziona **Crea una risorsa**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

Nella schermata delle risorse, immetti **Evento** nella barra di ricerca e seleziona **Hub eventi** dal menu a discesa:

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Fai clic su **Crea**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Se questa è la prima volta che crei una risorsa in Azure, dovrai creare un nuovo **gruppo di risorse**. Se disponi già di un gruppo di risorse, puoi selezionarlo (o crearne uno nuovo).

Seleziona **Crea nuovo**, assegna un nome al gruppo `--aepUserLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

Completare il test dei campi come indicato di seguito:

- Spazio dei nomi : Definisci lo spazio dei nomi, deve essere univoco, utilizza il seguente pattern `--aepUserLdap---aep-enablement`
- Posizione: **Europa occidentale** fa riferimento al centro dati di Azure ad Amsterdam
- Piano tariffario: **Base**
- Unità di velocità effettiva: **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

Fai clic su **Rivedi + crea**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Fai clic su **Crea**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

L’implementazione del gruppo di risorse può richiedere 1-2 minuti; una volta completata, viene visualizzata la seguente schermata:

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 2.4.1.3 Configurare l’hub eventi in Azure

Vai a [https://portal.azure.com/#home](https://portal.azure.com/#home) e seleziona **Tutte le risorse**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

Dall&#39;elenco delle risorse, selezionare lo spazio dei nomi `--aepUserLdap---aep-enablement`:

![1-10-list-resources.png](./images/1-10-list-resources.png)

Nella schermata dei dettagli di `--aepUserLdap---aep-enablement`, seleziona **Hub eventi**:

![1-11-eventub-namespace.png](./images/1-11-eventhub-namespace.png)

Fare clic su **+ Hub eventi**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

Utilizza `--aepUserLdap---aep-enablement-event-hub` come nome e fai clic su **Crea**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

Fai clic su **Hub eventi** nello spazio dei nomi dell&#39;hub eventi. Ora dovresti visualizzare il tuo **Hub eventi** nell&#39;elenco. In questo caso, è possibile passare all&#39;esercizio successivo.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 2.4.1.4 Configurare l’account di archiviazione Azure

Per eseguire il debug della funzione dell&#39;hub eventi di Azure negli esercizi successivi, è necessario fornire un account di archiviazione di Azure come parte della configurazione del progetto di codice di Visual Studio. Ora creerai l’account di archiviazione Azure.

Vai a [https://portal.azure.com/#home](https://portal.azure.com/#home) e seleziona **Crea una risorsa**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Immetti **storage** nella ricerca e seleziona **Account di archiviazione** dall&#39;elenco.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

Seleziona **Crea**.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

Specifica il **gruppo di risorse** (creato all&#39;inizio di questo esercizio), utilizza `--aepUserLdap--aepstorage` come nome dell&#39;account di archiviazione, seleziona **Archiviazione localmente ridondante (LRS)**, quindi fai clic su **Verifica + crea**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

Fai clic su **Crea**.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

La creazione dell&#39;account di archiviazione richiederà un paio di secondi:

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

Al termine della schermata verrà visualizzato il pulsante **Vai alla risorsa**.

Fare clic su **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

L&#39;account di archiviazione è ora visibile in **Risorse recenti**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

Passaggio successivo: [2.4.2 Configurare la destinazione dell&#39;hub eventi di Azure in Adobe Experience Platform](./ex2.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
