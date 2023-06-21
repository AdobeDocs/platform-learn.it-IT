---
title: Acquisire dati batch
seo-title: Ingest batch data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Acquisire dati batch
description: In questa lezione, acquisirai dati batch in Experience Platform utilizzando vari metodi.
role: Data Engineer
feature: Data Ingestion
kt: 4348
thumbnail: 4348-ingest-batch-data.jpg
exl-id: fc7db637-e191-4cc7-9eec-29f4922ae127
source-git-commit: 0b13a4fa625cd29cc98c319b81fcb2a278b7b19a
workflow-type: tm+mt
source-wordcount: '2528'
ht-degree: 0%

---

# Acquisire dati batch

<!-- 1hr-->
In questa lezione, acquisirai dati batch in Experience Platform utilizzando vari metodi.

L’inserimento di dati in batch consente di acquisire una grande quantità di dati in Adobe Experience Platform contemporaneamente. Puoi acquisire dati batch in un caricamento una tantum nell’interfaccia di Platform o utilizzando l’API. Puoi anche configurare caricamenti in batch pianificati regolarmente da servizi di terze parti, come i servizi di archiviazione cloud, utilizzando i connettori di origine.

**Ingegneri dati** dovrà acquisire dati batch all’esterno di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sull’acquisizione dei dati:
>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)


## Autorizzazioni richieste

In [Configurare le autorizzazioni](configure-permissions.md) Per completare questa lezione, è necessario impostare tutti i controlli di accesso necessari.

<!--
* Permission item **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]**, **[!UICONTROL Manage Datasets]** and **[!UICONTROL Data Monitoring]**
* Permission items **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

Per l’esercizio Sources (Origini) è necessario avere accesso a un server (S)FTP o a una soluzione di archiviazione cloud. Se non ne disponi, esiste una soluzione alternativa.

## Acquisire dati in batch con l’interfaccia utente di Platform

I dati possono essere caricati direttamente in un set di dati nella schermata dei set di dati in formati JSON e parquet. Questo è un ottimo modo per testare l’acquisizione di alcuni dei tuoi dati dopo aver creato una

### Scaricare e preparare i dati

Innanzitutto, ottieni i dati di esempio e personalizzali per il tuo tenant:

>[!NOTE]
>
>Dati contenuti nel [luma-data.zip](assets/luma-data.zip) il file è fittizio e deve essere utilizzato solo a scopo dimostrativo.

1. Scarica [luma-data.zip](assets/luma-data.zip) al tuo **Risorse di esercitazione Luma** cartella.
1. Decomprimi il file, creando una cartella denominata `luma-data` che contiene i quattro file di dati che utilizzeremo in questa lezione
1. Apri `luma-loyalty.json` in un editor di testo e sostituire tutte le istanze di `_techmarketingdemos` con il tuo id tenant underscore, come visualizzato nei tuoi schemi:
   ![Sottolinea ID tenant](assets/ingestion-underscoreTenant.png)

1. Salva il file aggiornato

### Inserire i dati

1. Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra
1. Apri il `Luma Loyalty Dataset`
1. Scorri verso il basso fino a visualizzare **[!UICONTROL Aggiungi dati]** nella colonna di destra
1. Carica `luma-loyalty.json` file.
1. Una volta caricato il file, viene visualizzata una riga per il batch
1. Se ricarichi la pagina dopo alcuni minuti, dovresti notare che il batch è stato caricato correttamente con 1000 record e 1000 frammenti di profilo.

   ![Acquisizione](assets/ingestion-loyalty-uploadJson.png)
   <!--do i need to explain error diagnostics and partial ingestion-->

>[!NOTE]
>
>Sono disponibili alcune opzioni: **[!UICONTROL Diagnostica degli errori]** e **[!UICONTROL Acquisizione parziale]**, che verrà visualizzata su vari schermi in questa lezione. Queste opzioni non sono trattate nell&#39;esercitazione. Informazioni rapide:
>
>* L’abilitazione della diagnostica degli errori genera dati sull’acquisizione dei dati, che puoi esaminare utilizzando l’API di accesso ai dati. Ulteriori informazioni in [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html).
>* L’acquisizione parziale ti consente di acquisire dati contenenti errori, fino a una determinata soglia che puoi specificare. Ulteriori informazioni in [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/partial.html)

### Convalidare i dati

Sono disponibili alcuni modi per verificare che i dati siano stati acquisiti correttamente.

#### Convalida nell’interfaccia utente di Platform

Per confermare che i dati sono stati acquisiti nel set di dati:

1. Nella stessa pagina in cui hai acquisito i dati, seleziona la **[!UICONTROL Anteprima set di dati]** pulsante in alto a destra
1. Seleziona la **Anteprima** e dovresti essere in grado di visualizzare alcuni dei dati acquisiti.

   ![Anteprima del set di dati riuscito](assets/ingestion-loyalty-preview.png)


Per confermare che i dati sono arrivati nel profilo (potrebbero essere necessari alcuni minuti per l’atterraggio dei dati):

1. Vai a **[!UICONTROL Profili]** nel menu di navigazione a sinistra
1. Seleziona l’icona accanto a **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** per aprire il modale
1. Seleziona il `Luma Loyalty Id` namespace
1. Quindi inserisci uno dei `loyaltyId` valori del set di dati,  `5625458`
1. Seleziona **[!UICONTROL Visualizza]**
   ![Conferma un profilo dal set di dati](assets/ingestion-loyalty-profile.png)

#### Convalida con eventi di acquisizione dati

Se ti sei iscritto agli eventi di acquisizione dati della lezione precedente, controlla l’URL univoco del sito webhook.site. Dovresti visualizzare tre richieste nell’ordine seguente, con un po’ di tempo tra le due, con le seguenti `eventCode` valori:

1. `ing_load_success`- il batch come acquisito
1. `ig_load_success`- il batch è stato acquisito in un grafo di identità
1. `ps_load_success`- il batch è stato acquisito nel servizio profilo

![Webhook di acquisizione dati](assets/ingestion-loyalty-webhook.png)

Consulta la [documentazione](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events) per ulteriori dettagli sulle notifiche.

## Acquisire dati in batch con API Platform

Ora carichiamo i dati utilizzando l’API.

>[!NOTE]
>
>Architetti dei dati, puoi caricare i dati CRM tramite il metodo dell’interfaccia utente.

### Scaricare e preparare i dati

1. Dovresti avere già scaricato e decompresso [luma-data.zip](assets/luma-data.zip) nel tuo `Luma Tutorial Assets` cartella.
2. Apri `luma-crm.json` in un editor di testo e sostituire tutte le istanze di `_techmarketingdemos` con il tuo id tenant underscore, come mostrato negli schemi
3. Salva il file aggiornato

### Ottieni l’ID del set di dati

Innanzitutto, prendiamo l’ID del set di dati del set di dati in cui vogliamo acquisire i dati:

1. Apri [!DNL Postman]
1. Se non hai un token di accesso, apri la richiesta **[!DNL OAuth: Request Access Token]** e seleziona **Invia** per richiedere un nuovo token di accesso, proprio come hai fatto in [!DNL Postman] lezione.
1. Apri le variabili di ambiente e assicurati che il valore di **CONTAINER_ID** è fermo `tenant`
1. Apri la richiesta **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]** e seleziona **Invia**
1. Dovresti ricevere un `200 OK` risposta
1. Copia l’ID del `Luma CRM Dataset` dal corpo della risposta
   ![Ottieni l’ID del set di dati](assets/ingestion-crm-getDatasetId.png)

### Creare il batch

Ora possiamo creare un batch nel set di dati:

1. Scarica [Acquisizione dei dati API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json) al tuo `Luma Tutorial Assets` cartella
1. Importa la raccolta in [!DNL Postman]
1. Seleziona la richiesta **[!DNL Data Ingestion API > Batch Ingestion > Create a new batch in Catalog Service.]**
1. Incolla quanto segue come **Corpo** della richiesta, ***sostituzione del valore datasetId con il proprio***:

   ```json
   {
       "datasetId":"REPLACE_WITH_YOUR_OWN_DATASETID",
       "inputFormat": {
           "format": "json"
       }
   }
   ```

1. Seleziona la **Invia** pulsante
1. Dovresti ricevere una risposta Creata 201 contenente l’ID del nuovo batch.
1. Copia il `id` del nuovo batch
   ![Batch creato](assets/ingestion-crm-createBatch.png)

### Inserire i dati

Ora possiamo caricare i dati nel batch:

1. Seleziona la richiesta **[!DNL Data Ingestion API > Batch Ingestion > Upload a file to a dataset in a batch.]**
1. In **Parametri** , inserisci l’ID del set di dati e l’ID del batch nei rispettivi campi
1. In **Parametri** , immetti `luma-crm.json` come **filePath**
1. In **Corpo** , seleziona la scheda **binario** opzione
1. Seleziona il download `luma-crm.json` dal tuo locale `Luma Tutorial Assets` cartella
1. Seleziona **Invia** e dovresti ottenere una risposta di 200 OK con &quot;1&quot; nel corpo della risposta

   ![Dati caricati](assets/ingestion-crm-uploadFile.png)

A questo punto, se osservi il batch nell’interfaccia utente di Platform, vedrai che si trova in una &quot;[!UICONTROL Caricamento]&quot;stato:
![Caricamento batch](assets/ingestion-crm-loading.png)

Poiché l’API Batch viene spesso utilizzata per caricare più file, devi comunicare a Platform quando un batch è completo, operazione che eseguiremo nel passaggio successivo.

### Completa il batch

Per completare il batch:

1. Seleziona la richiesta **[!DNL Data Ingestion API > Batch Ingestion > Finish uploading a file to a dataset in a batch.]**
1. In **Parametri** , immetti `COMPLETE` come **azione**
1. In **Parametri** , immettere l&#39;ID batch. Non preoccuparti dell’ID del set di dati o di filePath, se presente.
1. Assicurati che l’URL del POST sia `https://platform.adobe.io/data/foundation/import/batches/:batchId?action=COMPLETE` e che non siano presenti riferimenti superflui al `datasetId` o `filePath`
1. Seleziona **Invia** e dovresti ottenere una risposta di 200 OK con &quot;1&quot; nel corpo della risposta

   ![Batch completato](assets/ingestion-crm-complete.png)

### Convalidare i dati

#### Convalida nell’interfaccia utente di Platform

Verifica che i dati siano stati inseriti nell’interfaccia utente di Platform come hai fatto per il set di dati Fedeltà.

Innanzitutto, verifica che il batch mostri che sono stati acquisiti 1000 record:

![Batch completata](assets/ingestion-crm-success.png)

Quindi, conferma il batch utilizzando il set di dati di anteprima:

![Anteprima batch](assets/ingestion-crm-preview.png)

Infine, conferma che uno dei profili è stato creato cercando uno dei profili da `Luma CRM Id` spazio dei nomi, ad esempio `112ca06ed53d3db37e4cea49cc45b71e`

![Profilo acquisito](assets/ingestion-crm-profile.png)

C&#39;è una cosa interessante che è appena successa che voglio sottolineare. Apri quella `Danny Wright` profilo. Il profilo ha sia `Lumacrmid` e un `Lumaloyaltyid`. Ricorda la `Luma Loyalty Schema` conteneva due campi di identità, ID fedeltà Luma e ID CRM. Ora che abbiamo caricato entrambi i set di dati, sono stati uniti in un singolo profilo. I dati sulla fedeltà avevano `Daniel` come nome e &quot;New York City&quot; come indirizzo di casa, mentre i dati CRM avevano `Danny` come nome e `Portland` come indirizzo dell’abitazione del cliente con lo stesso ID fedeltà. Torneremo al motivo per cui viene visualizzato il nome `Danny` nella lezione sui criteri di unione.

Congratulazioni, hai appena unito i profili.

![Profilo unito ](assets/ingestion-crm-profileLinkedIdentities.png)

#### Convalida con eventi di acquisizione dati

Se ti sei iscritto agli eventi di acquisizione dati della lezione precedente, controlla l’URL univoco del sito webhook.site. Dovresti ricevere tre richieste, proprio come per i dati fedeltà:

![Webhook di acquisizione dati](assets/ingestion-crm-webhook.png)

Consulta la [documentazione](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html#available-status-notification-events) per ulteriori dettagli sulle notifiche.

## Acquisire dati con flussi di lavoro

Vediamo un altro modo di caricare i dati. La funzione Flussi di lavoro consente di acquisire dati CSV che non sono già modellati in XDM.

### Scaricare e preparare i dati

1. Dovresti avere già scaricato e decompresso [luma-data.zip](assets/luma-data.zip) nel tuo `Luma Tutorial Assets` cartella.
1. Conferma di avere`luma-products.csv`

### Creare un flusso di lavoro

Ora configuriamo il flusso di lavoro:

1. Vai a **[!UICONTROL Flussi di lavoro]** nel menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Mappa lo schema CSV a XDM]** e seleziona la **[!UICONTROL Launch]** pulsante
   ![Avvia il flusso di lavoro](assets/ingestion-products-launchWorkflow.png)
1. Seleziona il `Luma Product Catalog Dataset` e seleziona la **[!UICONTROL Successivo]** pulsante
   ![Seleziona il set di dati](assets/ingestion-products-selectDataset.png)
1. Aggiungi il `luma-products.csv` file scaricato e seleziona il file **[!UICONTROL Successivo]** pulsante
   ![Seleziona il set di dati](assets/ingestion-products-selectData.png)
1. Ora ti trovi nell’interfaccia di mappatura, in cui puoi mappare un campo dai dati di origine (uno dei nomi di colonna nel `luma-products.csv` XDM nello schema di destinazione. Nel nostro esempio, i nomi delle colonne sono sufficientemente vicini ai nomi dei campi dello schema da consentire al mapper di rilevare automaticamente la mappatura corretta. Se il mapper non è in grado di rilevare automaticamente il campo corretto, seleziona l’icona a destra del campo di destinazione per selezionare il campo XDM corretto. Inoltre, se non desideri acquisire una delle colonne dal file CSV, puoi eliminare la riga dal mapper. Puoi giocare e modificare le intestazioni di colonna nella sezione `luma-products.csv` per acquisire familiarità con il funzionamento del mapper.
1. Seleziona la **[!UICONTROL Fine]** pulsante
   ![Seleziona il set di dati](assets/ingestion-products-mapper.png)

### Convalidare i dati

Una volta caricato il batch, verifica il caricamento visualizzando l’anteprima del set di dati.

Poiché il `Luma Product SKU` è uno spazio dei nomi non relativo alle persone, non verranno visualizzati profili per gli sku del prodotto.

Dovresti vedere i tre hit nel tuo webhook.

## Acquisire dati con origini

Ok, hai fatto le cose nel modo più difficile. Ora spostiamoci nella terra promessa _automatizzato_ acquisizione batch! Quando dico, &quot;IMPOSTA!&quot; dite: &quot;DIMENTICATELO!&quot; &quot;IMPOSTALO!&quot; &quot;DIMENTICATELO!&quot; &quot;IMPOSTALO!&quot; &quot;DIMENTICATELO!&quot; Scherzi a parte, non faresti mai una cosa del genere! Ok, tornate al lavoro. Hai quasi finito.

Vai a **[!UICONTROL Sorgenti]** nel menu di navigazione a sinistra per aprire il catalogo Sources. Qui vedrai diverse integrazioni pronte all’uso con i principali fornitori di dati e storage del settore.

![Catalogo di origine](assets/ingestion-offline-sourceCatalog.png)

Ok, acquisiamo i dati utilizzando un connettore di origine.

Questo esercizio sarà scegliere il proprio stile di avventura. Sto per mostrare il flusso di lavoro utilizzando il connettore di origine FTP. Puoi utilizzare un connettore di origine diverso per l’archiviazione cloud, utilizzato dalla tua azienda, oppure caricare il file json utilizzando l’interfaccia utente del set di dati, come abbiamo fatto con i dati fedeltà.

Molte delle origini hanno un flusso di lavoro di configurazione simile, in cui:

1. Immetti i dettagli di autenticazione
1. Seleziona i dati da acquisire
1. Seleziona il set di dati di Platform in cui desideri acquisirlo
1. Mappa i campi sullo schema XDM
1. Scegli la frequenza con cui vuoi riacquisire i dati da quella posizione

>[!NOTE]
>
>I dati di acquisto offline che utilizzeremo in questo esercizio contengono dati datetime. I dati di data e ora devono essere in [Stringhe formattate ISO 8061](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) o il tempo Unix formattato in millisecondi (1531263959000) e vengono convertiti al momento dell’acquisizione nel tipo XDM di destinazione. Per ulteriori informazioni sulla conversione dei dati e su altri vincoli, consulta [Documentazione API per l’acquisizione in batch](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/api-overview.html#types).

### Scarica, prepara e carica i dati sul fornitore di archiviazione cloud preferito

1. Dovresti avere già scaricato e decompresso [luma-data.zip](assets/luma-data.zip) nel tuo `Luma Tutorial Assets` cartella.
1. Apri `luma-offline-purchases.json` in un editor di testo e sostituire tutte le istanze di `_techmarketingdemos` con il tuo id tenant underscore, come mostrato negli schemi
1. Aggiorna tutti i timestamp in modo che gli eventi si verifichino nell’ultimo mese (ad esempio, cerca `"timestamp":"2022-06` e sostituire l&#39;anno e il mese)
1. Scegli il provider di archiviazione cloud preferito, assicurandoti che sia disponibile nella [!UICONTROL Sorgenti] catalogo
1. Carica `luma-offline-purchases.json` in una posizione nel provider di archiviazione cloud preferito

### Inserire i dati nella posizione di archiviazione cloud preferita

1. Nell’interfaccia utente di Platform, filtra il [!UICONTROL Sorgenti] catalogo a **[!UICONTROL Archiviazione cloud]**
1. Tieni presente che nella sezione sono presenti collegamenti utili per la documentazione di `...`
1. Nella casella del fornitore di archiviazione cloud preferito, seleziona la **[!UICONTROL Configura]** pulsante
   ![Seleziona configura](assets/ingestion-offline-selectFTP.png)
1. **[!UICONTROL Autenticazione]** è il primo passaggio. Inserisci il nome dell’account, ad esempio `Luma's FTP Account` e i dettagli di autenticazione. Questo passaggio dovrebbe essere abbastanza simile per tutte le origini di archiviazione cloud, anche se i campi possono variare leggermente. Dopo aver immesso i dettagli di autenticazione per un account, è possibile riutilizzarli per altre connessioni di origine che potrebbero inviare dati diversi su pianificazioni diverse da altri file nello stesso account
1. Seleziona la **[!UICONTROL Pulsante Connetti all&#39;origine]**
1. Una volta che Platform si è connessa correttamente all’origine, seleziona **[!UICONTROL Successivo]** pulsante
   ![Autentica nell&#39;origine](assets/ingestion-offline-authentication.png)

1. Il giorno **[!UICONTROL Seleziona dati]** passaggio, l’interfaccia utente utilizzerà le credenziali per aprire la cartella nella soluzione di archiviazione cloud
1. Seleziona i file da acquisire, ad esempio `luma-offline-purchases.json`
1. Come **[!UICONTROL Formato dati]**, seleziona `XDM JSON`
1. Puoi quindi visualizzare in anteprima la struttura json e i dati di esempio nel file
1. Seleziona la **[!UICONTROL Successivo]** pulsante
   ![Seleziona i file di dati](assets/ingestion-offline-selectData.png)

1. Il giorno **[!UICONTROL Mappatura]** passaggio, seleziona il tuo `Luma Offline Purchase Events Dataset` e seleziona la **[!UICONTROL Successivo]** pulsante. Nota nel messaggio che, poiché i dati che stiamo acquisendo sono un file JSON, non esiste un passaggio di mappatura in cui mappiamo il campo sorgente al campo di destinazione. I dati JSON devono essere già in XDM. Se stavi acquisendo un CSV, visualizzeresti l’interfaccia utente di mappatura completa in questo passaggio:
   ![Seleziona il set di dati](assets/ingestion-offline-mapping.png)
1. Il giorno **[!UICONTROL Pianificazione]** scegli la frequenza con cui vuoi riacquisire i dati dall’origine. Dedica un momento a scoprire le opzioni disponibili. Stiamo per effettuare un’acquisizione una tantum, quindi lascia **[!UICONTROL Frequenza]** il **[!UICONTROL Una volta]** e seleziona la **[!UICONTROL Successivo]** pulsante:
   ![Pianificare il flusso di dati](assets/ingestion-offline-scheduling.png)
1. Il giorno **[!UICONTROL Dettagli del flusso di dati]** passo, puoi scegliere un nome per il flusso di dati, inserire una descrizione facoltativa, attivare la diagnostica degli errori e l’acquisizione parziale. Lascia le impostazioni invariate e seleziona la **[!UICONTROL Successivo]** pulsante:
   ![Modificare i dettagli del flusso di dati](assets/ingestion-offline-detail.png)
1. Il giorno **[!UICONTROL Revisione]** fase, è possibile rivedere tutte le impostazioni insieme e modificarle o selezionare **[!UICONTROL Fine]** pulsante
1. Dopo il salvataggio verrà visualizzata una schermata simile alla seguente:
   ![Completa](assets/ingestion-offline-complete.png)

### Convalidare i dati

Una volta caricato il batch, verifica il caricamento visualizzando l’anteprima del set di dati.

Dovresti vedere i tre hit nel tuo webhook.

Cercare il profilo con il valore `5625458` nel `loyaltyId` per verificare se nel loro profilo sono presenti eventi di acquisto. Dovresti vedere un acquisto. Puoi approfondire i dettagli dell’acquisto selezionando **[!UICONTROL Visualizza JSON]**:

![Evento di acquisto nel profilo](assets/ingestion-offline-eventInProfile.png)

## Strumenti ETL

Adobe collabora con più fornitori ETL per supportare l’acquisizione dei dati in Experience Platform. A causa della varietà di fornitori di terze parti, ETL non è trattato in questa esercitazione, anche se è opportuno rivedere alcune di queste risorse:

* [Sviluppo di integrazioni ETL per Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/etl/home.html)
* [Pagina Connettore Adobe Experience Platform Informatica su Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101570.informatica-adobe-experience-cloud-connector.html)
* [Documentazione informatica del connettore Adobe Experience Platform](https://docs.informatica.com/integration-cloud/cloud-data-integration-connectors/current-version/adobe-experience-platform-connector/preface.html)
* [[!DNL Snaplogic] Pacchetto Snap Di Adobe Experience Platform](https://www.snaplogic.com/resources/videos/august-2020-aep)

## Risorse aggiuntive

* [Documentazione sull’acquisizione in batch](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html)
* [Riferimento API per acquisizione in batch](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Batch-Ingestion)

Ora andiamo [inviare dati tramite Web SDK](ingest-streaming-data.md)
