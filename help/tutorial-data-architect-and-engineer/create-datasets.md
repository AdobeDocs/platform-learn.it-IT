---
title: Creare set di dati
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Creare set di dati
description: In questa lezione verranno creati set di dati per la ricezione dei dati.
role: Data Architect, Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 10%

---

# Creare set di dati

<!--15min-->

In questa lezione verranno creati set di dati per la ricezione dei dati. Sarai entusiasta di scoprire che questa è la lezione più breve dell’esercitazione.

Tutti i dati acquisiti correttamente in Adobe Experience Platform vengono mantenuti nel data lake come set di dati. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

**Architetti di dati** dovrà creare set di dati al di fuori di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sui set di dati:
>[!VIDEO](https://video.tv.adobe.com/v/27269?learn=on)

## Autorizzazioni richieste

In [Configurare le autorizzazioni](configure-permissions.md) Per completare questa lezione, è necessario impostare tutti i controlli di accesso necessari.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Creare set di dati nell’interfaccia utente

In questo esercizio creeremo i set di dati nell’interfaccia utente di. Iniziamo con i dati fedeltà:

1. Vai a **[!UICONTROL Set di dati]** nell’area di navigazione a sinistra dell’interfaccia utente di Platform
1. Seleziona la **[!UICONTROL Crea set di dati]** pulsante
   ![Creare un set di dati](assets/datasets-createDataset.png)

1. Nella schermata successiva, seleziona **Crea set di dati dallo schema**
1. Nella schermata successiva, seleziona il tuo `Luma Loyalty Schema` e quindi selezionare **[!UICONTROL Successivo]** pulsante
   ![Seleziona il set di dati](assets/datasets-selectSchema.png)

1. Denomina il set di dati `Luma Loyalty Dataset` e seleziona la **[!UICONTROL Fine]** pulsante
   ![Denomina il set di dati](assets/datasets-nameDataset.png)
1. Quando il set di dati è stato salvato, viene visualizzata una schermata come questa:
   ![Set di dati creato](assets/datasets-created.png)

Tutto qui. Te l&#39;ho detto che sarebbe stato veloce. Crea questi altri set di dati seguendo gli stessi passaggi:

1. `Luma Offline Purchase Events Dataset` per `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` per `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` per `Luma Product Catalog Schema`


## Creare un set di dati tramite API

Ora crea il `Luma CRM Dataset` utilizzando l’API.

>[!NOTE]
>
>Se desideri saltare l’esercizio API e creare `Luma CRM Dataset` nell’interfaccia utente, operazione corretta. Assegna un nome `Luma CRM Dataset` e utilizza `Luma CRM Schema`.

### Ottieni l’ID dello schema da utilizzare nel set di dati

Prima di tutto dobbiamo ottenere `$id` del `Luma CRM Schema`:

1. Apri [!DNL Postman]
1. Se non hai un token di accesso, apri la richiesta **[!DNL OAuth: Request Access Token]** e seleziona **Invia** per richiedere un nuovo token di accesso, proprio come hai fatto in [!DNL Postman] lezione.
1. Apri la richiesta **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Seleziona la **Invia** pulsante
1. Dovresti ricevere una risposta 200
1. Cerca nella risposta per `Luma CRM Schema` elemento e copia `$id` valore
   ![Copia il $id](assets/dataset-crm-getSchemaId.png)

### Creare il set di dati

Ora puoi creare il set di dati:

1. Scarica [API.postman_collection.json di Catalog Service](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) al tuo `Luma Tutorial Assets` cartella.
1. Importa la raccolta in [!DNL Postman]
1. Seleziona la richiesta **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. Incolla quanto segue come **Corpo** della richiesta, ***sostituzione del valore id con il tuo***:

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
1. Dovresti ricevere una risposta Creata 201 contenente l’ID del nuovo set di dati.
   ![Set di dati creato con API, il $id personalizzato utilizzato nel corpo](assets/datasets-crm-created.png)

>[!TIP]
>
> Problemi comuni relativi a questa richiesta e possibili correzioni:
>
> * `400: There was a problem retrieving xdm schema`. Assicurati di aver sostituito l’ID nell’esempio precedente con l’ID del tuo `Luma CRM Schema`
> * Nessun token di autenticazione: esegui **OAuth: richiedi token di accesso** richiesta di generazione di un nuovo token
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: aggiorna il **CONTAINER_ID** variabile di ambiente da `global` a `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: verifica le autorizzazioni utente nell’Admin Console


È possibile tornare al **[!UICONTROL Set di dati]** Nell’interfaccia utente di Platform, puoi verificare se la creazione di tutti e cinque i set di dati è andata a buon fine.
![Cinque set di dati completati](assets/datasets-allComplete.png)


## Risorse aggiuntive

* [Documentazione sui set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=it)
* [Riferimento API per i set di dati (parte di Catalog Service)](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

Ora che tutti i nostri schemi, identità e set di dati sono presenti, possiamo [abilitarli per Real-Time Customer Profile](enable-profiles.md).
