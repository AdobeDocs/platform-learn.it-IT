---
title: Creare uno schema XDM
description: Scopri come creare uno schema XDM per gli eventi delle app mobili.
feature: Mobile SDK,Schemas
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 5%

---

# Creare uno schema XDM

Scopri come creare uno schema XDM per gli eventi delle app mobili.

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

## Cosa sono gli schemi XDM?

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni che consentono a qualsiasi applicazione di comunicare con i servizi di Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più veloce e integrato. Ottieni informazioni preziose dalle azioni dei clienti, definisci i tipi di pubblico dei clienti attraverso i segmenti e utilizzi gli attributi del cliente a scopo di personalizzazione.

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedere [nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it) o il corso [Modellare i dati sull’esperienza del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=it).

>[!TIP]
>
>Se conosci Analytics Solution Design Reference (SDR), puoi considerare uno schema come un SDR più affidabile. Consulta [Creare e gestire un documento Solution Design Reference (SDR)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html?lang=it) per ulteriori informazioni.

## Prerequisiti

Per completare la lezione, è necessario disporre dell&#39;autorizzazione per la creazione di uno schema di Experience Platform.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Creare uno schema nell’interfaccia di Data Collection
* Aggiungere un gruppo di campi standard allo schema
* Creare e aggiungere un gruppo di campi personalizzato allo schema

## Passare agli schemi

1. Accedi a Adobe Experience Cloud.

1. Assicurati di trovarti nella sandbox di Experience Platform che stai utilizzando per questa esercitazione.

1. Apri il commutatore app ![Commutatore app](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg)  (in alto a destra)

1. Seleziona **[!UICONTROL Raccolta dati]** dal menu.

   ![Accedi all’Experience Cloud](assets/experiencecloud-login.png)

   >[!NOTE]
   >
   > Per questa esercitazione, i clienti di applicazioni basate su Platform come Real-Time CDP devono utilizzare una sandbox di sviluppo. Altri clienti utilizzano la sandbox di produzione predefinita.


1. Seleziona **[!UICONTROL Schemi]** in **[!UICONTROL Gestione dati]** nella barra a sinistra.

   ![tag nella schermata iniziale](assets/mobile-schema-navigate.png)

Ora ti trovi nella pagina degli schemi principali e viene visualizzato un elenco degli schemi esistenti. Puoi anche visualizzare le schede corrispondenti ai blocchi predefiniti principali di uno schema:

* **Gruppi di campi** sono componenti riutilizzabili che definiscono uno o più campi per acquisire dati specifici, ad esempio dati personali, preferenze di hotel o indirizzi.
* **Classi** definisci gli aspetti comportamentali dei dati contenuti nello schema. Ad esempio: `XDM ExperienceEvent` acquisisce serie temporali, dati evento e `XDM Individual Profile` acquisisce i dati attributo relativi a un individuo.
* **Tipi di dati** vengono utilizzati come tipi di campi di riferimento nelle classi o nei gruppi di campi allo stesso modo dei campi letterali di base.

Le descrizioni di cui sopra rappresentano una panoramica di alto livello. Per ulteriori dettagli, vedi [Elementi di base dello schema](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schema-building-blocks.html?lang=it) video o lettura [Nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it) nella documentazione del prodotto.

In questa esercitazione utilizzi il gruppo di campi Evento esperienza del consumatore e creane uno personalizzato per illustrare il processo.

>[!NOTE]
>
>Adobe continua ad aggiungere altri gruppi di campi standard che devono essere utilizzati quando possibile, in quanto questi campi sono implicitamente compresi dai servizi Experienci Platform e forniscono maggiore coerenza quando vengono utilizzati tra i componenti Platform. L’utilizzo di gruppi di campi standard offre vantaggi tangibili, come la mappatura automatica nelle funzioni di Analytics e AI in Platform.

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

1. Seleziona **[!UICONTROL Crea schema]**.

1. Seleziona **[!UICONTROL XDM ExperienceEvent]** dal menu.

   ![Selezione di ExperienceEvent dal menu a discesa](assets/schema-create.png)

1. Seleziona ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Aggiungi** accanto a **[!UICONTROL Gruppi di campi]**.

   ![Aggiungere un gruppo di campi](assets/add-field-group.png)

1. Cerca `Consumer Experience Event`.

1. Seleziona ![Anteprima](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Preview_18_N.svg) per visualizzare in anteprima i campi e/o leggere la descrizione per ulteriori dettagli prima di selezionare un gruppo di campi.

1. Seleziona **Evento esperienza del consumatore**.

1. Seleziona **[!UICONTROL Aggiungi gruppi di campi]**.

   ![Selezione del gruppo di campi](assets/schema-select-field-groups.png)

   Viene visualizzata di nuovo la schermata principale di composizione dello schema, in cui puoi visualizzare tutti i campi disponibili.

1. Assegna un nome allo schema selezionando **[!UICONTROL Schema senza titolo]** dal **[!UICONTROL Composizione]** riquadro (sotto **[!UICONTROL Schema]**) e fornendo un **[!UICONTROL Nome visualizzato]** E **[!UICONTROL Descrizione]**, ad esempio `Luma Mobile App Event Schema` e `Schema for Luma mobile app experience events.`

   >[!NOTE]
   >
   >Se segui questa esercitazione con più persone su una singola sandbox o se utilizzi un account condiviso, puoi aggiungere o anteporre un’identificazione come parte delle convenzioni di denominazione. Ad esempio, usa `Luma Mobile App Event Schema - Joe Smith` invece di `Luma Mobile App Event Schema`. Vedi anche la nota in [Panoramica](overview.md).


1. Seleziona **[!UICONTROL Salva]**.

   ![Selezione dell&#39;opzione Applica](assets/schema-name-save.png)

>[!NOTE]
>
>Non è necessario utilizzare tutti i campi di un gruppo. Puoi anche rimuovere i campi se questo consente di mantenere lo schema conciso e comprensibile. Se è utile, puoi considerare uno schema come un livello dati vuoto. Nell’app, puoi popolare i valori pertinenti al momento giusto.

Il [!UICONTROL Evento esperienza del consumatore] il gruppo di campi ha un tipo di dati denominato [!UICONTROL Informazioni web], che descrive eventi come la visualizzazione della pagina e i clic sui collegamenti. Al momento della stesura di questo articolo, non esiste una parità di app mobile con questa funzione, quindi intendi crearne una tua.

## Creare un tipo di dati personalizzato

Per iniziare, crea un tipo di dati personalizzato che descrive i due eventi:

* Visualizzazione a schermo
* Interazione app

1. Seleziona la **[!UICONTROL Tipi di dati]** scheda.

1. Seleziona **[!UICONTROL Crea tipo di dati]**.

   ![Selezione del menu del tipo di dati](assets/schema-datatype-create.png)

1. Fornisci un **[!UICONTROL Nome visualizzato]** e **[!UICONTROL Descrizione]**, ad esempio `App Information` e `Custom data type describing "Screen Views" & "App Actions"`

   ![Nome e descrizione](assets/schema-datatype-name.png)

   >[!TIP]
   >
   > Usa sempre testo leggibile e descrittivo [!UICONTROL nomi visualizzati] per i campi personalizzati, in quanto questa procedura li rende più accessibili agli esperti di marketing quando i campi vengono visualizzati in servizi a valle come il Generatore di segmenti.


1. Per aggiungere un campo, seleziona la ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) pulsante.


1. Questo campo è un oggetto contenitore per l’interazione dell’app. , quindi fornisci una notazione camel **[!UICONTROL Nome campo]** `appInteraction`, **[!UICONTROL Nome visualizzato]** `App Interaction`, e seleziona `Object` dal **[!UICONTROL Tipo]** elenco.

1. Seleziona **[!UICONTROL Applica]**.

   ![Aggiunta di un nuovo evento azione app](assets/schema-datatype-app-action.png)

1. Per misurare la frequenza di un’azione, aggiungi un campo selezionando la ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto al pulsante **[!UICONTROL appInteraction]** oggetto creato.

1. Dagli una scatola di cammello **[!UICONTROL Nome campo]** `appAction`, **[!UICONTROL Nome visualizzato]** di `App Action` e **[!UICONTROL Tipo]** `Measure`.

   Questo passaggio sarebbe l’equivalente di un evento di successo in Adobe Analytics.

1. Seleziona **[!UICONTROL Applica]**.

   ![Aggiunta del campo nome azione](assets/schema-datatype-action-name.png)

1. Aggiungi un campo che descrive il tipo di interazione selezionando la ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto al pulsante **[!UICONTROL appInteraction]** oggetto.

1. Assegna un **[!UICONTROL Nome campo]** `name`, **[!UICONTROL Nome visualizzato]** di `Name` e **[!UICONTROL Tipo]** `String`.

   Questo passaggio è l’equivalente di una dimensione in Adobe Analytics.

   ![Selezione dell&#39;opzione Applica](assets/schema-datatype-apply.png)

1. Scorri fino alla parte inferiore della barra a destra e seleziona **[!UICONTROL Applica]**.

1. Per creare un `appStateDetails` oggetto contenente un **[!UICONTROL Misura]** campo denominato `screenView` e due **[!UICONTROL Stringa]** campi denominati `screenName` e `screenType`, segui gli stessi passaggi eseguiti durante la creazione del **[!UICONTROL appInteraction]** oggetto.

1. Seleziona **[!UICONTROL Salva]**.

   ![Stato finale del tipo di dati](assets/schema-datatype-final.png)

## Aggiungere un gruppo di campi personalizzato

Ora aggiungi un gruppo di campi personalizzato utilizzando il tipo di dati personalizzato:

1. Apri lo schema creato in precedenza in questa lezione.

1. Seleziona ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]**.

   ![Aggiunta di un nuovo gruppo di campi](assets/schema-fieldgroup-add.png)

1. Seleziona **[!UICONTROL Crea nuovo gruppo di campi]**.

1. Fornisci un **[!UICONTROL Nome visualizzato]** e **[!UICONTROL Descrizione]** ad esempio: `App Interactions` e `Fields for app interactions`.

1. Seleziona **Aggiungi gruppi di campi**.

   ![Nome e descrizione](assets/schema-fieldgroup-name.png)

1. Dalla schermata principale della composizione, selezionate **[!UICONTROL Interazioni app**].

1. Aggiungi un campo alla radice dello schema selezionando la ![Più](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto al nome dello schema.

1. Nella barra a destra, specifica **[!UICONTROL Nome campo]** di `appInformation`, a **[!UICONTROL Nome visualizzato]** di `App Information`, e un **[!UICONTROL Tipo]** di `App Information`.

1. Seleziona **[!UICONTROL Interazioni app]** dal **[!UICONTROL Gruppo di campi]** , per assegnare i campi al nuovo gruppo di campi.

1. Seleziona **[!UICONTROL Applica]**.

1. Seleziona **[!UICONTROL Salva]**.

   ![Selezione dell&#39;opzione Applica](assets/schema-fieldgroup-apply.png)

>[!NOTE]
>
>I gruppi di campi personalizzati si trovano sempre sotto l’identificatore dell’organizzazione di Experience Cloud.


>[!SUCCESS]
>
>Ora disponi di uno schema da utilizzare per il resto dell’esercitazione.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Creare un [!UICONTROL flusso di dati]](create-datastream.md)**
