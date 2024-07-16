---
title: Inviare dati all’Experience Platform con Platform Mobile SDK
description: Scopri come inviare dati ad Experience Platform.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
jira: KT-14637
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 2%

---

# Invia dati all’Experience Platform

Scopri come inviare dati da app mobili a Adobe Experience Platform.

Questa lezione facoltativa è valida per tutti i clienti di Real-time Customer Data Platform (Real-Time CDP), Journey Optimizer e Customer Journey Analytics. Ad Experience Platform, la base dei prodotti Experience Cloud, è un sistema aperto che trasforma tutti i tuoi dati (Adobi e non Adobi) in solidi profili cliente. Questi profili cliente vengono aggiornati in tempo reale e utilizzano informazioni basate sull’intelligenza artificiale per aiutarti a fornire le esperienze giuste su ogni canale.

I dati [event](events.md), [lifecycle](lifecycle-data.md) e [identity](identity.md) che hai raccolto e inviato all&#39;Edge Network di Platform nelle lezioni precedenti vengono inoltrati ai servizi configurati nel flusso di dati, incluso Adobe Experience Platform.

![Architettura](assets/architecture-aep.png)


## Prerequisiti

È necessario eseguire il provisioning della tua organizzazione e concedere le autorizzazioni per Adobe Experience Platform.

Se non hai accesso, puoi [saltare questa lezione](install-sdks.md).

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Crea un set di dati di Experience Platform.
* Configura lo stream di dati per inoltrare i dati ad Experience Platform.
* Convalida i dati nel set di dati.
* Abilita lo schema e il set di dati per Real-Time Customer Profile.
* Convalidare i dati in Real-Time Customer Profile.
* Convalida i dati nel grafico delle identità.


## Creare un set di dati

Tutti i dati acquisiti correttamente in Adobe Experience Platform vengono memorizzati nel data lake come set di dati. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati (in genere una tabella) che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati. Per informazioni, consulta la [documentazione](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=it).

1. Passa all&#39;interfaccia Experience Platform selezionandola dal menu App ![App](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) in alto a destra.


1. Seleziona **[!UICONTROL Set di dati]** dal menu di navigazione a sinistra.

1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Crea set di dati]**.

1. Seleziona **[!UICONTROL Crea set di dati dallo schema]**.
   ![home set di dati](assets/dataset-create.png)

1. Cerca lo schema. ad esempio utilizzando `Luma Mobile` nel campo di ricerca.
1. Selezionare lo schema, ad esempio **[!DNL Luma Mobile App Event Schema]**.

1. Seleziona **[!UICONTROL Avanti]**.
   ![configurazione set di dati](assets/dataset-configure.png)

1. Fornisci un **[!UICONTROL Nome]**, ad esempio `Luma Mobile App Events Dataset` e una **[!UICONTROL Descrizione]**.

1. Seleziona **[!UICONTROL Fine]**.
   ![fine set di dati](assets/dataset-finish.png)


## Aggiungi servizio flusso di dati Adobe Experience Platform

Per inviare i dati XDM dall&#39;Edge Network a Adobe Experience Platform, aggiungi il servizio Adobe Experience Platform allo stream di dati configurato come parte di [Crea uno stream di dati](create-datastream.md).

>[!IMPORTANT]
>
>Puoi abilitare il servizio Adobe Experience Platform solo dopo aver creato un set di dati evento.

1. Nell&#39;interfaccia utente di Data Collection, seleziona **[!UICONTROL Datastreams]** e il tuo datastream.

1. Quindi selezionare ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi servizio]**.

1. Selezionare **[!UICONTROL Adobe Experience Platform]** dall&#39;elenco [!UICONTROL Service].

1. Abilitare il servizio attivando **[!UICONTROL Enabled]**.

1. Seleziona il **[!UICONTROL Set di dati evento]** creato in precedenza, ad esempio **[!DNL Luma Mobile App Event Dataset]**.

1. Seleziona **[!UICONTROL Salva]**.

   ![Aggiungi Adobe Experience Platform come servizio di stream di dati](assets/datastream-service-aep.png)
1. La configurazione finale sarà simile alla seguente.

   ![impostazioni dello stream di dati](assets/datastream-settings.png)


## Convalidare i dati nel set di dati

Dopo aver creato un set di dati e aggiornato lo stream di dati per inviare i dati ad Experience Platform, tutti i dati XDM inviati ad Edge Network Platform vengono inoltrati a Platform e vengono inseriti nel set di dati.

Apri l’app e passa alle schermate in cui tieni traccia degli eventi. Puoi anche attivare le metriche del ciclo di vita.

Apri il set di dati nell’interfaccia di Platform. Dovresti visualizzare i dati in arrivo in batch nel set di dati. I dati in genere arrivano in microbatch ogni 15 minuti, pertanto potresti non visualizzare immediatamente i dati.

![convalida dei batch di set di dati di Platform di destinazione](assets/platform-dataset-batches.png)

Dovresti anche essere in grado di visualizzare record e campi di esempio utilizzando la funzionalità **[!UICONTROL Anteprima set di dati]**:
![convalida ciclo di vita inviato al set di dati della piattaforma](assets/lifecycle-platform-dataset.png)

Uno strumento più affidabile per la convalida dei dati è il [servizio query](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=it) di Platform.

## Abilita Real-Time Customer Profile

Il profilo cliente in tempo reale di Experience Platform consente di creare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. Il profilo ti consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

### Abilita lo schema

1. Aprire lo schema, ad esempio **[!DNL Luma Mobile App Event Schema]**.
1. Abilita **[!UICONTROL Profilo]**.
1. Selezionare **[!UICONTROL I dati per questo schema conterranno un&#39;identità primaria nel campo identityMap.]** nella finestra di dialogo
1. **[!UICONTROL Salva]** lo schema.

   ![abilita lo schema per il profilo](assets/platform-profile-schema.png)

### Abilitare il set di dati

1. Apri il set di dati, ad esempio **[!DNL Luma Mobile App Event Dataset]**.
1. Abilita **[!UICONTROL Profilo]**.

   ![abilita il set di dati per il profilo](assets/platform-profile-dataset.png)

### Convalidare i dati nel profilo

Apri l’app e passa alle schermate in cui stai tracciando gli eventi, ad esempio: accedi all’app Luma e fai un acquisto.

Utilizza Assurance per trovare una delle identità passate in identityMap (E-mail, lumaCrmId o ECID), ad esempio l’ID del sistema di gestione delle relazioni con i clienti.

![acquisire un valore di identità](assets/platform-identity.png)

Nell’interfaccia di Platform,

1. Passa a **[!UICONTROL Profili]** e seleziona **[!UICONTROL Sfoglia]** dalla barra superiore.
1. Specifica i dettagli di identità appena acquisiti, ad esempio `Luma CRM ID` per **[!UICONTROL Identity namespace]** e il valore copiato per **[!UICONTROL Identity value]**. Quindi seleziona **[!UICONTROL Visualizza]**.
1. Per visualizzare i dettagli, seleziona il profilo.

![cercare un valore di identità](assets/platform-profile-lookup.png)

Nella schermata **[!UICONTROL Dettagli]**, puoi visualizzare le informazioni di base sull&#39;utente, incluse le **[!UICONTROL ** identità collegate **]**:
![dettagli profilo](assets/platform-profile-details.png)

Nei **[!UICONTROL Eventi]** puoi visualizzare gli eventi raccolti dall&#39;implementazione della tua app mobile per questo utente:

![eventi profilo](assets/platform-profile-events.png)


Dalla schermata dei dettagli del profilo:

1. Per visualizzare il grafo delle identità, fai clic sul collegamento o passa a **[!UICONTROL Identità]**, quindi seleziona **[!UICONTROL Grafo delle identità]** dalla barra superiore.
1. Per cercare il valore di identità, specificare `Luma CRM ID` come **[!UICONTROL Spazio dei nomi identità]** e il valore copiato come **[!UICONTROL Valore identità]**. Quindi seleziona **[!UICONTROL Visualizza]**.

   Questa visualizzazione mostra tutte le identità collegate tra loro in un profilo e la loro origine. Di seguito è riportato un esempio di grafo di identità costituito da dati raccolti dal completamento di questa esercitazione dell&#39;SDK per dispositivi mobili (Data Source 2) e dell&#39;[esercitazione dell&#39;SDK per web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it) (Data Source 1):

   ![acquisire un valore di identità](assets/platform-profile-identitygraph.png)


## Passaggi successivi

Gli esperti di marketing e analisi possono fare molto di più con i dati acquisiti in Experience Platform, compresa l’analisi di Customer Journey Analytics e la creazione di segmenti in Real-time Customer Data Platform. Stai partendo bene!


>[!SUCCESS]
>
>Ora hai configurato l’app per inviare dati non solo all’Edge Network, ma anche a Adobe Experience Platform.<br>Grazie per aver dedicato il tuo tempo all&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Creare e inviare notifiche push](journey-optimizer-push.md)**
