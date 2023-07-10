---
title: Creare uno schema XDM
description: Scopri come creare uno schema XDM per gli eventi delle app mobili.
feature: Mobile SDK,Schemas
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 4%

---

# Creare uno schema XDM

Scopri come creare uno schema XDM per gli eventi delle app mobili.

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

## Cosa sono gli schemi XDM?

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni che consentono a qualsiasi applicazione di comunicare con i servizi di Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e quindi ottenere valore dai dati.

Prima di poter acquisire i dati in Platform, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli al tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema.

Per ulteriori informazioni sul modello di composizione dello schema, inclusi i principi di progettazione e le best practice, vedi [nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it) o il corso [Modellare i dati sull’esperienza del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=it).

>[!TIP]
>
>Se conosci Analytics Solution Design Reference (SDR), puoi considerare uno schema come un SDR più affidabile.

## Prerequisiti

Per completare la lezione, è necessario disporre dell&#39;autorizzazione per la creazione di uno schema di Experience Platform.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Creare uno schema nell’interfaccia di Data Collection
* Aggiungere un gruppo di campi standard allo schema
* Creare e aggiungere un gruppo di campi personalizzato allo schema

## Passare agli schemi

1. Accedi ad Adobe Experience Cloud.

1. Apri il commutatore di app, quindi seleziona **[!UICONTROL Raccolta dati]**

   ![Menu a discesa 3x3](assets/mobile-schema-navigate1.png)

1. Assicurati di trovarti nella sandbox di Experience Platform che stai utilizzando per questa esercitazione.

   >[!NOTE]
   >
   > Per questa esercitazione, i clienti di applicazioni basate su Platform come Real-Time CDP devono utilizzare una sandbox di sviluppo. Gli altri clienti utilizzeranno la sandbox di produzione predefinita.


1. Seleziona **[!UICONTROL Schemi]** in **[!UICONTROL Gestione dati]**.

   ![tag nella schermata iniziale](assets/mobile-schema-navigate3.png)

Ora ti trovi nella pagina degli schemi principali e viene visualizzato un elenco degli schemi esistenti. Puoi anche visualizzare le schede corrispondenti ai blocchi predefiniti principali di uno schema:

* **Gruppi di campi** sono componenti riutilizzabili che definiscono uno o più campi per acquisire dati specifici, ad esempio dati personali, preferenze di hotel o indirizzi.
* **Classi** definisci gli aspetti comportamentali dei dati contenuti nello schema. Ad esempio: `XDM ExperienceEvent` acquisisce serie temporali, dati evento e `XDM Individual Profile` acquisisce i dati attributo relativi a un individuo.
* **Tipi di dati** vengono utilizzati come tipi di campi di riferimento nelle classi o nei gruppi di campi allo stesso modo dei campi letterali di base.

Le descrizioni di cui sopra rappresentano una panoramica di alto livello. Per ulteriori dettagli, vedi [Elementi di base dello schema](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schema-building-blocks.html?lang=it) video o lettura [Nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it) nella documentazione del prodotto.

In questa esercitazione utilizzi il gruppo di campi Evento esperienza del consumatore e creane uno personalizzato per illustrare il processo.

>[!NOTE]
>
>Adobe continua ad aggiungere altri gruppi di campi standard che devono essere utilizzati quando possibile, in quanto questi campi sono implicitamente compresi dai servizi Experience Platform e forniscono maggiore coerenza quando vengono utilizzati tra i componenti Platform. L’utilizzo di gruppi di campi standard offre vantaggi tangibili, come la mappatura automatica nelle funzioni di Analytics e AI in Platform.

## Architettura dello schema dell’app Luma

In uno scenario reale, il processo di progettazione dello schema potrebbe essere simile al seguente:

* Raccogliere i requisiti aziendali.
* Trova gruppi di campi predefiniti per soddisfare il maggior numero possibile di requisiti.
* Crea gruppi di campi personalizzati per eventuali spazi.

A scopo di apprendimento, utilizzerai gruppi di campi predefiniti e personalizzati.

* **Evento esperienza del consumatore**: gruppo di campi predefinito con molti campi comuni.
* **Informazioni app**: gruppo di campi personalizzato progettato per simulare i concetti di TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Creare uno schema

1. Seleziona **[!UICONTROL Crea schema]** per visualizzare il menu a discesa delle opzioni, seleziona **[!UICONTROL XDM ExperienceEvent]**.

   ![Selezione di ExperienceEvent dal menu a discesa](assets/mobile-schema-create.png)

1. Cerca `Consumer Experience Event`.

1. Puoi visualizzare in anteprima i campi e/o leggere la descrizione per ulteriori dettagli prima di selezionare.

1. Seleziona la casella di controllo e quindi **[!UICONTROL Aggiungi gruppi di campi]**.

   ![Selezione del gruppo di campi](assets/mobile-schema-select-field-groups.png)

   Viene visualizzata di nuovo la schermata principale di composizione dello schema, in cui puoi visualizzare tutti i campi disponibili.

1. Assegna un nome allo schema selezionando **[!UICONTROL Schema senza titolo]** dall&#39;alto a sinistra e quindi fornendo un **[!UICONTROL Nome visualizzato]** E **[!UICONTROL Descrizione]**, ad esempio `Luma Tutorial Mobile` e `"Luma App" schema for Adobe Tutorial`

1. Seleziona **[!UICONTROL Salva]**.

   ![Selezione dell&#39;opzione Applica](assets/mobile-schema-name-save.png)

>[!NOTE]
>
>Non è necessario utilizzare tutti i campi di un gruppo. Se è utile, puoi considerare uno schema come un livello dati vuoto. Nell’app, puoi popolare i valori pertinenti al momento giusto.
>
>Il `Consumer Experience Event` ha un tipo di dati denominato `Web information`, che descrive eventi come la visualizzazione della pagina e i clic sui collegamenti. Al momento della stesura di questo articolo, non esiste una parità di app mobile con questa funzione, quindi intendi crearne una tua.

## Creare un tipo di dati personalizzato

Per iniziare, crea un tipo di dati personalizzato che descrive i due eventi:

* Visualizzazione a schermo
* Interazione app

1. Seleziona la **[!UICONTROL Tipi di dati]** , quindi seleziona **[!UICONTROL Crea tipo di dati]**.

   ![Selezione del menu del tipo di dati](assets/mobile-schema-datatype-create.png)

1. Assegna un **[!UICONTROL Nome visualizzato]** e **[!UICONTROL Descrizione]**, ad esempio `App Information` e `Custom data type describing "Screen Views" & "App Actions"`

   ![Nome e descrizione](assets/mobile-schema-datatype-name.png)

   >[!TIP]
   >
   > Usa sempre testo leggibile e descrittivo [!UICONTROL nomi visualizzati] per i campi personalizzati, in quanto questa procedura li rende più accessibili agli esperti di marketing quando i campi vengono visualizzati in servizi a valle come il Generatore di segmenti.


1. Per aggiungere un campo, selezionare il pulsante (+).

   Questo campo è un oggetto contenitore per l’interazione con l’app. Dagli una scatola di cammello **[!UICONTROL Nome campo]** `appInteraction`, **[!UICONTROL nome visualizzato]** `App Interaction`, e **[!UICONTROL tipo]** `Object`.

1. Seleziona **[!UICONTROL Applica]**.

   ![Aggiunta di un nuovo evento azione app](assets/mobile-schema-datatype-app-action.png)

1. Per misurare la frequenza di un’azione, aggiungi un campo facendo clic sul pulsante (+) accanto al `appInteraction` oggetto creato.

1. Dagli una scatola di cammello **[!UICONTROL Nome campo]** `appAction`, **[!UICONTROL nome visualizzato]** di `App Action` e **[!UICONTROL tipo]** `Measure`.

   Questo passaggio sarebbe l’equivalente di un evento di successo in Adobe Analytics.

1. Seleziona **[!UICONTROL Applica]**.

   ![Aggiunta del campo nome azione](assets/mobile-schema-datatype-action-name.png)

1. Aggiungi un campo che descrive il tipo di interazione selezionando il pulsante (+) accanto al `appInteraction` oggetto.

1. Assegna un **[!UICONTROL Nome campo]** `name`, **[!UICONTROL nome visualizzato]** di `Name` e **[!UICONTROL tipo]** `String`.

   Questo passaggio è l’equivalente di una dimensione in Adobe Analytics.

   ![Selezione dell&#39;opzione Applica](assets/mobile-schema-datatype-apply.png)

1. Scorri fino alla parte inferiore della barra a destra e seleziona **[!UICONTROL Applica]**.

1. Seguire lo stesso pattern per creare un `appStateDetails` oggetto contenente un campo Measure denominato `screenView` e due stringhe denominate `screenName` e `screenType`.

1. Seleziona **[!UICONTROL Salva]**.

   ![Stato finale del tipo di dati](assets/mobile-schema-datatype-final.png)

## Aggiungere un gruppo di campi personalizzato

Ora aggiungi un gruppo di campi personalizzato utilizzando il tipo di dati personalizzato:

1. Apri lo schema creato in precedenza in questa lezione.

1. Seleziona **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]**.

   ![Aggiunta di un nuovo gruppo di campi](assets/mobile-schema-fieldgroup-add.png)

1. Questa volta puoi creare un gruppo di campi personalizzato selezionando l’ **[!UICONTROL Crea nuovo gruppo di campi]** nella parte superiore, quindi fornisci un nome e una descrizione, ad esempio `App Interactions` e `Fields for app interactions`.

   ![Nome e descrizione](assets/mobile-schema-fieldgroup-name.png)

1. Dalla schermata di composizione principale, aggiungi un campo alla directory principale dello schema.

1. Seleziona (+) accanto al nome dello schema.

1. Nella barra a destra, specifica **[!UICONTROL Nome campo]** di `appInformation`, un nome visualizzato di `App Information`.

1. Seleziona `App Information` dal **[!UICONTROL Tipo]** , il tipo di dati creato nell&#39;esercizio precedente.

1. Seleziona **[!UICONTROL Applica]**.

   ![Selezione dell&#39;opzione Applica](assets/mobile-schema-fieldgroup-apply.png)

>[!NOTE]
>
>I gruppi di campi personalizzati si trovano sempre sotto l’identificatore dell’organizzazione di Experience Cloud.
>
>`_techmarketingdemos` viene sostituito con il valore univoco della tua organizzazione.

Ora disponi di uno schema da utilizzare per il resto dell’esercitazione.

Successivo: **[Creare un [!UICONTROL flusso di dati]](create-datastream.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)