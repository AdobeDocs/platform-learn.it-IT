---
title: Creare set di dati
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Creare set di dati
description: In questa lezione verranno creati set di dati per ricevere i dati.
role: Data Architect, Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 8%

---

# Creare set di dati

<!--15min-->

In questa lezione verranno creati set di dati per ricevere i dati. Sarete entusiasti di sapere che questa è la lezione più breve del tutorial!

Tutti i dati correttamente acquisiti in Adobe Experience Platform vengono memorizzati nel data lake come set di dati. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

**Architetti dei dati** dovrà creare set di dati al di fuori di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sui set di dati:
>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)

## Autorizzazioni necessarie

In [Configurare le autorizzazioni](configure-permissions.md) per completare la lezione, è necessario impostare tutti i controlli di accesso necessari.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Creare set di dati nell’interfaccia utente

In questo esercizio, creeremo i set di dati nell’interfaccia utente. Cominciamo con i dati fedeltà:

1. Vai a **[!UICONTROL Set di dati]** nella navigazione a sinistra dell’interfaccia utente di Platform
1. Seleziona la **[!UICONTROL Creare un set di dati]** pulsante
   ![Creare un set di dati](assets/datasets-createDataset.png)

1. Nella schermata successiva, seleziona **Creare un set di dati dallo schema**
1. Nella schermata successiva, seleziona la `Luma Loyalty Schema` quindi seleziona la **[!UICONTROL Successivo]** pulsante
   ![Selezionare il set di dati](assets/datasets-selectSchema.png)

1. Denomina il set di dati `Luma Loyalty Dataset` e seleziona la **[!UICONTROL Fine]** pulsante
   ![Denomina il set di dati](assets/datasets-nameDataset.png)
1. Una volta salvato il set di dati, verrai portato su una schermata come questa:
   ![Set di dati creato](assets/datasets-created.png)

Tutto qui. Te l&#39;ho detto che sarebbe stato veloce. Crea questi altri set di dati seguendo gli stessi passaggi:

1. `Luma Offline Purchase Events Dataset` per `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` per `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` per `Luma Product Catalog Schema`


## Creare un set di dati tramite API

Ora crea il `Luma CRM Dataset` utilizzando l’API .

>[!NOTE]
>
>Se desideri saltare l’esercizio API e creare la `Luma CRM Dataset` nell&#39;interfaccia utente che va bene. Denomina `Luma CRM Dataset` e utilizza `Luma CRM Schema`.

### Ottieni l’id dello schema da utilizzare nel set di dati

Per prima cosa dobbiamo ottenere il `$id` del `Luma CRM Schema`:

1. Apri [!DNL Postman]
1. Se non hai effettuato una richiesta nelle ultime 24 ore, i token di autorizzazione probabilmente sono scaduti. Apri la richiesta **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** e seleziona **Invia** per richiedere nuovi token JWT e di accesso, proprio come nel [!DNL Postman] lezione.
1. Apri la richiesta **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Seleziona la **Invia** pulsante
1. Dovresti ricevere una risposta di 200
1. Cerca nella risposta per `Luma CRM Schema` e copia il `$id` value
   ![Copia il $id](assets/dataset-crm-getSchemaId.png)

### Creare il set di dati

Ora puoi creare il set di dati:

1. Scarica [API.postman_collection.json del servizio catalogo](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) al tuo `Luma Tutorial Assets` cartella.
1. Importa la raccolta in [!DNL Postman]
1. Seleziona la richiesta **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. Incolla quanto segue come **Corpo** della richiesta, ***sostituzione del valore id con il proprio***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. Seleziona la **Invia** pulsante
1. Dovresti ottenere una risposta Creato 201 contenente l’id del nuovo set di dati.
   ![Set di dati creato con API, il tuo $id personalizzato utilizzato nel corpo](assets/datasets-crm-created.png)

>[!TIP]
>
> Problemi comuni che effettuano questa richiesta e possibili correzioni:
>
> * `400: There was a problem retrieving xdm schema`. Assicurati di aver sostituito l&#39;id nell&#39;esempio precedente con l&#39;id del tuo `Luma CRM Schema`
> * Nessun token di autenticazione: Esegui il **IMS: JWT Genera + Auth tramite token utente** chiamata per generare nuovi token
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: Aggiorna **CONTAINER_ID** variabile di ambiente da `global` a `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Verifica le autorizzazioni utente nell’Admin Console



Puoi tornare alla sezione **[!UICONTROL Set di dati]** nell’interfaccia utente di Platform, puoi verificare la corretta creazione di tutti e cinque i set di dati.
![Cinque set di dati completati](assets/datasets-allComplete.png)


## Risorse aggiuntive

* [Documentazione dei set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=it)
* [Riferimento API dei set di dati (parte del servizio catalogo)](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

Ora che tutti i nostri schemi, le nostre identità e i nostri set di dati sono pronti, possiamo [attivarli per il profilo cliente in tempo reale](enable-profiles.md).
