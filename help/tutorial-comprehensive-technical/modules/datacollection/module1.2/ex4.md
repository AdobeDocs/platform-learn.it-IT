---
title: Foundation - Acquisizione dei dati - Acquisizione dei dati da origini offline
description: Foundation - Acquisizione dei dati - Acquisizione dei dati da origini offline
kt: 5342
doc-type: tutorial
exl-id: a4909a47-0652-453b-ae65-ba4c261f087c
source-git-commit: ef26abbeb0c1076adbada57f0f18f11c7634d022
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 5%

---

# 1.2.4 Acquisizione dei dati da origini offline

In questo esercizio, l’obiettivo è quello di integrare dati esterni come i dati CRM in Platform.

## Finalità di apprendimento

- Scopri come generare i dati di test
- Scopri come acquisire CSV
- Scopri come utilizzare l’interfaccia utente web per l’acquisizione dei dati tramite flussi di lavoro
- Comprendere le funzioni di governance dei dati di Experience Platform

## Risorse

- Mockaroo: [https://www.mockaroo.com/](https://www.mockaroo.com/)
- Adobe Experience Platform: [https://experience.adobe.com/platform/](https://experience.adobe.com/platform/)

## Attività

- Crea un file CSV con dati dimostrativi. Acquisisci il file CSV in Adobe Experience Platform utilizzando i flussi di lavoro disponibili.
- Comprendere le opzioni di governance dei dati in Adobe Experience Platform

## Creare un set di dati di gestione delle relazioni con i clienti utilizzando uno strumento per la generazione dei dati

Per questo esercizio, sono necessarie 1000 righe di esempio di dati CRM.

Apri il modello Mockaroo da [https://www.mockaroo.com/12674210](https://www.mockaroo.com/12674210).

![Acquisizione dei dati](./images/mockaroo.png)

Nel modello, noterai i seguenti campi:

- id
- nome
- cognome
- e-mail
- genere
- bornDate
- home_latitude
- home_longitude
- country_code
- città
- paese
- crmId
- consent.email
- consent.commercialEmail
- consent.any

Tutti questi campi sono stati definiti per produrre dati compatibili con Platform.

Per generare il file CSV, fai clic sul pulsante **[!UICONTROL Genera dati]** per creare e scaricare un file CSV con 1000 righe di dati dimostrativi.

![Acquisizione dei dati](./images/dd.png)

Apri il file CSV per visualizzarne il contenuto.

![Acquisizione dei dati](./images/excel.png)

Quando il file CSV è pronto, puoi procedere con l’acquisizione in AEP.

### Verificare il set di dati

Vai a [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare una **[!UICONTROL sandbox]**. La sandbox da selezionare è denominata ``--aepSandboxName--``.

![Acquisizione dei dati](./images/sb1.png)

In Adobe Experience Platform, fai clic su **[!UICONTROL Set di dati]** nel menu sul lato sinistro dello schermo.

![Acquisizione dei dati](./images/menudatasetssb.png)

Utilizzerai un set di dati condiviso. Il set di dati condiviso è già stato creato ed è denominato **[!UICONTROL Sistema demo - Set di dati profilo per CRM (Global v1.1)]**. Fai clic su di esso per aprirlo.

![Acquisizione dei dati](./images/emeacrmoverview.png)

Nella schermata di panoramica puoi visualizzare 3 informazioni principali.

>[!NOTE]
>
>È possibile che la visualizzazione del set di dati sia vuota, se non si è verificata alcuna attività negli ultimi 7 giorni.

![Acquisizione dei dati](./images/dashboard.png)

Innanzitutto, il dashboard [!UICONTROL Attività set di dati] mostra il numero totale di record CRM nel set di dati, i batch acquisiti e il relativo stato

![Acquisizione dei dati](./images/batchids.png)

In secondo luogo, scorrendo la pagina, puoi verificare quando sono stati acquisiti i batch di dati, quanti record sono stati caricati e anche se il batch è stato caricato correttamente o meno. L&#39;**[!UICONTROL ID batch]** è l&#39;identificatore di un processo batch specifico e l&#39;**[!UICONTROL ID batch]** è importante in quanto può essere utilizzato per la risoluzione dei problemi relativi al mancato avvio di un batch specifico.

Infine, la scheda di informazioni del [!UICONTROL Set di dati] mostra informazioni importanti come [!UICONTROL ID set di dati] (importante anche in questo caso dal punto di vista della risoluzione dei problemi), il nome del set di dati e se il set di dati è stato abilitato per il profilo.

![Acquisizione dei dati](./images/datasetsettings.png)

L’impostazione più importante è il collegamento tra il set di dati e lo schema. Lo schema definisce quali dati possono essere acquisiti e come dovrebbero apparire.

In questo caso, viene utilizzato lo schema di profilo **[!UICONTROL Sistema demo per CRM (Global v1.1)]**, mappato alla classe di **[!UICONTROL Profilo]** e con estensioni implementate, dette anche gruppi di campi.

![Acquisizione dei dati](./images/ds_schemalink.png)

Facendo clic sul nome dello schema, si passa alla panoramica dello [!UICONTROL schema] in cui è possibile visualizzare tutti i campi attivati per questo schema.

![Acquisizione dei dati](./images/schemads.png)

Ogni schema deve avere un descrittore primario personalizzato definito. Nel caso del set di dati CRM, lo schema ha definito che il campo **[!UICONTROL crmId]** deve essere l&#39;identificatore primario. Se desideri creare uno schema e collegarlo al [!UICONTROL Profilo cliente in tempo reale], devi definire un [!UICONTROL Gruppo di campi] personalizzato che faccia riferimento al descrittore principale.

Puoi anche vedere che la nostra identità primaria si trova in `--aepTenantId--.identification.core.crmId`, collegata allo [!UICONTROL spazio dei nomi] di **[!UICONTROL sistema demo - CRMID]**.

![Acquisizione dei dati](./images/schema_descriptor.png)

Ogni schema e, di conseguenza, ogni set di dati da utilizzare nel [!UICONTROL Profilo cliente in tempo reale] deve avere un [!UICONTROL Identificatore primario]. Questo [!UICONTROL identificatore primario] è l&#39;identificatore utente per marchio di un cliente in quel set di dati. Nel caso di un set di dati CRM potrebbe essere l’indirizzo e-mail o l’ID del sistema di gestione delle relazioni con i clienti; nel caso di un set di dati Call Center potrebbe essere il numero di cellulare di un cliente.

È consigliabile creare uno schema separato e specifico per ogni set di dati e impostare il descrittore per ogni set di dati in modo che corrisponda al funzionamento delle soluzioni correnti utilizzate dal brand.

### Utilizzo di un flusso di lavoro per mappare un file CSV a uno schema XDM

L’obiettivo di questo esercizio è integrare i dati CRM in AEP. Tutti i dati acquisiti in Platform devono essere mappati sullo schema XDM specifico. Attualmente disponi di un set di dati CSV con 1000 righe da un lato e un set di dati collegato a uno schema dall’altro. Per caricare il file CSV in tale set di dati, è necessario eseguire una mappatura. Per facilitare questo esercizio di mappatura, sono disponibili **[!UICONTROL Flussi di lavoro]** in Adobe Experience Platform.

Fai clic su **[!UICONTROL Mappa CSV a schema XDM]**, quindi fai clic su **[!UICONTROL Avvia]** per avviare il processo.

![Acquisizione dei dati](./images/workflows.png)

Nella schermata successiva, devi selezionare un set di dati in cui acquisire il file. Puoi scegliere se selezionare un set di dati già esistente o crearne uno nuovo. Per questo esercizio ne riutilizzeremo uno esistente: seleziona **[!UICONTROL Sistema demo - Set di dati profilo per CRM (Global v1.1)]** come indicato di seguito e lascia le altre impostazioni predefinite.

Fai clic su **Avanti**.

![Acquisizione dei dati](./images/datasetselection.png)

Trascina e rilascia il file CSV o fai clic su **[!UICONTROL Scegli i file]**, passa al desktop del computer e seleziona il file CSV.

![Acquisizione dei dati](./images/dragdrop.png)

Dopo aver selezionato il file CSV, verrà caricato immediatamente e visualizzerai un’anteprima del file in pochi secondi.

Fai clic su **Avanti**.

![Acquisizione dei dati](./images/previewcsv.png)

Ora devi mappare le intestazioni di colonna dal file CSV con una proprietà XDM nel **[!UICONTROL sistema di dimostrazione - set di dati profilo per CRM]**.

Adobe Experience Platform ha già fatto alcune proposte per te, tentando di collegare [!UICONTROL Attributi Source] con i [!UICONTROL Campi schema di destinazione].

>[!NOTE]
>
>Se noti degli errori nella schermata di mappatura, non preoccuparti. Dopo aver seguito le istruzioni riportate di seguito, tali errori verranno risolti.

![Acquisizione dei dati](./images/mapschema.png)

Per le [!UICONTROL mappature schema], Adobe Experience Platform ha già tentato di collegare i campi. Tuttavia, non tutte le proposte di mappatura sono corrette. È ora necessario aggiornare i **campi di destinazione** uno alla volta.

#### bornDate

Il campo schema Source **dataDiNascita** deve essere collegato al campo di destinazione **person.dataDiNascita**.

![Acquisizione dei dati](./images/tfbd.png)

#### città

Il campo schema Source **city** deve essere collegato al campo di destinazione **homeAddress.city**.

![Acquisizione dei dati](./images/tfcity.png)

#### paese

Il campo schema Source **country** deve essere collegato al campo di destinazione **homeAddress.country**.

![Acquisizione dei dati](./images/tfcountry.png)

#### country_code

Il campo schema Source **country_code** deve essere collegato al campo di destinazione **homeAddress.countryCode**.

![Acquisizione dei dati](./images/tfcountrycode.png)

#### e-mail

Il campo schema Source **email** deve essere collegato al campo di destinazione **personalEmail.address**.

![Acquisizione dei dati](./images/tfemail.png)

#### crmid

Il campo schema Source **crmid** deve essere collegato al campo di destinazione **`--aepTenantId--`.identifier.core.crmId**.

![Acquisizione dei dati](./images/tfemail1.png)

#### nome

Il campo schema Source **first_name** deve essere collegato al campo di destinazione **person.name.firstName**.

![Acquisizione dei dati](./images/tffname.png)

#### genere

Il campo schema Source **gender** deve essere collegato al campo di destinazione **person.gender**.

![Acquisizione dei dati](./images/tfgender.png)

#### home_latitude

Il campo schema Source **home_latitude** deve essere collegato al campo di destinazione **homeAddress._schema.latitude**.

![Acquisizione dei dati](./images/tflat.png)

#### home_longitude

Il campo schema Source **home_longitude** deve essere collegato al campo di destinazione **homeAddress._schema.longitude**.

![Acquisizione dei dati](./images/tflon.png)

#### id

Il campo schema Source **id** deve essere collegato al campo di destinazione **_id**.

![Acquisizione dei dati](./images/tfid1.png)

#### cognome

Il campo schema Source **last_name** deve essere collegato al campo di destinazione **person.name.lastName**.

![Acquisizione dei dati](./images/tflname.png)

#### consents.marketing.email.val

Il campo schema Source **consent.email** deve essere collegato al campo di destinazione **consents.marketing.email.val**.

![Acquisizione dei dati](./images/cons1.png)

#### consents.marketing.commercialEmail.val

Il campo schema Source **consent.commercialEmail** deve essere collegato al campo di destinazione **consents.marketing.commercialEmail.val**.

![Acquisizione dei dati](./images/cons2.png)

#### consents.marketing.any.val

Il campo schema Source **consent.any** deve essere collegato al campo di destinazione **consents.marketing.any.val**.

![Acquisizione dei dati](./images/cons3.png)

Ora dovresti avere questo. Fai clic su **Fine**.

![Acquisizione dei dati](./images/overview.png)

Dopo aver fatto clic su **[!UICONTROL Fine]**, verrà visualizzata la **panoramica del flusso di dati** e dopo alcuni minuti sarà possibile aggiornare la schermata per verificare se il flusso di lavoro è stato completato correttamente. Fai clic sul nome del set di dati di **destinazione**.

![Acquisizione dei dati](./images/dfsuccess.png)

Vedrai quindi il set di dati in cui è stata elaborata l&#39;acquisizione e un [!UICONTROL ID batch] appena acquisito, con 1000 record acquisiti e uno stato di **[!UICONTROL Operazione completata]**. Fare clic su **[!UICONTROL Anteprima set di dati]**.

![Acquisizione dei dati](./images/ingestdataset.png)

Ora visualizzerai un piccolo esempio del set di dati per garantire che i dati caricati siano corretti.

![Acquisizione dei dati](./images/previewdata.png)

Una volta caricati i dati, puoi definire l’approccio di governance dei dati corretto per il nostro set di dati.

### Aggiunta della governance dei dati al set di dati

Ora che i dati del cliente vengono acquisiti, è necessario assicurarsi che questo set di dati sia gestito correttamente per il controllo dell’utilizzo e dell’esportazione. Fai clic sulla scheda **[!UICONTROL Governance dei dati]** e osserva che puoi impostare più tipi di restrizioni: Contratto, Identità e Sensibile, Ecosistema partner e Personalizzato.

![Acquisizione dei dati](./images/dsgovernance.png)

Limitiamo i dati di identità per l’intero set di dati. Passa il puntatore sul nome del set di dati, quindi fai clic sull’icona a forma di matita per modificare le impostazioni.

![Acquisizione dei dati](./images/pencil.png)

Vai a **[!UICONTROL Etichette di identità]** e vedrai che l&#39;opzione **[!UICONTROL I2]** è selezionata. Ciò presuppone che tutte le informazioni in questo set di dati siano almeno indirettamente identificabili per la persona.

Fai clic su **[!UICONTROL Salva modifiche]**.

![Acquisizione dei dati](./images/identity.png)

In un altro modulo, approfondiremo il framework Who della governance dei dati e delle etichette.

Con questo, ora hai acquisito e classificato correttamente i dati CRM in Adobe Experience Platform.

Passaggio successivo: [1.2.5 Data Landing Zone](./ex5.md)

[Torna al modulo 1.2](./data-ingestion.md)

[Torna a tutti i moduli](../../../overview.md)
