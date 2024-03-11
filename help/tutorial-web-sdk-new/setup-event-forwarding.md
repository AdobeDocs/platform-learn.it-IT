---
title: Impostare una proprietà di inoltro eventi
description: Scopri come utilizzare la proprietà di inoltro degli eventi utilizzando i dati Experienci Platform Web SDK. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Event Forwarding
source-git-commit: fd366a4848c2dd9e01b727782e2f26005a440725
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 3%

---

# Impostare una proprietà di inoltro eventi

Scopri come utilizzare la proprietà di inoltro degli eventi utilizzando i dati Experienci Platform Web SDK.

L’inoltro degli eventi è un nuovo tipo di proprietà disponibile in Raccolta dati. L’inoltro di eventi consente di inviare dati a fornitori di terze parti non Adobi direttamente da Adobe Experience Platform Edge Network anziché dal tradizionale browser lato client. Ulteriori informazioni sui vantaggi dell’inoltro degli eventi nel [Panoramica sull’inoltro degli eventi](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en).


![Diagramma dell’SDK per web e dell’inoltro degli eventi](assets/dc-websdk-eventforwarding.png)

Per utilizzare l’inoltro degli eventi in Adobe Experience Platform, i dati devono essere inviati a Adobe Experience Platform Edge Network utilizzando una o più delle tre opzioni seguenti:

* [Adobe Experience Platform Web SDK](overview.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
  <!--* [Server-to-Server API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)-->


>[!NOTE]
>Platform Web SDK e Platform Mobile SDK non richiedono la distribuzione tramite tag; tuttavia, si consiglia di utilizzare i tag per distribuire questi SDK.

Dopo aver completato le lezioni precedenti in questa esercitazione, dovresti inviare dati a Platform Edge Network utilizzando Web SDK. Una volta che i dati sono in Platform Edge Network, puoi abilitare l’inoltro degli eventi e utilizzare una proprietà di inoltro degli eventi per inviare dati a soluzioni non basate su Adobi.

## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Creare una proprietà di inoltro degli eventi
* Collegare una proprietà di inoltro eventi a un flusso di dati dell’SDK web di Platform
* Comprendere le differenze tra elementi dati e regole della proprietà tag e elementi dati e regole della proprietà di inoltro eventi
* Creare un elemento dati per l’inoltro degli eventi
* Configurare una regola per l’inoltro degli eventi
* Convalidare una proprietà di inoltro eventi sta inviando correttamente i dati


## Prerequisiti

* Una licenza software che include l&#39;inoltro di eventi. L’inoltro di eventi è una funzione a pagamento di Data Collection. Per ulteriori informazioni, contatta il team del tuo account di Adobe.
* L’inoltro degli eventi è abilitato nell’organizzazione Experience Cloud.
* Autorizzazione utente per l’inoltro di eventi. (in entrata [Admin Console](https://adminconsole.adobe.com/), nel prodotto Adobe Experience Platform Launch, elementi di autorizzazione per[!UICONTROL Piattaforme] > [!UICONTROL Bordo] e tutti [!UICONTROL Diritti di proprietà]). Una volta concesso, dovresti vedere [!UICONTROL Inoltro eventi] nel menu di navigazione a sinistra dell’interfaccia di Data Collection:
  ![Proprietà inoltro eventi](assets/event-forwarding-menu.png)

* Adobe Experience Platform Web SDK o Mobile SDK configurato per inviare dati a Edge Network. Devi aver completato le seguenti lezioni di questa esercitazione:

   * Configurazione iniziale

      * [Configurare uno schema XDM](configure-schemas.md)
      * [Configurare uno spazio dei nomi delle identità](configure-identities.md)
      * [Configurare uno stream di dati](configure-datastream.md)

   * Configurazione tag

      * [Installare l’estensione Web SDK](install-web-sdk.md)
      * [Creare elementi dati](create-data-elements.md)
      * [Creare identità](create-identities.md)
      * [Creare regole di tag](create-tag-rule.md)
      * [Convalida con Adobe Experience Platform Debugger](validate-with-debugger.md)


## Creare una proprietà di inoltro degli eventi

Per prima cosa, crea una proprietà di inoltro degli eventi:

1. Apri [Interfaccia di Data Collection](https://experience.adobe.com/#/data-collection)
1. Seleziona **[!UICONTROL Inoltro eventi]** dal menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Nuova proprietà]**.
   ![Proprietà inoltro eventi](assets/event-forwarding-new.png)

1. Denomina la proprietà. In questo caso `Server-Side - Web SDK Course`

1. Seleziona **[!UICONTROL Salva]**.
   ![salvataggio proprietà inoltro eventi](assets/event-forwarding-save.png)

## Configurare lo stream di dati

Affinché l’inoltro degli eventi possa utilizzare i dati inviati alla rete Edge, è necessario collegare la proprietà di inoltro degli eventi appena creata allo stesso flusso di dati utilizzato per inviare dati alle soluzioni Adobe.

Per configurare Target nello stream di dati:

1. Vai a [Raccolta dati](https://experience.adobe.com/#/data-collection){target="blank"} Interfaccia
1. Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Flussi di dati]**
1. Seleziona il creato in precedenza `Luma Web SDK: Development Environment` flusso di dati

   ![Seleziona lo stream di dati dell’SDK web Luma](assets/datastream-luma-web-sdk-development.png)

1. Seleziona **[!UICONTROL Aggiungi servizio]**
   ![Aggiungere un servizio allo stream di dati](assets/event-forwarding-datastream-addService.png)
1. Seleziona **[!UICONTROL Inoltro eventi]** come **[!UICONTROL Servizio]**

1. Sotto **[!UICONTROL ID proprietà]** , in questo caso seleziona il nome assegnato alla proprietà di inoltro degli eventi `Server-Side - Web SDK Course`

1. Sotto **[!UICONTROL ID ambiente]** a discesa, seleziona l’ambiente di tag a cui stai collegando l’ambiente di inoltro degli eventi, in questo caso `Development`

   >[!TIP]
   >
   >    Per inviare i dati a un ambiente di inoltro degli eventi che si trova all’esterno dell’organizzazione Adobe, seleziona **[!UICONTROL Immetti manualmente gli ID]** e incolla un ID. L’ID viene fornito quando crei una proprietà di inoltro degli eventi.

1. Seleziona **[!UICONTROL Salva]**.

   ![Abilitazione dello stream di dati di inoltro degli eventi](assets/event-forwarding-datastream-enable.png)

Ripeti questi passaggi per gli stream di dati di staging e produzione quando sei pronto per promuovere le modifiche tramite il flusso di pubblicazione.

## Inoltra i dati dalla rete Edge di Platform a una soluzione non basata su Adobi

In questo esercizio imparerai a impostare un elemento dati per l’inoltro degli eventi, configurare una regola per l’inoltro degli eventi e convalidare utilizzando uno strumento di terza parte denominato [Webhook.site](https://webhook.site/).

>[!NOTE]
>
>Un webhook è un modo per integrare diversi sistemi in tempo semi-reale. [Webhook.site](https://webhook.site/) è uno strumento di terze parti che consente di verificare, testare e automatizzare facilmente (con il generatore di azioni personalizzate visive o WebhookScript) eventuali richieste HTTP o e-mail in arrivo.

>[!IMPORTANT]
>
>Per procedere ulteriormente, devi aver già creato e mappato elementi dati su un oggetto XDM, nonché configurato regole di tag e creato tali modifiche all’interno di una libreria in un ambiente di tag. In caso contrario, fare riferimento al **Configurazione tag** passaggi in [prerequisiti](setup-event-forwarding.md#prerequisites) sezione. Questi passaggi assicurano che i dati vengano inviati alla rete Edge di Platform e da lì puoi configurare una proprietà di inoltro degli eventi per inoltrare i dati a una soluzione non Adobe.


### Creare un elemento dati per l’inoltro degli eventi

L’oggetto XDM configurato in precedenza utilizzando l’estensione tag Platform Web SDK diventa l’origine dati per gli elementi dati in una proprietà di inoltro degli eventi. Come origine dati per l’inoltro degli eventi puoi utilizzare gli stessi dati già configurati nella proprietà tag.

>[!IMPORTANT]
>
>Esiste una differenza di sintassi chiave quando si fa riferimento a campi XDM nell’inoltro degli eventi rispetto ad altri contesti. Per fare riferimento ai dati in una proprietà di inoltro degli eventi, il percorso dell&#39;elemento dati deve includere `arc.event` prefisso:
>
> * `arc` sta per Adobe Response Context (Contesto di risposta Adobe).
> * Ad esempio: `arc.event.xdm.web.webPageDetails.URL`
>
>Se il percorso specificato non è corretto, i dati non vengono raccolti.

In questo esercizio, inoltrerai l’altezza del riquadro di visualizzazione del browser e l’ID Experience Cloud dall’oggetto XDM a un webhook. Il percorso del campo XDM è determinato dallo schema XDM creato durante il [Configurare uno schema XDM](configure-schemas.md) lezione.

>[!TIP]
>
>Puoi anche trovare il percorso dell’oggetto XDM utilizzando gli strumenti di rete del browser web, filtrando per `/ee` richieste, apertura del beacon [!UICONTROL **Payload**] ed eseguire il drilling verso il basso fino alla variabile desiderata. Quindi fare clic con il pulsante destro del mouse e selezionare &quot;Copia percorso proprietà&quot;. Di seguito è riportato un esempio per l’altezza del riquadro di visualizzazione del browser:
> ![Percorso XDM per inoltro eventi](assets/event-forwarding-xdm-path.png)

1. Vai a **[!UICONTROL Inoltro eventi]** proprietà creata di recente

1. Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Elementi dati]**

1. Seleziona per **[!UICONTROL Creare un nuovo elemento dati]**

   ![Inoltro eventi - Nuovo elemento dati](assets/event-forwarding-new-dataelement.png)

1. **[!UICONTROL Nome]** l’elemento dati `environment.browserDetails.viewportHeight`

1. Sotto **[!UICONTROL Estensione]**, congedo `CORE`

1. Sotto **[!UICONTROL Tipo di elemento dati]**, seleziona `Path`

1. Digitare il percorso dell&#39;oggetto XDM contenente l&#39;altezza del riquadro di visualizzazione del browser `arc.event.xdm.environment.browserDetails.viewportHeight`

1. Seleziona **[!UICONTROL Salva]**

   ![Percorso ECID di inoltro eventi](assets/event-forwarding-browser-viewpoirt-height.png)


1. Creare un altro elemento dati

1. **[!UICONTROL Nome]** it `ecid`

1. Sotto **[!UICONTROL Estensione]**, congedo `CORE`

1. Sotto **[!UICONTROL Tipo di elemento dati]**, seleziona `Path`

1. Digitare il percorso dell&#39;oggetto XDM che contiene l&#39;ID Experience Cloud `arc.event.xdm.identityMap.ECID.0.id`

1. Seleziona **[!UICONTROL Salva]**

   ![Percorso ECID di inoltro eventi](assets/event-forwarding-ecid.png)

   >[!CAUTION]
   >
   > Assicurati di includere `arc.event.` nel percorso. Inoltre, accertati di seguire la stessa maiuscola del nome del campo Oggetto XDM: lo spazio dei nomi ECID deve essere in maiuscolo.


   >[!TIP]
   >
   >Quando lavori con il tuo sito web, puoi trovare il percorso dell’oggetto XDM con gli strumenti di rete del browser web, filtrando per `/ee` richieste, apertura del beacon [!UICONTROL **Payload**] ed eseguire il drilling verso il basso fino alla variabile desiderata. Quindi fare clic con il pulsante destro del mouse e selezionare &quot;Copia percorso proprietà&quot;. Di seguito è riportato un esempio per l’altezza del riquadro di visualizzazione del browser:
   > ![Percorso XDM per inoltro eventi](assets/event-forwarding-xdm-path.png)

### Installare l’estensione Adobe Cloud Connector

Per inviare dati a percorsi di terze parti, installi prima il [!UICONTROL Connettore cloud Adobe] estensione.

1. Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra

1. Seleziona la **[!UICONTROL Catalogo]** scheda

1. Cerca **[!UICONTROL Connettore cloud Adobe]**, seleziona **[!UICONTROL Installa]**

   ![Percorso ECID di inoltro eventi](assets/event-forwarding-adobe-cloud-connector.png)

Non è necessaria alcuna configurazione di estensione. Con questa estensione, ora puoi inoltrare i dati a una soluzione non basata su Adobi.

### Creare una regola per l’inoltro degli eventi

Esistono alcune differenze principali tra la configurazione delle regole in una proprietà tag e una regola in una proprietà di inoltro eventi:

* **[!UICONTROL Eventi] E [!UICONTROL Condizioni]**:

   * **Tag**: tutte le regole vengono attivate da un evento che deve essere specificato nella regola, ad esempio, `Library Loaded - Page Top`. Le condizioni sono facoltative.
   * **Inoltro eventi**: si presume che ogni evento inviato a Platform Edge Network sia un trigger per l’inoltro di dati. Pertanto, non vi sono [!UICONTROL Eventi] che deve essere selezionato nelle regole di inoltro degli eventi. Per gestire gli eventi che attivano una regola di inoltro degli eventi, è necessario configurare le condizioni.

* **Tokenizzazione degli elementi dati**:

   * **Tag**: i nomi degli elementi dati sono tokenizzati con un simbolo `%` all&#39;inizio e alla fine del nome dell&#39;elemento dati quando viene utilizzato in una regola. Ad esempio, `%viewportHeight%`.

   * **Inoltro eventi**: i nomi degli elementi dati sono tokenizzati con `{{` all&#39;inizio e `}}` alla fine del nome dell’elemento dati quando viene utilizzato in una regola. Ad esempio, `{{viewportHeight}}`.

* **Sequenza di azioni della regola**:

   * La sezione Azioni di una regola di inoltro degli eventi viene sempre eseguita in sequenza. Quando si salva una regola, occorre assicurarsi che l&#39;ordine delle azioni sia corretto. Questa sequenza di esecuzione non può essere eseguita in modo asincrono come con i tag.

<!--
  * **Tags**: Rule actions can easily be reordered using drag-and-drop functionality.
  * **Event forwarding**: Rule actions are always executed sequentially. Make sure the order of actions is correct when you save a rule.
-->

Per configurare una regola per l’inoltro di dati al webhook, devi prima ottenere il webhook personale:

1. Vai a [Webhook.site](https://webhook.site)

1. Trova **L’URL univoco**, utilizzerai questo come richiesta URL nella regola di inoltro degli eventi

1. Seleziona **[!UICONTROL Copia negli Appunti]**

1. Lascia aperta questa finestra perché potrai convalidare i dati di inoltro degli eventi in tempo reale acquisiti da Webhook

   ![Copia URL webhook](assets/event-forwarding-webhook.png)

1. Torna indietro **[!UICONTROL Raccolta dati]** > **[!UICONTROL Inoltro eventi]** > **[!UICONTROL Regole]** dal menu di navigazione a sinistra

1. Seleziona **[!UICONTROL Crea nuova regola]**

   ![Inoltro eventi: nuova regola](assets/event-forwarding-new-rules.png)

1. Assegna un nome `all events - ad cloud connector - webhook`

1. Aggiungi un&#39;azione

1. Sotto **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Connettore cloud Adobe]**

1. Sotto **[!UICONTROL Tipo di azione]**, seleziona **[!UICONTROL Effettua chiamata di recupero]**

1. Incolla l’URL del webhook in **[!UICONTROL URL]** campo

   ![Copia URL webhook](assets/event-forwarding-rule.png)

1. Sotto **[Parametri query]**, verranno aggiunti entrambi gli elementi dati creati in precedenza.

1. Il giorno **[!UICONTROL Chiave]** tipo di colonna in `viewPortHeight`. Il giorno **[!UICONTROL Valore]** , immetti il `{{environment.browserDetails.viewportHeight}}` elemento dati digitandolo o selezionandolo dall&#39;icona del selettore dell&#39;elemento dati

1. Seleziona [!UICONTROL **+ Aggiungi altro**] per aggiungere un altro parametro di query

1. Il giorno **[!UICONTROL Chiave]** tipo di colonna in `ecid`. Nella colonna Valore immettere il valore `{{ecid}}` elemento dati

1. Seleziona **[!UICONTROL Mantieni modifiche]**

   ![Aggiungi parametro di query](assets/event-forwarding-rule-query-parameter.png)

1. La regola dovrebbe essere simile a quella riportata di seguito

1. Seleziona **[!UICONTROL Salva]**

   ![Salva regola di inoltro degli eventi](assets/event-forwarding-rule-save.png)

### Creare e generare la libreria

Crea una libreria e crea tutte le modifiche nell’ambiente di sviluppo per l’inoltro degli eventi come si farebbe normalmente in una proprietà tag.

>[!NOTE]
>
>Se non hai collegato le proprietà di inoltro degli eventi di staging e produzione allo stream di dati, vedrai l’ambiente di sviluppo come unica opzione per generare una libreria in.

![Salva regola di inoltro degli eventi](assets/event-forwarding-initial-build.png)

## Convalida regola di inoltro eventi

Ora puoi convalidare la proprietà di inoltro degli eventi utilizzando Platform Debugger e Webhook.site:

1. Segui i passaggi per [cambiare la libreria di tag](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) il [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en/men.html) alla proprietà tag dell’SDK web a cui è stata mappata la proprietà di inoltro degli eventi nello stream di dati.

1. Prima di ricaricare la pagina, apri Experienci Platform Debugger **[!UICONTROL Registri]** dal menu di navigazione a sinistra

1. Seleziona la **[!UICONTROL Bordo]** , quindi seleziona **[!UICONTROL Connetti]** per visualizzare le richieste di Platform Edge Network

   ![Sessione rete Edge di inoltro eventi](assets/event-forwarding-edge-session.png)

1. Ricarica la pagina

1. Vedrai ulteriori richieste che ti danno visibilità sulle richieste lato server inviate dalla rete Edge di Platform al WebHook

1. La richiesta su cui concentrarsi sulla convalida è quella che mostra l’URL completamente costruito inviato dalla rete Edge

   ![Debugger inoltro eventi](assets/event-forwarding-debugger.png)


1. Osserva i parametri viewPortHeight e della stringa di query ecid

   ![Inoltro eventi: convalida stringhe di query](assets/event-forwarding-validate-data.png)

1. Corrispondono ai dati visualizzati nell’oggetto XDM

   ![Dati corrispondenti per l’inoltro degli eventi](assets/event-forwarding-matching-data.png)

1. Infine, convalida le corrispondenze dei dati in [Webhook.site](https://webhook.site) nonché visualizzando la finestra del webhook aperta

   ![Dati del sito del webhook di inoltro eventi](assets/event-forwarding-webhook-data.png)

Congratulazioni! Hai configurato l’inoltro degli eventi.

[Successivo: ](conclusion.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)