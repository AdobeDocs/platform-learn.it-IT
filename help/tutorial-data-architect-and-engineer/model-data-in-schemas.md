---
title: Dati modello negli schemi
seo-title: Model data in schemas | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Dati modello negli schemi
description: In questa lezione, modellerai i dati di Luma in schemi. Questa è una delle lezioni più lunghe dell'esercitazione, quindi prendi un bicchiere d'acqua e allacci la cintura!
role: Data Architect
feature: Schemas
jira: KT-4348
thumbnail: 4348-model-data-in-schemas.jpg
exl-id: 317f1c39-7f76-4074-a246-ef19f044cb85
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 1%

---

# Dati modello negli schemi

<!-- 60min -->
In questa lezione, modellerai i dati di Luma in schemi. Questa è una delle lezioni più lunghe dell&#39;esercitazione, quindi prendi un bicchiere d&#39;acqua e allacci la cintura!

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di Adobe Experience Platform. Experience Data Model (XDM) è un tentativo di standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione da utilizzare per comunicare con i servizi di Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che può fornire informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione.

XDM è il framework fondamentale che consente a Adobe Experience Cloud, con tecnologia Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, nel momento esatto giusto. La metodologia su cui viene generato Experience Platform, **XDM System**, rende operativi gli schemi Experience Data Model per l&#39;utilizzo da parte dei servizi Platform.

<!--
This seems too lengthy. The video should suffice

Key terms:

* **Schema**: a representation of your data. A schema is comprised of a class and optional field groups and is used to create datasets. A schema includes behavioral attributes, timestamp, identity, attribute definitions, and relationships.
* **XDM Profile Class**: a common schema class used to represent record data
* **XDM ExperienceEvent Class**: a common schema class used to represent time-series data
* **Field group**: allows users to extend reusable fields that contain variables defining one or more attribute intended to be included in a schema or added to a class.
* **Standard Field group**: an open-source Field group built to conform to common industry standards, used to accelerate implementation and support repeatable services operating on the data
* **Data type**: a reusable object with properties in a hierarchical representation. These can be standard types or custom-defined defined types to describe your own data in your own way (for example, a collection of fields that you use to describe your products). Unlike Field groups, data types can be used in schemas regardless of the class.
* **Field**: a field is the lowest level element of a schema. Each field has a name for referencing and a type to identify the type of data that it contains. Field types can include, integer, number, string, Boolean and schema.
-->

**Gli architetti di dati** dovranno creare schemi al di fuori di questa esercitazione, ma **i Data Engineer** lavoreranno a stretto contatto con gli schemi creati dall&#39;architetto di dati.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sugli schemi e sull’Experience Data Model (XDM):
>[!VIDEO](https://video.tv.adobe.com/v/27105?learn=on&enablevpops)

>[!TIP]
>
> Per informazioni più approfondite sulla modellazione dei dati in Experience Platform, ti consigliamo di guardare la playlist [Modellare i dati sull&#39;esperienza del cliente con XDM](https://experienceleague.adobe.com/en/playlists/experience-platform-model-your-customer-experience-data-with-xdm), disponibile gratuitamente su Experience League.

## Autorizzazioni richieste

Nella lezione [Configurare le autorizzazioni](configure-permissions.md) è possibile impostare tutti i controlli di accesso necessari per completare la lezione.

<!--, specifically:

* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)-->


<!--
## Luma's goals
-->

## Creare uno schema di fedeltà tramite l’interfaccia utente

In questo esercizio, creeremo uno schema per i dati fedeltà di Luma.

1. Vai all’interfaccia utente di Platform e accertati che la sandbox sia selezionata.
1. Vai a **[!UICONTROL Schemi]** nel menu di navigazione a sinistra.
1. Seleziona il pulsante **[!UICONTROL Crea schema]** in alto a destra.
   ![Schema con gruppo di campi OOTB](assets/schemas-loyaltyCreateSchema.png)

1. Nel flusso di lavoro Crea schema, seleziona **[!UICONTROL Profilo individuale]** come classe base per lo schema, poiché verranno modellati gli attributi di un singolo cliente (punti, stato e così via).
1. Seleziona **[!UICONTROL Avanti]**.
   ![Seleziona classe base](assets/schemas-loyaltySelectBaseClass.png)

1. Immetti `Luma Loyalty Schema` nel campo di testo **[!UICONTROL Schema display name]**. Nell’area di lavoro seguente, puoi anche rivedere e verificare la struttura dello schema di base fornita dalla classe scelta.
1. Seleziona **[!UICONTROL Fine]** per creare lo schema.
   ![Fine creazione schema fedeltà](assets/schemas-loyaltyFinishSchemaCreation.png)

### Aggiungi gruppi di campi standard

Una volta creato lo schema, verrai reindirizzato all’editor schema, dove potrai aggiungere campi allo schema. Puoi aggiungere campi singoli direttamente allo schema o utilizzare gruppi di campi. È importante notare che tutti i singoli campi sono ancora associati a una classe o a un gruppo di campi. Puoi scegliere tra un ampio set di gruppi di campi standard del settore forniti da Adobe o crearne di personalizzati. Quando inizi a modellare i tuoi dati in Experience Platform, è bene acquisire familiarità con i gruppi di campi standard di settore forniti da Adobe. Quando possibile, è consigliabile utilizzarli in quanto a volte alimentano servizi a valle, come IA per l’analisi dei clienti, IA per l’attribuzione e Adobe Analytics.

Quando lavori con i tuoi dati, un passaggio importante consisterà nel determinare quali dei tuoi dati devono essere acquisiti in Platform e come devono essere modellati. Questo argomento di grandi dimensioni viene discusso più approfonditamente nella playlist [Modellare i dati sull&#39;esperienza del cliente con XDM](https://experienceleague.adobe.com/en/playlists/experience-platform-model-your-customer-experience-data-with-xdm). In questa esercitazione, ti guiderò attraverso l&#39;implementazione di alcuni schemi predeterminati.

Per aggiungere gruppi di campi:

1. Seleziona **[!UICONTROL Aggiungi]** nell&#39;intestazione **[!UICONTROL Gruppi di campi]**.
   ![Aggiungi un nuovo gruppo di campi](assets/schemas-loyalty-addFieldGroup.png)
1. Nel modale **[!UICONTROL Aggiungi gruppi di campi]**, seleziona i seguenti gruppi di campi:
   1. **[!UICONTROL Dettagli demografici]** per dati cliente di base come nome e data di nascita
   1. **[!UICONTROL Dati personali]** per informazioni di contatto di base quali indirizzo e-mail e numero di telefono
1. Puoi visualizzare in anteprima i campi che hanno contribuito nel gruppo di campi selezionando l’icona a destra della riga.
   ![Selezionare gruppi di campi standard](assets/schemas-loyalty-addFirstTwoFieldGroups.png)

1. Seleziona la casella **[!UICONTROL Settore]** > **[!UICONTROL Vendita al dettaglio]** per esporre gruppi di campi specifici del settore.
1. Seleziona **[!UICONTROL Dettagli fedeltà]** per aggiungere i campi del programma fedeltà.
1. Seleziona **[!UICONTROL Aggiungi gruppi di campi]** per aggiungere tutti e tre i gruppi di campi allo schema.
   ![Aggiungi gruppi di campi standard allo schema fedeltà](assets/schemas-loyalty-saveOotbMixins.png)


Ora, prendi un po’ di tempo per esplorare lo stato corrente dello schema. I gruppi di campi hanno aggiunto campi standard relativi a una persona, ai relativi dettagli di contatto e allo stato del programma fedeltà. Questi due gruppi di campi possono risultare utili quando si creano schemi per i dati della propria azienda. Seleziona una riga specifica del gruppo di campi o seleziona la casella accanto al nome del gruppo di campi per visualizzare le modifiche apportate alla visualizzazione.

Per salvare lo schema, selezionare **[!UICONTROL Salva]**.
![Salva schema](assets/schemas-loyalty-saveSchema.png)

>[!NOTE]
>
>È possibile aggiungere un campo per un punto dati che non viene raccolto da un gruppo di campi. Ad esempio, &quot;faxPhone&quot; potrebbe essere un campo per il quale Luma non raccoglie dati. Va bene. Solo perché un campo è definito nello schema non significa che i dati per esso *devono* essere acquisiti in un secondo momento. Puoi anche rimuovere il campo dallo schema.

### Aggiungere un gruppo di campi personalizzato

Ora creiamo un gruppo di campi personalizzato.

Anche se il gruppo di campi fedeltà conteneva un campo `loyaltyID`, Luma vorrebbe gestire tutti i suoi identificatori di sistema in un unico gruppo per garantire la coerenza tra i suoi schemi.

I gruppi di campi devono essere creati nel flusso di lavoro dello schema. Puoi effettuare le seguenti operazioni:

* Aggiungere prima un nuovo campo personalizzato allo schema, quindi creare un gruppo di campi personalizzato oppure
* Creare prima un gruppo di campi personalizzato e quindi aggiungervi campi.

Questa esercitazione inizia con la creazione di un gruppo di campi personalizzato.

Per creare il gruppo di campi:

1. Seleziona **[!UICONTROL Aggiungi]** nell&#39;intestazione **[!UICONTROL Gruppi di campi schema]**
   ![Aggiungi un nuovo gruppo di campi](assets/schemas-loyalty-addFieldGroup.png)
1. Seleziona **[!UICONTROL Crea nuovo gruppo di campi]**
1. Usa `Luma Identity profile field group` come **[!UICONTROL Nome visualizzato]**
1. Utilizza `system identifiers for XDM Individual Profile class` come **[!UICONTROL Descrizione]**
1. Seleziona **[!UICONTROL Aggiungi gruppi di campi]**
   ![Aggiungi un nuovo gruppo di campi](assets/schemas-loyalty-nameFieldGroup.png)

Il nuovo gruppo di campi vuoto viene aggiunto allo schema. I pulsanti **[!UICONTROL +]** possono essere utilizzati per aggiungere nuovi campi a qualsiasi posizione nella gerarchia. Nel nostro caso, vogliamo aggiungere campi a livello principale:

1. Seleziona **[!UICONTROL +]** accanto al nome dello schema. Questo aggiunge un nuovo campo nello spazio dei nomi dell’ID tenant per gestire i conflitti tra i campi personalizzati e tutti i campi standard.
1. Nella barra laterale **[!UICONTROL Proprietà campo]** aggiungi i dettagli del nuovo campo:
   1. **[!UICONTROL Nome campo]**: `systemIdentifier`
   1. **[!UICONTROL Nome visualizzato]**: `System Identifier`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Oggetto]**
   1. Nel menu a discesa **[!UICONTROL Gruppo di campi]**, seleziona il gruppo di campi **Profilo identità Luma** che abbiamo creato.

      ![Aggiungi un nuovo gruppo di campi](assets/schemas-loyalty-addSystemIdentifier.png)
   1. Seleziona **[!UICONTROL Applica]**

      ![Applica nuove proprietà campo](assets/schemas-loyalty-applySystemIdentifier.png)

Ora aggiungi due campi sotto l&#39;oggetto `systemIdentifier`:

1. Primo campo
   1. **[!UICONTROL Nome campo]**: `loyaltyId`
   1. **[!UICONTROL Nome visualizzato:]** `Loyalty Id`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Stringa]**
1. Secondo campo
   1. **[!UICONTROL Nome Campo]**: `crmId`
   1. **[!UICONTROL Nome visualizzato]**: `CRM Id`
   1. **[!UICONTROL Tipo]**: **[!UICONTROL Stringa]**

Il nuovo gruppo di campi sarà simile al seguente. Seleziona il pulsante **[!UICONTROL Salva]** per salvare lo schema, ma lascia aperto lo schema per l&#39;esercizio successivo.
![Gruppo di campi fedeltà completato](assets/schemas-loyalty-identityFieldGroupComplete.png)

## Creare un tipo di dati

I gruppi di campi, ad esempio il nuovo `Luma Identity profile field group`, possono essere riutilizzati in altri schemi, consentendo di applicare definizioni di dati standard in più sistemi. Ma possono essere riutilizzati solo _negli schemi che condividono una classe_, in questo caso la classe Profilo individuale XDM.

Il tipo di dati è un altro costrutto a più campi che può essere riutilizzato negli schemi _in più classi_. Convertiamo il nuovo oggetto `systemIdentifier` in un tipo di dati:

Con `Luma Loyalty Schema` ancora aperto, selezionare l&#39;oggetto `systemIdentifier` e selezionare **[!UICONTROL Converti in nuovo tipo di dati]**

![Gruppo di campi fedeltà completato](assets/schemas-loyalty-convertToDataType.png)

Se **[!UICONTROL Annulla]** esce dallo schema e passi alla scheda **[!UICONTROL Tipi di dati]**, verrà visualizzato il nuovo tipo di dati creato. Questo tipo di dati verrà utilizzato più avanti nella lezione.

![Gruppo di campi fedeltà completato](assets/schemas-loyalty-confirmDataType.png)


## Creare uno schema di gestione delle relazioni con i clienti tramite API

Ora creeremo uno schema utilizzando l’API.

>[!TIP]
>
> Se preferisci saltare l’esercizio API, puoi creare il seguente schema utilizzando il metodo dell’interfaccia utente:
>
> 1. Usa la classe [!UICONTROL Profilo individuale]
> 1. Denomina `Luma CRM Schema`
> 1. Utilizza i seguenti gruppi di campi: Dettagli demografici, Dettagli contatto personale e Gruppo di campi del profilo Identità Luma

Innanzitutto creiamo lo schema vuoto:

1. Apri [!DNL Postman]
1. Se non disponi di un token di accesso, apri la richiesta **[!DNL OAuth: Request Access Token]** e seleziona **Invia** per richiedere un nuovo token di accesso.
1. Apri le variabili di ambiente e cambia il valore di **CONTAINER_ID** da `global` a `tenant`. Ricorda che devi utilizzare `tenant` ogni volta che desideri interagire con i tuoi elementi personalizzati in Platform, ad esempio la creazione di uno schema.
1. Seleziona **Salva**
   ![Modifica CONTAINER_ID in tenant](assets/schemas-crm-changeContainerId.png)
1. Apri la richiesta **[!DNL Schema Registry API > Schemas > Create a new custom schema.]**
1. Apri la scheda **Corpo** e incolla il seguente codice e seleziona **Invia** per effettuare la chiamata API. Questa chiamata crea un nuovo schema utilizzando la stessa classe base `XDM Individual Profile`:

   ```json
   {
     "type": "object",
     "title": "Luma CRM Schema",
     "description": "Schema for CRM data of Luma Retail ",
     "allOf": [{
       "$ref": "https://ns.adobe.com/xdm/context/profile"
     }]
   }
   ```

   >[!NOTE]
   >
   >I riferimenti allo spazio dei nomi in questo e nei successivi esempi di codice (ad esempio `https://ns.adobe.com/xdm/context/profile`), possono essere ottenuti utilizzando le chiamate API di elenco con **[!DNL CONTAINER_ID]** e accettando l&#39;intestazione impostata sui valori corretti. Alcune sono facilmente accessibili anche nell’interfaccia utente.

1. Dovresti ricevere una risposta `201 Created`
1. Copia `meta:altId` dal corpo della risposta. La utilizzeremo successivamente in un altro esercizio.
   ![Creare lo schema CRM](assets/schemas-crm-createSchemaCall.png)

1. Il nuovo schema deve essere visibile nell’interfaccia utente, ma senza gruppi di campi
   ![Creare lo schema CRM](assets/schemas-loyalty-emptySchemaInTheUI.png)

>[!NOTE]
>
> È inoltre possibile ottenere l&#39;ID di schema o `meta:altId` effettuando la richiesta API **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]** con **[!UICONTROL CONTAINER_ID]** impostato su `tenant` e un&#39;intestazione Accept `application/vnd.adobe.xdm+json`.

>[!TIP]
>
> Problemi comuni relativi a questa chiamata e probabili correzioni:
>
> * Nessun token di autenticazione: esegui la richiesta **OAuth: Request Access Token** per generare un nuovo token
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: aggiorna la variabile di ambiente **CONTAINER_ID** da `global` a `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: verificare le autorizzazioni utente in Admin Console

### Aggiungi gruppi di campi standard

Ora è il momento di aggiungere i gruppi di campi allo schema:

1. In [!DNL Postman], apri la richiesta **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. Nella scheda **Parametri**, incolla il valore `meta:altId` dalla risposta precedente come `SCHEMA_ID`
1. Apri la scheda Corpo e incolla il seguente codice e seleziona **Invia** per effettuare la chiamata API. Questa chiamata aggiunge i gruppi di campi standard al tuo `Luma CRM Schema`:

   ```json
   [{
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
       }
     },
     {
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
       }
     }
   ]
   ```

1. Dovresti ottenere uno stato OK 200 per la risposta e i gruppi di campi dovrebbero essere visibili come parte dello schema nell’interfaccia utente

   ![Gruppi di campi standard aggiunti](assets/schemas-crm-addMixins.png)


### Aggiungi gruppo di campi personalizzato

Ora aggiungiamo `Luma Identity profile field group` allo schema. Innanzitutto, dobbiamo trovare l’ID del nuovo gruppo di campi, utilizzando un’API di elenco:

1. Apri la richiesta **[!DNL Schema Registry API > Field groups > Retrieve a list of field groups within the specified container.]**
1. Seleziona il pulsante **Invia** per recuperare un elenco di tutti i gruppi di campi personalizzati nel tuo account
1. Acquisisci il valore `$id` di `Luma Identity profile field group` (il tuo sarà diverso dal valore in questa schermata)
   ![Recupera l&#39;elenco dei gruppi di campi](assets/schemas-crm-getListOfMixins.png)
1. Apri di nuovo la richiesta **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. La scheda **Parametri** deve contenere ancora `$id` dello schema
1. Apri la scheda **Corpo** e incolla il seguente codice, sostituendo il valore `$ref` con il `$id` del tuo `Luma Identity profile field group`:

   ```json
   [{
     "op": "add",
     "path": "/allOf/-",
     "value": {
       "$ref": "REPLACE_WITH_YOUR_OWN_FIELD_GROUP_ID"
     }
   }]
   ```

1. Seleziona **Invia**
   ![Aggiunta del gruppo di campi di identità](assets/schemas-crm-addIdentityMixin.png)

Verifica che il gruppo di campi sia stato aggiunto allo schema controllando sia la risposta API che l’interfaccia.

## Crea schema eventi di acquisto offline

Ora creiamo uno schema basato sulla classe **[!UICONTROL Experience Event]** per i dati di acquisto offline di Luma. Poiché ora conosci l’interfaccia utente dell’editor schema, ridurrò il numero di schermate nelle istruzioni:

1. Crea uno schema con la classe **[!UICONTROL Experience Event]**.
1. Denomina lo schema `Luma Offline Purchase Events Schema`.
1. Aggiungi il gruppo di campi standard **[!UICONTROL Dettagli Commerce]** per acquisire i dettagli dell&#39;ordine comuni. Trascorri qualche minuto ad esplorare gli oggetti al loro interno.
1. Cerca `Luma Identity profile field group`. Non è disponibile. Ricorda che i gruppi di campi sono legati a una classe e che non è possibile utilizzarlo poiché per questo schema viene utilizzata una classe diversa. È necessario aggiungere un nuovo gruppo di campi per la classe ExperienceEvent XDM contenente i campi di identità. Il nostro tipo di dati lo renderà molto semplice!
1. Seleziona il pulsante di scelta **[!UICONTROL Crea nuovo gruppo di campi]**
1. Immetti **[!UICONTROL Nome visualizzato]** come `Luma Identity ExperienceEvent field group` e seleziona il pulsante **[!UICONTROL Aggiungi gruppi di campi]**
1. Seleziona **[!UICONTROL +]** accanto al nome dello schema.
1. Come **[!UICONTROL Nome campo]**, immetti `systemIdentifier`.
1. Come **[!UICONTROL Nome visualizzato]**, immetti `System Identifier`.
1. Come **[!UICONTROL Tipo]**, selezionare **Identificatore di sistema** che è il tipo di dati personalizzato creato in precedenza.
1. Come **[!UICONTROL Gruppo di campi]**, seleziona **Gruppo di campi ExperienceEvent Luma Identity**.
1. Selezionare il pulsante **[!UICONTROL Applica]**.
1. Seleziona il pulsante **[!UICONTROL Salva]**.

Il tipo di dati ha aggiunto tutti i campi.

![Aggiungi il tipo di dati al gruppo di campi](assets/schemas-offlinePurchases-addDatatype.png)

Inoltre, seleziona **[!UICONTROL XDM ExperienceEvent]** sotto l&#39;intestazione **[!UICONTROL Class]** ed esamina alcuni dei campi forniti da questa classe. Tieni presente che i campi _id e timestamp sono obbligatori quando utilizzi la classe ExperienceEvent XDM: questi campi devono essere compilati per ogni record acquisito quando utilizzi questo schema:

![Struttura base evento esperienza](assets/schemas-offlinePurchase-experienceEventbase.png)

## Crea schema eventi web

Ora creeremo un altro schema per i dati del sito web di Luma. A questo punto dovresti essere un esperto nella creazione di schemi. Genera lo schema seguente con queste proprietà

| Proprietà | Valore |
|---------------|-----------------|
| Classe | Evento esperienza |
| Nome schema | Schema eventi web Luma |
| Gruppo di campi | AEP Web SDK ExperienceEvent |
| Gruppo di campi | Evento esperienza del consumatore |

Seleziona il gruppo di campi **[!UICONTROL Evento esperienza del consumatore]**. Questo gruppo di campi contiene gli oggetti commerce e productListItems presenti anche in [!UICONTROL Dettagli Commerce]. In effetti [!UICONTROL Consumer Experience Event] è una combinazione di diversi altri gruppi di campi standard disponibili separatamente. Il gruppo di campi [!UICONTROL ExperienceEvent] di AEP Web SDK contiene anche altri gruppi di campi, inclusi alcuni degli stessi in [!UICONTROL Evento esperienza del consumatore]. Fortunatamente, si fondono perfettamente.

Non è stato aggiunto `Luma Identity ExperienceEvent field group` a questo schema. Questo perché il Web SDK ha un modo diverso di raccogliere le identità. Se si seleziona la classe **[!UICONTROL XDM ExperienceEvent]** nella sezione **[!UICONTROL Composition]** dell&#39;editor schema, si noterà che uno dei campi aggiunti per impostazione predefinita è denominato **[!UICONTROL IdentityMap]**. [!DNL IdentityMap] viene utilizzato da varie applicazioni Adobe per il collegamento a Platform. Nella lezione di acquisizione in streaming, vedrai come le identità vengono inviate a Platform tramite identityMap.


## Crea schema catalogo prodotti

Utilizzando i gruppi di campi [!UICONTROL Dettagli Commerce] e [!UICONTROL Evento esperienza del consumatore], Luma segnala alcuni dettagli di eventi relativi al prodotto tramite il tipo di dati productListItems standard. ma dispongono anche di campi aggiuntivi per i dettagli del prodotto che desiderano inviare a Platform. Invece di acquisire tutti questi campi nei loro sistemi di punto vendita e e-commerce, Luma preferirebbe acquisire questi campi direttamente dal proprio sistema di catalogo dei prodotti. Una &quot;relazione di schema&quot; consente di definire una relazione tra due schemi a scopo di classificazione o ricerca. Luma utilizzerà una relazione per classificare i propri dettagli di prodotto. Inizieremo il processo ora e lo completeremo alla fine della prossima lezione.

>[!NOTE]
>
>Se sei un cliente Analytics o Target esistente, la classificazione delle entità con relazioni di schema è analoga alla classificazione di SAINT o al caricamento del catalogo prodotti per la funzione Consigli

Innanzitutto, devi creare uno schema per il catalogo prodotti di Luma utilizzando una classe personalizzata:

1. Selezionare il pulsante **[!UICONTROL Crea schema]**.
1. Nel flusso di lavoro Crea schema, seleziona l&#39;opzione **[!UICONTROL Altro]**.
   ![Crea nuovo schema](assets/schemas-newSchema-browseClasses.png)
1. Seleziona il pulsante **[!UICONTROL Crea classe]**
1. Denomina `Luma Product Catalog Class`
1. Lascia **[!UICONTROL Comportamento]** come **[!UICONTROL Record]**
1. Seleziona il pulsante **[!UICONTROL Crea]**.
   ![Crea nuova classe](assets/schemas-productClass.png)
1. La **classe del catalogo prodotti Luma** creata viene visualizzata nella tabella Classi seguente. Assicurati che la classe sia selezionata, quindi seleziona **[!UICONTROL Successivo]**.
   ![Nuova classe aggiunta](assets/schemas-productClassSelected.png)
1. Denomina lo schema `Luma Product Catalog Schema`.
1. Crea un nuovo [!UICONTROL gruppo di campi] denominato `Luma Product Catalog field group` con i campi seguenti:
   1. productName: Product Name: String
   1. productCategory: ProductCategory: String
   1. productColor: Product Color: String
   1. productSku: Product SKU: String | Obbligatorio
   1. productSize: Product Size: String
   1. productPrice: Product Price: Double
1. **[!UICONTROL Salva]** lo schema

Il nuovo schema deve essere simile al seguente. Il campo `productSku` è elencato nella sezione [!UICONTROL Campi obbligatori]:
![Schema prodotto](assets/schemas-productSchema.png)

Il passaggio successivo consiste nel definire la relazione tra i due schemi ExperienceEvent e `Luma Product Catalog Schema`. Tuttavia, prima di procedere, è necessario eseguire alcuni passaggi aggiuntivi nella lezione successiva.


## Risorse aggiuntive

* [Documentazione del sistema Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it)
* [API Registro schemi](https://www.adobe.io/experience-platform-apis/references/schema-registry/)


Ora che hai i tuoi schemi puoi [mappare le identità](map-identities.md)!
