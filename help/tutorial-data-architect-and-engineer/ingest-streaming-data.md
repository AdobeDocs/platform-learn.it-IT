---
title: Acquisire dati in streaming
seo-title: Ingest streaming data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Acquisire dati in streaming
description: In questa lezione, trasmetterai i dati in Experienci Platform utilizzando l’SDK per web.
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-streaming-data.jpg
exl-id: 09c24673-af8b-40ab-b894-b4d76ea5b112
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '3344'
ht-degree: 2%

---

# Acquisire dati in streaming

<!--1hr-->

In questa lezione, i dati verranno trasmessi in streaming utilizzando Adobe Experience Platform Web SDK.

Nell’interfaccia di Data Collection è necessario completare due attività principali:

* Dobbiamo implementare Web SDK sul sito web Luma per inviare i dati sull’attività del visitatore dal sito web alla rete Adobe Edge. Verrà eseguita una semplice implementazione utilizzando i tag (precedentemente Launch)

* È necessario configurare un datastream che indichi alla rete Edge dove inoltrare i dati. Lo configureremo per inviare i dati al nostro `Luma Web Events` nella sandbox di Platform.

**Ingegneri dati** dovrà acquisire dati in streaming all’esterno di questa esercitazione. Quando si implementano gli SDK per web o dispositivi mobili di Adobe Experience Platform, in genere uno sviluppatore web o mobile è coinvolto nella creazione del livello dati e nella configurazione delle proprietà dei tag.

Prima di iniziare gli esercizi, guarda questi due brevi video per ulteriori informazioni sull’acquisizione di dati in streaming e Web SDK:

>[!VIDEO](https://video.tv.adobe.com/v/28425?learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/34141?learn=on)

>[!NOTE]
>
>Questo tutorial si concentra sull’acquisizione in streaming da siti web con Web SDK, ma puoi anche eseguire lo streaming dei dati utilizzando [Adobe Mobile SDK](https://developer.adobe.com/client-sdks/documentation/), [Apache Kafka Connect](https://github.com/adobe/experience-platform-streaming-connect)e altri meccanismi.

## Autorizzazioni richieste

In [Configurare le autorizzazioni](configure-permissions.md) Per completare questa lezione, è necessario impostare tutti i controlli di accesso necessari.

<!--
* Permission items **[!UICONTROL Launch]** > **[!UICONTROL Property Rights]** > **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]**, and **[!UICONTROL Publish]**
* Permission item **[!UICONTROL Launch]** > **[!UICONTROL Company Rights]** > **[!UICONTROL Manage Properties]**
* User-role access to the `Luma Tutorial Launch` product profile
* Admin-role access to the `Luma Tutorial Launch` product profile
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Profiles]** > **[!UICONTROL View Profiles]**, **[!UICONTROL Manage Profiles]** and **[!UICONTROL Export Audience Segment]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

<!--## Create a streaming source

1. Log into the [Experience Platform  user interface](https://experience.adobe.com/platform/)
1. Go to **[!UICONTROL Sources]** in the left navigation
1. Filter the list by selecting **[!UICONTROL Streaming]**
1. In the **[!UICONTROL HTTP API]** section, select the **[!UICONTROL Configure]** button
    ![Configure an HTTP API streaming source](assets/websdk-source-confiigureHTTPAPI.png)
1. On the **[!UICONTROL Authentication]** step, enter `Luma Web Events Source` as the **[!UICONTROL Account name]** and select the **[!UICONTROL Connect to source]** button (we don't need to enable authentication since the data will be originating from website visitors)
    ![Configure an HTTP API streaming source](assets/websdk-source-connectSource.png)
1. Once connected, select the **[!UICONTROL Next]** button to proceed to the next step in the workflow
1. On the **[!UICONTROL Select data]** step, choose **[!UICONTROL Existing Dataset]**, select your `Luma Web Events Dataset`, and then select the **[!UICONTROL Next]** button
    ![Select your dataset](assets/websdk-source-selectDataset.png)
1. On the **[!UICONTROL Dataflow detail]** step, select the **[!UICONTROL Next]** button:
    ![Select Next](assets/websdk-source-dataflowName.png)
    <!--What is a good practice for naming the data flow vs the source-->
<!--
1. On the **[!UICONTROL Review]** step, review your source details and select the **[!UICONTROL Finish]** button:
    ![Select Finish](assets/websdk-source-review.png)
-->

## Configurare lo stream di dati

Innanzitutto configureremo lo stream di dati. Un flusso di dati indica alla rete Adobe Edge dove inviare i dati dopo averli ricevuti dalla chiamata SDK web. Inviare i dati ad Experience Platform, Adobe Analytics o Adobe Target? Gli stream di dati vengono gestiti nell’interfaccia utente di Data Collection (precedentemente Launch) e sono fondamentali per la raccolta dei dati con Web SDK.

Per creare [!UICONTROL flusso di dati]:

1. Accedi a [Experience Platform di interfaccia utente di Data Collection](https://experience.adobe.com/launch/)
   <!--when will the edge config go live?-->

1. Seleziona **[!UICONTROL Flussi di dati]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Nuovo flusso di dati]** nell&#39;angolo superiore destro

   ![Seleziona gli stream di dati nel menu di navigazione a sinistra](assets/websdk-edgeConfig-clickNav.png)


1. Per **[!UICONTROL Nome intuitivo]**, immetti `Luma Platform Tutorial` (aggiungi il tuo nome alla fine, se più persone della tua azienda stanno seguendo questo tutorial)
1. Seleziona il pulsante **[!UICONTROL Salva]**

   ![Denomina il flusso di dati e salva](assets/websdk-edgeConfig-name.png)

Nella schermata successiva, specifica dove desideri inviare i dati. Per inviare dati ad Experience Platform:

1. Attiva **[!UICONTROL Adobe Experience Platform]** per esporre campi aggiuntivi
1. Per **[!UICONTROL Sandbox]**, seleziona `Luma Tutorial`
1. Per **[!UICONTROL Set di dati evento]**, seleziona `Luma Web Events Dataset`
1. Se utilizzi altre applicazioni di Adobe, puoi esplorare le altre sezioni per vedere quali informazioni sono necessarie nella configurazione Edge di queste altre soluzioni. L’SDK per web è stato sviluppato non solo per inviare in streaming i dati in Experienci Platform, ma anche per sostituire tutte le librerie JavaScript precedenti utilizzate da altre applicazioni Adobe. La configurazione Edge viene utilizzata per specificare i dettagli dell’account di ogni applicazione a cui si desidera inviare i dati.
1. Seleziona **[!UICONTROL Salva]**
   ![Configurare lo stream di dati e salvare](assets/websdk-edgeConfig-addEnvironment.png)

Una volta salvata la configurazione Edge, la schermata risultante mostrerà tre ambienti creati per Sviluppo, Staging e Produzione. È possibile aggiungere altri ambienti di sviluppo:
![Ogni configurazione Edge può avere più ambienti](assets/websdk-edgeConfig-environments.png)
Tutti e tre gli ambienti contengono i dettagli della piattaforma appena immessi. Tuttavia, questi dettagli possono essere configurati in modo diverso in base all’ambiente. Ad esempio, ogni ambiente potrebbe inviare dati a una sandbox di Platform diversa. In questa esercitazione, non verranno effettuate ulteriori personalizzazioni del flusso di dati.

## Installare l’estensione Web SDK

### Aggiungi una proprietà

Innanzitutto, è necessario creare una proprietà tag (in precedenza una proprietà tag ). Una proprietà è un contenitore per tutti i JavaScript, le regole e le altre funzioni necessarie per raccogliere i dettagli da una pagina web e inviarla a varie posizioni.

Per creare una proprietà:

1. Vai a **[!UICONTROL Proprietà]** nel menu di navigazione a sinistra
1. Seleziona il pulsante **[!UICONTROL Nuova proprietà]**
   ![Aggiungi una nuova proprietà](assets/websdk-property-addNewProperty.png)
1. Come **[!UICONTROL Nome]**, immetti `Luma Platform Tutorial` (aggiungi il tuo nome alla fine, se più persone della tua azienda stanno seguendo questo tutorial)
1. Come **[!UICONTROL Domini]**, immetti `enablementadobe.com` (spiegato in seguito)
1. Seleziona **[!UICONTROL Salva]**
   ![Dettagli proprietà](assets/websdk-property-propertyDetails.png)

<!--
After saving the property, you might see an error message like the one below. If so, this is because you don't actually have access to the property you just created. To fix this, we need to go to the Admin Console to give yourself access:
    ![Error after saving the profile](assets/websdk-property-errorCreating.png)

To give yourself access to the property:

1. In a separate browser tab, log into the [Admin Console](https://adminconsole.adobe.com/)
1. Go to **[!UICONTROL Products]** from the top navigation
1. Select **[!UICONTROL Adobe Experience Platform Launch]** on the left navigation
1. Go to your `Luma Tutorial Launch` product profile
1. Go to the **[!UICONTROL Permissions]** tab
1. On the **[!UICONTROL Properties]** row, select **[!UICONTROL Edit]**
    ![Edit the Property Permissions](assets/websdk-adminconsole-editPermissions.png)
1. Select the "+" icon to move your `Luma Platform Tutorial` property to the right-hand side and select the **[!UICONTROL Save]** button to update the permissions
   
    ![Add the new property](assets/websdk-adminconsole-addProperty.png)

Now switch back to your browser tab with the Data Collection interface still open. Reload the page and the `Luma Platform Tutorial` property should display in the list. Select to open the property:

![Luma Platform Tutorial should appear](assets/websdk-property-showsInList.png)
-->

## Aggiungere l’estensione Web SDK

Ora che disponi di una proprietà puoi aggiungere l’SDK web utilizzando un’estensione. Un’estensione è un pacchetto di codice che estende l’interfaccia e la funzionalità di Data Collection. Aggiungere l’estensione:

1. Apri la proprietà tag
1. Vai a **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra
1. Vai a **[!UICONTROL Catalogo]** scheda
1. Sono disponibili molte estensioni per i tag. Filtra il catalogo con il termine `Web SDK`
1. In **[!UICONTROL Adobe Experience Platform Web SDK]** , seleziona l&#39;estensione **[!UICONTROL Installa]** pulsante
   ![Installare l’estensione Adobe Experience Platform Web SDK](assets/websdk-property-addExtension.png)
1. Sono disponibili diverse configurazioni per l’estensione Web SDK, ma ne verranno configurate solo due per questa esercitazione. Aggiornare il **[!UICONTROL Dominio Edge]** a `data.enablementadobe.com`. Questa impostazione ti consente di impostare i cookie di prime parti con l’implementazione dell’SDK web, il che è consigliato. Più avanti in questa lezione verrà mappato un sito Web sul `enablementadobe.com` nella proprietà tag. Il CNAME per `enablementadobe.com` il dominio è già stato configurato in modo che `data.enablementadobe.com` inoltra ai server Adobe. Quando implementi Web SDK sul tuo sito web, dovrai creare un CNAME per le tue finalità di raccolta dati, ad esempio, `data.YOUR_DOMAIN.com`
1. Dalla sezione **[!UICONTROL Datastream]** a discesa, seleziona il tuo `Luma Platform Tutorial` flusso di dati.
1. Puoi esaminare le altre opzioni di configurazione (ma non modificarle!) e quindi seleziona **[!UICONTROL Salva]**
   <!--is edge domain required for first party? when will it break?-->
   <!--any other fields that should be highlighted-->
   ![](assets/websdk-property-configureExtension.png)



## Creare una regola per inviare dati

Ora creeremo una regola per inviare dati a Platform. Una regola è una combinazione di eventi, condizioni e azioni che indicano ai tag di eseguire un’operazione. Per creare una regola:

1. Vai a **[!UICONTROL Regole]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Crea nuova regola]** pulsante
   ![Creare una regola](assets/websdk-property-createRule.png)
1. Denomina la regola `All Pages - Library Loaded`
1. Sotto **[!UICONTROL Eventi]**, seleziona la **[!UICONTROL Aggiungi]** pulsante
   ![Denomina la regola e aggiungi un evento](assets/websdk-property-nameRule.png)
1. Utilizza il **[!UICONTROL Core]** **[!UICONTROL Estensione]** e seleziona **[!UICONTROL Library Loaded (Page Top)]** come **[!UICONTROL Tipo di evento]**. Questa impostazione significa che la regola viene attivata ogni volta che la libreria Launch viene caricata su una pagina.
1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole
   ![Aggiungere l’evento Library Loaded](assets/websdk-property-addEvent.png)
1. Esci **[!UICONTROL Condizioni]** vuoto, poiché vogliamo che questa regola venga attivata su tutte le pagine, in base al nome che le abbiamo assegnato
1. Sotto **[!UICONTROL Azioni]**, seleziona la **[!UICONTROL Aggiungi]** pulsante
1. Utilizza il **[!UICONTROL Adobe Experience Platform Web SDK]** **[!UICONTROL Estensione]** e seleziona **[!UICONTROL Invia evento]** come **[!UICONTROL Tipo di azione]**
1. A destra, seleziona **[!UICONTROL web.webpagedetails.pageViews]** dal **[!UICONTROL Tipo]** a discesa. Questo è uno dei campi XDM nel nostro `Luma Web Events Schema`
1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole
   ![Aggiungere l’azione Invia evento](assets/websdk-property-addAction.png)
1. Seleziona **[!UICONTROL Salva]** per salvare la regola\
   ![Salva la regola](assets/websdk-property-saveRule.png)

## Pubblicare la regola in una libreria

Ora pubblicheremo la regola nel nostro ambiente di sviluppo in modo da poter verificare che funzioni.

<!--
There are a few quick steps we must take in the **[!UICONTROL Publishing]** section of Launch.


### Create a host

Launch libraries can be hosted on Adobe's Content Delivery Network (CDN) or on your own servers. In this tutorial, we will use Adobe's CDN since it is faster to set up:

1. Go to **[!UICONTROL Hosts]** in the left navigation
1. Select the **[!UICONTROL Create New Host]** button
    ![Create a new host](assets/websdk-property-createHost.png)   
1. For the **[!UICONTROL Name]**, enter `Adobe CDN`
1. For the **[!UICONTROL Type]**, select **[!UICONTROL Managed by Adobe]**
1. Select the **[!UICONTROL Save]** button to complete the setup of the host
    ![Configure the host](assets/websdk-property-hostDetails.png)   

### Create an environment

Environments allow you to have different versions of a library in different publishing environments to accommodate your publishing workflow. For example, the fully tested version of your library can be published to a Production environment, while new changes are being created in a Development environment. You can also use different hosts for each environment. To create an environment:

1. Go to **[!UICONTROL Environments]** in the left navigation
1. Select the **[!UICONTROL Create New Environment]** button
    ![Create a new environment](assets/websdk-property-createEnvironment.png) 
1. Under **[!UICONTROL Development]** select **[!UICONTROL Select]**   
    ![Select the environment type](assets/websdk-property-selectEnvironment.png) 
1. For the **[!UICONTROL Name]**, enter `Development`
1. For the **[!UICONTROL Select Host]** dropdown, select `Adobe CDN`
1. Select the **[!UICONTROL Save]** button to complete the setup of the environment
    ![Configure the environment](assets/websdk-property-configureEnv.png)
1. You will see a modal with URL and other implementation details of this library. These are critical for a real Launch implementation, but we don't need to worry about them for this tutorial. Select the **[!UICONTROL Close]** button to exit the modal.

### Create and publish the library

Now let's bundle the contents of our property&mdash;currently an extension and a rule&mdash;into a library. 
-->

Per creare una libreria:

1. Vai a **[!UICONTROL Flusso di pubblicazione]** nel menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Aggiungi libreria]**
   ![Seleziona Aggiungi libreria](assets/websdk-property-pubAddNewLib.png)
1. Per **[!UICONTROL Nome]**, immetti `Luma Platform Tutorial`
1. Per **[!UICONTROL Ambiente]**, seleziona `Development`
1. Seleziona la **[!UICONTROL Aggiungi tutte le risorse modificate]** pulsante. (oltre al [!UICONTROL Adobe Experience Platform Web SDK] e `All Pages - Library Loaded` regola, visualizzerai anche il [!UICONTROL Core] è stata aggiunta un&#39;estensione che contiene il JavaScript di base richiesto da tutte le proprietà web di Launch.)
1. Seleziona la **[!UICONTROL Salva e genera per sviluppo]** pulsante
   ![Creare e generare la libreria](assets/websdk-property-buildLibrary.png)

La creazione della libreria potrebbe richiedere alcuni minuti e al termine viene visualizzato un punto verde a sinistra del nome della libreria:
![Compilazione completata](assets/websdk-property-buildComplete.png)

Come è possibile vedere sul [!UICONTROL Flusso di pubblicazione] , il processo di pubblicazione richiede molto di più, il che va oltre l’ambito di questa esercitazione. Utilizzeremo un’unica libreria nel nostro ambiente di sviluppo.

## Convalidare i dati nella richiesta

### Aggiungi l’Adobe Experience Platform Debugger

Experienci Platform Debugger è un’estensione disponibile per i browser Chrome e Firefox che consente di visualizzare la tecnologia Adobe implementata nelle pagine web. Scarica la versione per il browser preferito:

* [Estensione Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/)
* [Estensione Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se non hai mai utilizzato il debugger prima, e questo è diverso dal precedente Adobe Experience Cloud Debugger, potresti voler guardare questo video di panoramica di cinque minuti:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

### Apri il sito web Luma.

Per questo tutorial, utilizziamo una versione del sito web demo Luma in hosting pubblico. Apriamolo e aggiungiamo un segnalibro:

1. In una nuova scheda del browser, apri [Sito web Luma](https://luma.enablementadobe.com/content/luma/us/en.html).
1. Aggiungi ai segnalibri la pagina da utilizzare nel resto dell’esercitazione

Questo sito in hosting è il motivo per cui abbiamo utilizzato `enablementadobe.com` nel [!UICONTROL Domini] della configurazione iniziale della proprietà tag e il motivo per cui abbiamo utilizzato `data.enablementadobe.com` come dominio di prime parti in [!UICONTROL Adobe Experience Platform Web SDK] estensione. Vedi, avevo un piano!

![Home page Luma](assets/websdk-luma-homepage.png)

### Utilizza Experienci Platform Debugger per eseguire il mapping alla proprietà tag

Experienci Platform Debugger dispone di una funzione interessante che consente di sostituire una proprietà tag esistente con una diversa. Questo è utile per la convalida e ci consente di saltare molti passaggi di implementazione in questa esercitazione.

1. Assicurati di avere aperto il sito Luma e seleziona l’icona dell’estensione Experienci Platform Debugger
1. Debugger si aprirà e mostrerà alcuni dettagli dell’implementazione hardcoded, che non è correlata a questa esercitazione (potrebbe essere necessario ricaricare il sito Luma dopo aver aperto Debugger)
1. Conferma che il debugger è &quot;**[!UICONTROL Connesso a Luma]**&quot; come illustrato di seguito, quindi selezionare la&quot;**[!UICONTROL blocca]**&quot; per bloccare Debugger sul sito Luma.
1. Seleziona la **[!UICONTROL Accedi]** in alto a destra per eseguire l’autenticazione.
1. Ora vai a **[!UICONTROL Launch]** nel menu di navigazione a sinistra
1. Seleziona la scheda Configurazione.
1. A destra della posizione in cui è visualizzato **[!UICONTROL Codici di incorporamento pagina]**, apri **[!UICONTROL Azioni]** e seleziona **[!UICONTROL Sostituisci]**
   ![Seleziona Azioni > Sostituisci](assets/websdk-debugger-replaceLibrary.png)
1. Poiché sei autenticato, il Debugger estrae le proprietà e gli ambienti di Launch disponibili. Seleziona il `Luma Platform Tutorial` proprietà
1. Seleziona il `Development` ambiente
1. Seleziona la **[!UICONTROL Applica]** pulsante
   ![Seleziona la proprietà tag alternativa](assets/websdk-debugger-selectProperty.png)
1. Il sito web Luma verrà ricaricato _con la proprietà tag_. Aiuto, sono stato attaccato! Sto scherzando.
   ![proprietà tag sostituita](assets/websdk-debugger-propertyReplaced.png)
1. Vai a **[!UICONTROL Riepilogo]** nella barra di navigazione a sinistra, per visualizzare i dettagli [!UICONTROL Launch] proprietà
   ![Scheda Riepilogo](assets/websdk-debugger-summary.png)
1. Ora vai a **[!UICONTROL AEP Web SDK]** nel menu di navigazione a sinistra per visualizzare **[!UICONTROL Richieste di rete]**
1. Apri **[!UICONTROL Eventi]** riga

   ![richiesta Adobe Experience Platform Web SDK](assets/websdk-debugger-platformNetwork.png)
1. Nota come è possibile visualizzare `web.webpagedetails.pageView` tipo di evento specificato nel [!UICONTROL Invia evento] e altre variabili pronte all’uso conformi alla `AEP Web SDK ExperienceEvent Mixin` formato
   ![Dettagli evento](assets/websdk-debugger-eventDetails.png)
1. Questi tipi di dettagli della richiesta sono visibili anche negli strumenti di sviluppo web del browser **Rete** scheda. Apri e ricarica la pagina. Filtra per chiamate con `interact` per individuare la chiamata, selezionarla e quindi cercare nella **Intestazioni** scheda, **Richiedi payload** area.
   ![Scheda Rete](assets/websdk-debugger-networkTab.png)
1. Vai a **Risposta** e osserva come il valore ECID viene incluso nella risposta. Copia questo valore così come lo utilizzerai per convalidare le informazioni sul profilo nell’esercizio successivo.
   ![Scheda Rete](assets/websdk-debugger-networkTab-response.png)



## Convalidare i dati in Experienci Platform

Puoi verificare che i dati stiano arrivando in Platform osservando i batch di dati in arrivo in `Luma Web Events Dataset`. (Lo so, si chiama acquisizione di dati in streaming, ma ora sto dicendo che arriva in batch! Viene inviato in streaming al profilo in tempo reale, quindi può essere utilizzato per la segmentazione e l’attivazione in tempo reale, ma viene inviato in batch ogni 15 minuti al data lake.)

Per convalidare i dati:

1. Nell’interfaccia utente di Platform, vai a **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra
1. Apri `Luma Web Events Dataset` e confermare l&#39;arrivo di un batch. Ricordati che vengono inviati ogni 15 minuti, quindi potrebbe essere necessario attendere la visualizzazione del batch.
1. Seleziona la **[!UICONTROL Anteprima set di dati]** pulsante
   ![Apri il set di dati](assets/websdk-platform-dataset.png)
1. Nella finestra modale di anteprima, tieni presente come selezionare diversi campi dello schema a sinistra per visualizzare in anteprima tali punti dati specifici:
   ![Visualizzare l’anteprima dei campi](assets/websdk-platform-datasetPreview.png)

Puoi anche verificare che il nuovo profilo sia visualizzato:

1. Nell’interfaccia utente di Platform, vai a **[!UICONTROL Profili]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL ECID]** e cerca il valore ECID (copialo dalla risposta). Il profilo avrà un proprio ID, separato dall’ECID.
1. Seleziona la **[!UICONTROL ID profilo]** per aprire il profilo
   ![Trovare e aprire il profilo](assets/websdk-platform-openProfile.png)
1. Seleziona la **[!UICONTROL Eventi]** per visualizzare le pagine visualizzate
   ![Eventi profilo](assets/websdk-platform-profileEvents.png)\
   <!--![](assets/websdk-platform-confirmProfile.png)-->

## Aggiungere dati personalizzati all’evento

### Creare un elemento dati per nome pagina

1. Nell’interfaccia dei tag di raccolta dati, nell’angolo in alto a destra del `Luma Platform Tutorial` , apri la **[!UICONTROL Seleziona una libreria di lavoro]** e seleziona il tuo `Luma Platform Tutorial` libreria. Questa impostazione semplifica la pubblicazione di aggiornamenti aggiuntivi alla libreria.
1. Ora vai a **[!UICONTROL Elementi dati]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Creare un nuovo elemento dati]** pulsante

   ![Crea un nuovo elemento di dati](assets/websdk-property-createNewDataElement.png)
1. Come **[!UICONTROL Nome]**, immetti `Page Name`
1. Come **[!UICONTROL Tipo di elemento dati]**, seleziona `JavaScript Variable`
1. Come **[!UICONTROL Nome variabile JavaScript]**, immetti `digitalData.page.pageInfo.pageName`
1. Per semplificare la standardizzazione del formato dei valori, seleziona le caselle per **[!UICONTROL Forza valore minuscolo]** e **[!UICONTROL Pulisci testo]**
1. Assicurati che `Luma Platform Tutorial` è selezionato come libreria di lavoro
1. Seleziona **[!UICONTROL Salva nella libreria]**
   ![Creare un elemento dati per nome pagina](assets/websdk-property-dataElement-pageName.png)

### Mappare il nome della pagina all’elemento dati Oggetto XDM

Ora mapperemo il nome della nostra pagina all’SDK per web.

>[!IMPORTANT]
>
>Per completare questa attività, è necessario assicurarsi che l’utente abbia prima accesso alla sandbox di Prod. Se non disponi già dell’accesso alla sandbox Prod da un profilo di prodotto diverso, apri rapidamente il tuo `Luma Tutorial Platform` e aggiungere l’elemento di autorizzazione **[!UICONTROL Sandbox]** > **[!UICONTROL Prod]**. Dopo aver eseguito questa operazione, effettua un MAIUSC-Ricarica nella pagina Elementi dati per cancellare la cache
>![Aggiungere la sandbox Prod](assets/websdk-property-permissionToLoadSchema.png)

Il giorno **[!UICONTROL Elementi dati]** pagina:

1. Crea un nuovo elemento di dati
1. Come **[!UICONTROL Nome]**, immetti `XDM Object`
1. Come **[!UICONTROL Estensione]**, seleziona `Adobe Experience Platform Web SDK`
1. Come **[!UICONTROL Tipo di elemento dati]**, seleziona `XDM object`
1. Come **[!UICONTROL Sandbox]**, seleziona il tuo `Luma Tutorial` sandbox
1. Come **[!UICONTROL Schema]**, seleziona il tuo `Luma Web Events Schema`
1. Seleziona la `web.webPageDetails.name` campo
1. Come **[!UICONTROL Valore]**, seleziona l’icona per aprire il modale di selezione dell’elemento dati e scegli il tuo `Page Name` elemento dati
1. Seleziona **[!UICONTROL Salva nella libreria]**
   ![Mappare il nome della pagina all’elemento dati Oggetto XDM](assets/websdk-property-dataElement-createXDMObject.png)

Lo stesso processo viene utilizzato per mappare dati personalizzati aggiuntivi sul sito web ai campi XDM.

### Aggiungere i dati XDM all’azione Invia evento

Ora che hai mappato i dati sui campi XDM, puoi includerli nell’azione Invia evento:

1. Vai a **[!UICONTROL Regole]** screen
1. Apri il `All Pages - Library Loaded` regola
1. Apri `Adobe Experience Platform Web SDK - Send Event` azione
1. Come **[!UICONTROL Dati XDM]**, seleziona l’icona per aprire il modale di selezione dell’elemento dati e scegli il tuo `XDM Object` elemento dati
1. Seleziona la **[!UICONTROL Mantieni modifiche]** pulsante
   ![Aggiungere i dati XDM all’azione Invia evento](assets/websdk-property-addXDMtoSendEvent.png)
1. Da quando hai avuto `Luma Platform Tutorial` come libreria di lavoro per gli ultimi esercizi, le modifiche recenti sono state salvate direttamente nella libreria. Invece di pubblicare le modifiche tramite la schermata Flusso di pubblicazione, puoi aprire il menu a discesa sul pulsante blu e selezionare **[!UICONTROL Salva nella libreria e genera]**
   ![Salva nella libreria e genera](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

Inizia a creare una nuova libreria di tag con le tre modifiche appena apportate.

### Convalidare i dati XDM

Ora dovresti essere in grado di ricaricare la pagina home di Luma, mentre sei mappato sulla proprietà tag utilizzando il Debugger come hai imparato in precedenza, e vedere che il campo del nome pagina si popola nella richiesta.
![Convalidare i dati XDM](assets/websdk-debugger-pageName.png)

Puoi anche verificare che i dati del nome della pagina siano stati ricevuti in Platform, visualizzando in anteprima il set di dati e il profilo.

## Invia identità aggiuntive

L’implementazione dell’SDK per web sta ora inviando eventi con l’ID Experience Cloud (ECID) come identificatore primario. L’ECID viene generato automaticamente dall’SDK per web ed è univoco per dispositivo e browser. Un singolo cliente può avere più ECID a seconda del dispositivo e del browser in uso. Come possiamo ottenere una visione unificata di questo cliente e collegare la sua attività online ai nostri dati di gestione delle relazioni con i clienti, fedeltà e acquisto offline? Lo facciamo raccogliendo identità aggiuntive durante la loro sessione e collegando in modo deterministico il loro profilo tramite l’unione di identità.

Se ricordi, ho detto che avremmo utilizzato l’ECID e l’ID del sistema di gestione delle relazioni con i clienti come identità per i nostri dati web in [Mappare le identità](map-identities.md) lezione. Quindi raccogliamo l’ID del sistema di gestione delle relazioni con i clienti con l’SDK per web!

### Aggiungi elemento dati per l’ID CRM

Innanzitutto, memorizziamo l’ID del sistema di gestione delle relazioni con i clienti in un elemento dati:

1. Nell’interfaccia dei tag, aggiungi un elemento dati denominato `CRM Id`
1. Come **[!UICONTROL Tipo di elemento dati]**, seleziona **[!UICONTROL Variabile JavaScript]**
1. Come **[!UICONTROL Nome variabile JavaScript]**, immetti `digitalData.user.0.profile.0.attributes.username`
1. Seleziona la **[!UICONTROL Salva nella libreria]** pulsante (`Luma Platform Tutorial` dovrebbe essere ancora la tua libreria di lavoro)
   ![Aggiungi elemento dati per l’ID CRM](assets/websdk-property-dataElement-crmId.png)

### Aggiungere l’ID del sistema di gestione delle relazioni con i clienti all’elemento dati della Mappa identità

Ora che abbiamo acquisito il valore ID del sistema di gestione delle relazioni con i clienti, dobbiamo associarlo a un tipo di elemento dati speciale denominato [!UICONTROL Mappa identità] data element:

1. Aggiungi un elemento dati denominato `Identities`
1. Come **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Come **[!UICONTROL Tipo di elemento dati]**, seleziona **[!UICONTROL Mappa identità]**
1. Come **[!UICONTROL Namespace]**, immetti `Luma CRM Id`, che è il [!UICONTROL namespace] creato in una lezione precedente

   >[!WARNING]
   >
   >La versione 2.2 dell’estensione Adobe Experience Platform Web SDK consente di selezionare Spazio dei nomi da un elenco a discesa precompilato utilizzando i valori effettivi nell’account Platform. Sfortunatamente, questa funzione non è ancora &quot;in grado di riconoscere la sandbox&quot; e quindi `Luma CRM Id` Il valore potrebbe non essere visualizzato nel menu a discesa. Questo potrebbe impedirti di completare questo esercizio. Una volta confermata, verrà pubblicata una soluzione alternativa.

1. Come **[!UICONTROL ID]**, seleziona l’icona per aprire il modale di selezione dell’elemento dati e scegli il tuo `CRM Id` elemento dati
1. Come **[!UICONTROL Stato autenticato]**, seleziona **[!UICONTROL Autenticato]**
1. Esci **[!UICONTROL Principale]** _non selezionato_. Poiché l’ID CRM non è presente per la maggior parte dei visitatori del sito web Luma, puoi sicuramente _non desideri ignorare l’ECID come identificatore primario_. Sarebbe un caso d’uso raro utilizzare qualcosa di diverso dall’ECID come identificatore primario. Di solito non menziono le impostazioni predefinite in queste istruzioni, ma sto chiamando questo per aiutarti a evitare problemi più avanti nella tua implementazione.
1. Seleziona la **[!UICONTROL Salva nella libreria]** pulsante (`Luma Platform Tutorial` dovrebbe essere ancora la tua libreria di lavoro)
   ![Aggiungere l’ID del sistema di gestione delle relazioni con i clienti all’elemento dati della Mappa identità](assets/websdk-property-dataElement-identityMap.png)

>[!NOTE]
>
>Puoi trasmettere più identificatori utilizzando [!UICONTROL Mappa identità] tipo di dati.

### Aggiungere l’elemento dati Identity Map all’oggetto XDM

È necessario aggiornare un altro elemento dati: l’elemento dati Oggetto XDM. Può sembrare strano dover aggiornare tre elementi di dati separati per passare questa identità, ma questo processo è progettato per scalare per più identità. Non preoccuparti, questa lezione è quasi finita!

1. Aprire l’elemento dati Oggetto XDM
1. Apri il campo XDM di IdentityMap
1. Come **[!UICONTROL Elemento dati]**, seleziona l’icona per aprire il modale di selezione dell’elemento dati e scegli il tuo `Identities` elemento dati
1. Da quando hai avuto `Luma Platform Tutorial` come libreria di lavoro per gli ultimi esercizi, le modifiche recenti sono state salvate direttamente nella libreria. Invece di pubblicare le modifiche tramite la schermata Flusso di pubblicazione, puoi aprire il menu a discesa sul pulsante blu e selezionare **[!UICONTROL Salva nella libreria e genera]**
   ![Aggiungere l’elemento dati IdentityMap all’oggetto XDM](assets/websdk-property-dataElement-addIdentitiesToXDMObject.png)


### Convalidare l’identità

Per verificare che l’ID del sistema di gestione delle relazioni con i clienti sia ora inviato dall’SDK Web:

1. Apri [Sito web Luma](https://luma.enablementadobe.com/content/luma/us/en.html)
1. Mappare il file alla proprietà tag utilizzando Debugger, come indicato nelle istruzioni precedenti
1. Seleziona la **Login** collegamento in alto a destra del sito web Luma
1. Accedi utilizzando le credenziali `test@adobe.com`/`test`
1. Una volta autenticata, controlla la chiamata Experienci Platform Web SDK nel debugger (**[!UICONTROL Adobe Experience Platform Web SDK]** > **[!UICONTROL Richieste di rete]** > **[!UICONTROL Eventi]** della richiesta più recente) e dovresti vedere `lumaCrmId`:
   ![Convalidare l’identità nel debugger](assets/websdk-debugger-confirmIdentity.png)
1. Cerca di nuovo il profilo utente utilizzando lo spazio dei nomi e il valore ECID. Nel profilo troverai l’ID del sistema di gestione delle relazioni con i clienti, l’ID fedeltà e i dettagli del profilo, come il nome e il numero di telefono. Tutte le identità e i dati sono stati uniti in un unico profilo cliente in tempo reale.
   ![Convalidare l’identità in Platform](assets/websdk-platform-lumaCrmIdProfile.png)


## Risorse aggiuntive

* [Implementare Adobe Experience Cloud con Web SDK](/help/tutorial-web-sdk/overview.md)
* [Documentazione sull’acquisizione in streaming](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=it)
* [Riferimento API per Streaming Ingestion](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)

Ottimo lavoro! Queste erano molte informazioni su Web SDK e Launch. L’implementazione completa richiede molto più lavoro, ma queste sono le nozioni di base per aiutarti a iniziare e visualizzare i risultati in Platform.

>[!NOTE]
>
>Ora che hai terminato la lezione Streaming Ingestion, puoi rimuovere [!UICONTROL Prod] sandbox dal tuo `Luma Tutorial Platform` profilo prodotto


Ingegneri dati, se lo desideri puoi passare al [lezione sull’esecuzione di query](run-queries.md).

Architetti di dati, puoi passare a [criteri di unione](create-merge-policies.md)!
