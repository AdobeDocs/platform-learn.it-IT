---
title: Creare uno schema XDM per le implementazioni di Platform Mobile SDK
description: Scopri come creare uno schema XDM per gli eventi delle app mobili.
feature: Mobile SDK,Schemas
jira: KT-14624
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 2%

---

# Creare uno schema XDM

Scopri come creare uno schema XDM per gli eventi delle app mobili.

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), gestito da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

## Cosa sono gli schemi XDM?

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni che consentono a qualsiasi applicazione di comunicare con i servizi di Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più veloce e integrato. Ottieni informazioni preziose dalle azioni dei clienti, definisci i tipi di pubblico dei clienti attraverso i segmenti e utilizzi gli attributi del cliente a scopo di personalizzazione.

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, consulta le [nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/schema/composition) o la playlist [Modellare i dati sull&#39;esperienza del cliente con XDM](https://experienceleague.adobe.com/it/playlists/experience-platform-model-your-customer-experience-data-with-xdm).

>[!TIP]
>
>Se conosci Analytics Solution Design Reference (SDR), puoi considerare uno schema come un SDR più affidabile. Per ulteriori informazioni, vedere [Creare e gestire un documento Solution Design Reference (SDR)](https://experienceleague.adobe.com/it/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr).

## Prerequisiti

Per completare la lezione, devi disporre dell’autorizzazione per creare uno schema Experience Platform.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Creare uno schema nell’interfaccia di Data Collection
* Aggiungere un gruppo di campi standard allo schema
* Creare e aggiungere un gruppo di campi personalizzato allo schema

## Passare agli schemi

1. Accedi a Adobe Experience Cloud.

1. Assicurati di trovarti nella sandbox di Experience Platform che stai utilizzando per questa esercitazione.

1. Apri il commutatore di app ![Commutatore di app](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) (in alto a destra),

1. Seleziona **[!UICONTROL Raccolta dati]** dal menu.

   ![Accesso ad Experience Cloud](assets/experiencecloud-login.png){zoomable="yes"}

   >[!NOTE]
   >
   > Per questa esercitazione, i clienti di applicazioni basate su Platform come Real-Time CDP devono utilizzare una sandbox di sviluppo. Altri clienti utilizzano la sandbox di produzione predefinita.


1. Seleziona ![Schemi](/help/assets/icons/Schemas.svg) **[!UICONTROL Schemi]** in **[!UICONTROL Gestione dati]** nella barra a sinistra.

   ![tag nella schermata iniziale](assets/mobile-schema-navigate.png){zoomable="yes"}

Ora ti trovi nella pagina degli schemi principali e viene visualizzato un elenco degli schemi esistenti. Puoi anche visualizzare le schede corrispondenti ai blocchi predefiniti principali di uno schema:

* **I gruppi di campi** sono componenti riutilizzabili che definiscono uno o più campi per acquisire dati specifici, ad esempio dettagli personali, preferenze di hotel o indirizzo.
* **Le classi** definiscono gli aspetti comportamentali dei dati contenuti nello schema. Ad esempio: `XDM ExperienceEvent` acquisisce serie temporali, dati evento e `XDM Individual Profile` acquisisce dati attributo relativi a un individuo.
* **I tipi di dati** vengono utilizzati come tipi di campi di riferimento nelle classi o nei gruppi di campi allo stesso modo dei campi letterali di base.

Le descrizioni di cui sopra rappresentano una panoramica di alto livello. Per ulteriori dettagli, consulta il video [Elementi di base dello schema](https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/schemas/schema-building-blocks) o leggi [Nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/schema/composition) nella documentazione del prodotto.

In questa esercitazione utilizzi il gruppo di campi Evento esperienza del consumatore e creane uno personalizzato per illustrare il processo.

>[!NOTE]
>
>Adobe continua ad aggiungere altri gruppi di campi standard che devono essere utilizzati quando possibile. Questi campi sono compresi implicitamente dai servizi di Experience Platform e forniscono maggiore coerenza quando vengono utilizzati tra i componenti di Platform. L’utilizzo di gruppi di campi standard offre vantaggi tangibili, come la mappatura automatica nelle funzioni di Analytics e AI in Platform.

## Architettura dello schema dell’app Luma

In uno scenario reale, il processo di progettazione dello schema potrebbe essere simile al seguente:

* Raccogliere i requisiti aziendali.
* Trova gruppi di campi predefiniti per soddisfare il maggior numero possibile di requisiti.
* Crea gruppi di campi personalizzati per eventuali spazi.

A scopo di apprendimento, puoi utilizzare gruppi di campi predefiniti e personalizzati.

* **Evento esperienza del consumatore**: gruppo di campi predefinito con molti campi comuni.
* **Informazioni app**: gruppo di campi personalizzato progettato per simulare i concetti di TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Crea uno schema

1. Selezionare ![AddCircle](/help/assets/icons/AddCircle.svg) **[!UICONTROL Crea schema]**.

1. Nella finestra di dialogo **[!UICONTROL Crea schema]**, seleziona **[!UICONTROL Manuale]**. Utilizza **[!UICONTROL Seleziona]** per continuare.

   ![Manuale schema](assets/schema-manual.png){zoomable="yes"}

1. Nel passaggio **[!UICONTROL Seleziona una classe]** della procedura guidata **[!UICONTROL Crea schema]**, seleziona **[!UICONTROL Evento esperienza]** sotto **[!UICONTROL Seleziona una classe base per questo schema]**.

1. Seleziona **[!UICONTROL Avanti]**.

   ![Classe base della Creazione guidata schemi](assets/schema-wizard-base-class.png){zoomable="yes"}

1. Nel passaggio **[!UICONTROL Nome e revisione]** della procedura guidata **[!UICONTROL Crea schema]**, immettere un **[!UICONTROL Nome visualizzato dello schema]**, ad esempio `Luma Mobile Event Schema` e una [!UICONTROL Descrizione], ad esempio `Schema for Luma mobile app experience events`.

   >[!NOTE]
   >
   >Se segui questa esercitazione con più persone su una singola sandbox o se utilizzi un account condiviso, puoi aggiungere o anteporre un’identificazione come parte delle convenzioni di denominazione. Ad esempio, anziché `Luma Mobile App Event Schema`, utilizza `Luma Mobile App Event Schema - Joe Smith`. Vedi anche la nota in [Panoramica](overview.md).

1. Seleziona **[!UICONTROL Fine]** per completare la procedura guidata.

   ![Nome e revisione dello schema](assets/schema-wizard-name-and-review.png){zoomable="yes"}


1. Seleziona ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Aggiungi** accanto a **[!UICONTROL Gruppi di campi]**.

   ![Aggiungere un gruppo di campi](assets/add-field-group.png){zoomable="yes"}

1. Cerca `Consumer Experience Event`.

1. Seleziona ![Anteprima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Preview_18_N.svg) per visualizzare in anteprima i campi e/o leggere la descrizione per ulteriori dettagli prima di selezionare un gruppo di campi.

1. Seleziona **Evento esperienza del consumatore**.

1. Seleziona **[!UICONTROL Aggiungi gruppi di campi]**.

   ![Selezione del gruppo di campi](assets/schema-select-field-groups.png){zoomable="yes"}

   Viene visualizzata di nuovo la schermata principale di composizione dello schema, in cui puoi visualizzare tutti i campi disponibili.

1. Seleziona **[!UICONTROL Salva]**.
1. Seleziona ![Schemi](/help/assets/icons/Schemas.svg) **[!UICONTROL Schemi]** in **[!UICONTROL Gestione dati]** per tornare all&#39;interfaccia principale **[!UICONTROL Schemi]**.

>[!NOTE]
>
>Non è necessario utilizzare tutti i campi di un gruppo. Puoi anche rimuovere i campi per mantenere lo schema conciso e comprensibile. Se è utile, puoi considerare uno schema come un livello dati vuoto. Nell’app, puoi popolare i valori pertinenti al momento giusto.

Il gruppo di campi [!UICONTROL Evento esperienza del consumatore] include un tipo di dati denominato [!UICONTROL Informazioni Web], che descrive eventi quali la visualizzazione della pagina e i clic sui collegamenti. Al momento della stesura di questo articolo, non esiste una parità di app mobile con questa funzione, quindi intendi crearne una tua.

## Creare un tipo di dati personalizzato


Per iniziare, crea un tipo di dati personalizzato che descrive i due eventi:

* Visualizzazione a schermo
* Interazione app

1. Selezionare la scheda **[!UICONTROL Tipi di dati]**.

1. Selezionare **[!UICONTROL Crea tipo di dati]**.

   ![Selezione del menu del tipo di dati](assets/schema-datatype-create.png){zoomable="yes"}

1. Fornisci un **[!UICONTROL Nome visualizzato]** e una **[!UICONTROL Descrizione]**, ad esempio `App Information` e `Custom data type describing "Screen Views" & "App Actions"`

   ![Nome e descrizione](assets/schema-datatype-name.png){zoomable="yes"}

   >[!TIP]
   >
   > Utilizza sempre [!UICONTROL nomi visualizzati] leggibili e descrittivi per i campi personalizzati. Questa pratica rende i campi personalizzati più accessibili agli esperti di marketing quando compaiono in servizi a valle come il Generatore di segmenti.


1. Per aggiungere un campo, selezionare il pulsante ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg).


1. Questo campo è un oggetto contenitore per l&#39;interazione con l&#39;app. Fornisci un **[!UICONTROL Nome campo]** `appInteraction`, **[!UICONTROL Nome visualizzato]** `App Interaction` e seleziona `Object` dall&#39;elenco **[!UICONTROL Tipo]**.

1. Seleziona **[!UICONTROL Applica]**.

   ![Aggiunta di un nuovo evento azione app](assets/schema-datatype-app-action.png){zoomable="yes"}

1. Per misurare la frequenza di un&#39;azione, aggiungere un campo selezionando il pulsante ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto all&#39;oggetto **[!UICONTROL appInteraction]** creato.

1. Assegna al campo un **[!UICONTROL Nome campo]** `appAction`, **[!UICONTROL Nome visualizzato]** di `App Action` e **[!UICONTROL Tipo]** `Measure`.

   Questo passaggio sarebbe l’equivalente di un evento di successo in Adobe Analytics.

1. Seleziona **[!UICONTROL Applica]**.

   ![Aggiunta campo nome azione](assets/schema-datatype-action-name.png){zoomable="yes"}

1. Aggiungi un campo che descrive il tipo di interazione selezionando il pulsante ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto all&#39;oggetto **[!UICONTROL appInteraction]**.

1. Assegnagli un **[!UICONTROL Nome campo]** `name`, **[!UICONTROL Nome visualizzato]** di `Name` e **[!UICONTROL Tipo]** `String`.

   Questo passaggio è l’equivalente di una dimensione in Adobe Analytics.

   ![Selezione dell&#39;applicazione](assets/schema-datatype-apply.png){zoomable="yes"}

1. Scorri fino alla parte inferiore della barra a destra e seleziona **[!UICONTROL Applica]**.

1. Per creare un oggetto `appStateDetails` contenente un campo **[!UICONTROL Measure]** denominato `screenView` e due campi **[!UICONTROL String]** denominati `screenName` e `screenType`, eseguire la stessa procedura utilizzata per la creazione dell&#39;oggetto **[!UICONTROL appInteraction]**.

1. Seleziona **[!UICONTROL Salva]**.

   ![Stato finale del tipo di dati](assets/schema-datatype-final.png){zoomable="yes"}

## Aggiungere un gruppo di campi personalizzato

Ora, aggiungi un gruppo di campi personalizzato utilizzando il tipo di dati personalizzato:

1. Apri lo schema creato in precedenza in questa lezione.

1. Seleziona ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]**.

   ![Aggiunta di un nuovo gruppo di campi](assets/schema-fieldgroup-add.png){zoomable="yes"}

1. Seleziona **[!UICONTROL Crea nuovo gruppo di campi]**.

1. Fornisci un **[!UICONTROL Nome visualizzato]** e una **[!UICONTROL Descrizione]**, ad esempio `App Interactions` e `Fields for app interactions`.

1. Seleziona **Aggiungi gruppi di campi**.

   ![Nome e descrizione](assets/schema-fieldgroup-name.png){zoomable="yes"}

1. Dalla schermata di composizione principale, seleziona **[!UICONTROL Interazioni app**].

1. Aggiungi un campo alla radice dello schema selezionando il pulsante ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto al nome dello schema.

1. Nella barra a destra, fornisci un **[!UICONTROL Nome campo]** di `appInformation`, un **[!UICONTROL Nome visualizzato]** di `App Information` e un **[!UICONTROL Tipo]** di `App Information`.

1. Seleziona **[!UICONTROL Interazioni app]** dal menu a discesa **[!UICONTROL Gruppo di campi]**, per assegnare i campi al nuovo gruppo di campi.

1. Seleziona **[!UICONTROL Applica]**.

1. Seleziona **[!UICONTROL Salva]**.

   ![Selezione dell&#39;applicazione](assets/schema-fieldgroup-apply.png){zoomable="yes"}

>[!NOTE]
>
>I gruppi di campi personalizzati si trovano sempre sotto l’identificatore dell’organizzazione Experience Cloud.


>[!SUCCESS]
>
>Ora disponi di uno schema da utilizzare per il resto dell’esercitazione.
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=it).

Successivo: **[Crea un [!UICONTROL flusso di dati]](create-datastream.md)**
