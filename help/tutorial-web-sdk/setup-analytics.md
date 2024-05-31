---
title: Configurare Adobe Analytics utilizzando Experienci Platform Web SDK
description: Scopri come configurare Adobe Analytics utilizzando Experienci Platform Web SDK. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
solution: Data Collection, Analytics
jira: KT-15408
exl-id: de86b936-0a47-4ade-8ca7-834c6ed0f041
source-git-commit: c5318809bfd475463bac3c05d4f35138fb2d7f28
workflow-type: tm+mt
source-wordcount: '2735'
ht-degree: 1%

---

# Configurare Adobe Analytics con Adobe Experience Platform Web SDK

Scopri come configurare Adobe Analytics utilizzando [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/web-sdk/overview), crea regole di tag per inviare dati ad Adobe Analytics e verifica che Analytics stia acquisendo i dati come previsto.

[Adobe Analytics](https://experienceleague.adobe.com/it/docs/analytics) è un&#39;applicazione leader di settore che ti consente di comprendere i tuoi clienti come persone e gestire la tua attività grazie alle informazioni sul cliente.

![Diagramma da SDK per web ad Adobe Analytics](assets/dc-websdk-aa.png)

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Configurare uno stream di dati per abilitare Adobe Analytics
* Scopri quali campi XDM standard vengono mappati automaticamente sulle variabili di Analytics
* Impostare le variabili di Analytics nell’oggetto dati
* Inviare dati a un’altra suite di rapporti ignorando lo stream di dati
* Convalidare le variabili di Adobe Analytics utilizzando Debugger e Assurance

## Prerequisiti

Per completare questa lezione, devi prima:

* Acquisisci familiarità con Adobe Analytics e accedi ad esso.

* Avere almeno un ID suite per report test/dev. Se non hai una suite per report test/dev che puoi usare per questa esercitazione, [creane uno](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

* Completa le lezioni precedenti nelle sezioni Configurazione iniziale e Configurazione tag di questa esercitazione.

## Configurare lo stream di dati

Platform Web SDK invia i dati dal sito web all’Edge Network di Platform. Lo stream di dati comunica quindi all’Edge Network di Platform le suite di rapporti di Adobe Analytics a cui devono essere inviati i dati.

1. Vai a [Raccolta dati](https://experience.adobe.com/#/data-collection){target="blank"} Interfaccia
1. Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Flussi di dati]**
1. Seleziona il creato in precedenza `Luma Web SDK: Development Environment` flusso di dati

   ![Seleziona lo stream di dati dell’SDK web Luma](assets/datastream-luma-web-sdk-development.png)

1. Seleziona **[!UICONTROL Aggiungi servizio]**
   ![Aggiungere un servizio allo stream di dati](assets/datastream-analytics-addService.png)
1. Seleziona **[!UICONTROL Adobe Analytics]** come **[!UICONTROL Servizio]**
1. Inserisci il **[!UICONTROL ID suite di rapporti]** della suite di rapporti per lo sviluppo
1. Seleziona **[!UICONTROL Salva]**

   ![Analisi del salvataggio dello stream di dati](assets/datastream-add-analytics.png)

   >[!TIP]
   >
   >Aggiunta di più suite di rapporti selezionando **[!UICONTROL Aggiungi suite di rapporti]** equivale all’assegnazione tag per più suite.

>[!WARNING]
>
>In questa esercitazione, puoi configurare solo la suite di rapporti di Adobe Analytics per il tuo ambiente di sviluppo. Quando crei flussi di dati per il tuo sito web, devi creare flussi di dati e suite di rapporti aggiuntivi per gli ambienti di staging e produzione.

## Impostare le variabili di Analytics

Esistono diversi modi per impostare le variabili di Analytics in un’implementazione Web SDK:

1. Mappatura automatica dei campi XDM sulle variabili di Analytics (automatica).
1. Impostare i campi in `data` oggetto (consigliato).
1. Mappa i campi XDM sulle variabili di Analytics nelle regole di elaborazione di Analytics (non più consigliato).
1. Mappa sulle variabili di Analytics direttamente nello schema XDM (non più consigliato).

A partire da maggio 2024, non è più necessario creare uno schema XDM per implementare Adobe Analytics con Platform Web SDK. Il `data` oggetto (e `data.variable` elemento dati creato in questa esercitazione) può essere utilizzato per impostare tutte le variabili di Analytics personalizzate. L’impostazione di queste variabili nell’oggetto dati sarà familiare ai clienti Analytics esistenti, è più efficiente dell’utilizzo dell’interfaccia delle regole di elaborazione e impedisce che dati non necessari occupino spazio in Real-Time Customer Profiles (importante se si dispone di Real-time Customer Data Platform o Journey Optimizer).

### Campi mappati automaticamente

Molti campi XDM vengono mappati automaticamente alle variabili di Analytics. Per un elenco aggiornato delle mappature, consulta [Mappatura delle variabili di Analytics in Adobe Experience Edge](https://experienceleague.adobe.com/en/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars).

Ciò si verifica se _anche se non hai definito uno schema personalizzato_. Experienci Platform Web SDK raccoglie automaticamente alcuni dati e li invia a Platform Edge Network come campi XDM. Ad esempio, Web SDK legge l’URL della pagina corrente e lo invia come `web.webPageDetails.URL`. Questo campo viene inoltrato ad Adobe Analytics e viene automaticamente popolato nei rapporti URL pagina in Adobe Analytics.

Quando implementi Web SDK per Analytics e l’applicazione basata su piattaforma, crei uno schema XDM personalizzato, come descritto in questa esercitazione in [Configurare uno schema](configure-schemas.md) lezione. Alcuni dei campi XDM implementati sono mappati automaticamente alle variabili di Analytics, come descritto in questa tabella:

| Variabili mappate automaticamente da XDM ad Analytics | Variabile Adobe Analytics |
|-------|---------|
| `identitymap.ecid.[0].id` | mid |
| `web.webPageDetails.name` | s.pageName |
| `web.webPageDetails.server` | s.server |
| `web.webPageDetails.siteSection` | s.channel |
| `commerce.productViews.value` | prodView |
| `commerce.productListViews.value` | scView |
| `commerce.checkouts.value` | scCheckout |
| `commerce.purchases.value` | acquisto |
| `commerce.order.currencyCode` | s.currencyCode |
| `commerce.order.purchaseID` | s.purchaseID |
| `productListItems[].SKU` | s.products=;product name;;;; (primario - vedi nota sotto) |
| `productListItems[].name` | s.products=;product name;;;; (fallback - vedi la nota seguente) |
| `productListItems[].quantity` | s.products=;;quantità prodotto;;; |
| `productListItems[].priceTotal` | s.product=;;;;prezzo del prodotto;; |

Le singole sezioni della stringa di prodotto Analytics sono impostate tramite diverse variabili XDM sotto `productListItems` oggetto.

>Dal 18 agosto 2022, `productListItems[].SKU` ha priorità nella mappatura al nome del prodotto nella variabile s.products.
>Il valore impostato su `productListItems[].name` è mappato al nome del prodotto solo se `productListItems[].SKU` non esiste. In caso contrario, non è mappato ed è disponibile nei dati contestuali.
>Non impostare una stringa vuota o null su `productListItems[].SKU`. Questo ha l’effetto indesiderato di mappare al nome del prodotto nella variabile s.products.

### Impostare le variabili nell’oggetto dati

Impostazione delle variabili in `data` L’oggetto è il metodo consigliato per impostare le variabili di Analytics con Web SDK. L’impostazione delle variabili nell’oggetto dati può inoltre sovrascrivere qualsiasi variabile mappata automaticamente.

Prima di tutto, qual è la `data` oggetto? In qualsiasi evento Web SDK è possibile inviare due oggetti con dati personalizzati, il `data` oggetto e `xdm` oggetto. Entrambi vengono inviati all’Edge Network di Platform, ma solo `xdm` L’oggetto viene inviato al set di dati Experienci Platform. Proprietà in `data` L&#39;oggetto può essere mappato sul server Edge a `xdm` I campi che utilizzano la funzione Preparazione per la raccolta dati, ma che in caso contrario non vengono inviati ad Experienci Platform. Questo lo rende un modo ideale per inviare dati ad applicazioni come Analytics, che non sono native di Experienci Platform.

Di seguito sono riportati i due oggetti in una chiamata Web SDK generica:

![dati e oggetti xdm](assets/analytics-data-object-intro.png)

Adobe Analytics è configurato per cercare eventuali proprietà in `data.__adobe.analytics` e utilizzarli per le variabili di Analytics.

Ora facciamo questo.

Utilizziamo `data.variable` elemento dati t


<!--


### Map to Analytics variables with processing rules

All fields in the XDM schema become available to Adobe Analytics as Context Data Variables with the following prefix `a.x.`. For example, `a.x.web.webinteraction.region`

In this exercise, you map one XDM variable to a prop. Follow these same steps for any custom mapping that you must do for any `eVar`, `prop`, `event`, or variable accessible via Processing Rules.

1. Go to the Analytics interface
1. Go to [!UICONTROL Admin] > [!UICONTROL Admin Tools] > [!UICONTROL Report Suites ]
1. Select the dev/test report suite that you are using for the tutorial > [!UICONTROL Edit Settings] > [!UICONTROL General] > [!UICONTROL Processing Rules]

    ![Analytics Purchase](assets/analytics-process-rules.png)   

1. Create a rule to **[!UICONTROL Overwrite value of]** `[!UICONTROL Product SKU (prop1)]` to `a.x.productlistitems.0.sku`. Remember to add a note about why you are creating the rule and name your rule title. Select **[!UICONTROL Save]**

    ![Analytics Purchase](assets/analytics-set-processing-rule.png)   

    >[!IMPORTANT]
    >
    >The first time you map to a processing rule, the UI does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.

### Map to Analytics variables using the Adobe Analytics field group

An alternative to processing rules is to map to Analytics variables in the XDM schema using the `Adobe Analytics ExperienceEvent Template` field group. This approach has gained popularity because many users find it simpler than configuring processing rules, however, by increasing the size of the XDM payload it could in turn increase the profile size in other applications like Real-Time CDP.

To add the `Adobe Analytics ExperienceEvent Template` field group to your schema:

1. Open the [Data Collection](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Select **[!UICONTROL Schemas]** from the left navigation
1. Make sure you are in the sandbox you are using from the tutorial
1. Open your `Luma Web Event Data` schema
1. In the **[!UICONTROL Field Groups]** section, select **[!UICONTROL Add]**
1. Find the `Adobe Analytics ExperienceEvent Template` field group and add it to your schema


Now, set a merchandising eVar in the product string. With the `Adobe Analytics ExperienceEvent Template` field group, you are able to map variables to merchandising eVars or events within the product string. This is also known as setting **Product Syntax Merchandising**. 

1. Go back to your tag property

1. Open the rule `ecommerce - library loaded - set product details variables - 20`

1. Open the **[!UICONTROL Set Variable]** action

1. Select to open `_experience > analytics > customDimensions > eVars > eVar1`

1. Set the **[!UICONTROL Value]** to `%product.productInfo.title%`

1. Select **[!UICONTROL Keep Changes]**

    ![Product SKU XDM object Variable](assets/set-up-analytics-product-merchandising.png)

1. Select **[!UICONTROL Save]** to save the rule

As you just saw, basically all of the Analytics variables can be set in the `Adobe Analytics ExperienceEvent Template` field group.

>[!NOTE]
>
> Notice the `_experience` object under `productListItems` > `Item 1`. Setting any variable under this [!UICONTROL object] sets Product Syntax eVars or Events.

-->

## Inviare dati a una suite di rapporti diversa

Puoi modificare i dati della suite di rapporti di Adobe Analytics a cui vengono inviati i visitatori quando si trovano su determinate pagine. Questo richiede una configurazione sia nello stream di dati che in una regola.

### Configurare lo stream di dati per una sostituzione della suite di rapporti

Per configurare l’impostazione di sostituzione della suite di rapporti di Adobe Analytics nello stream di dati:

1. Apri lo stream di dati
1. Modifica il **[!UICONTROL Adobe Analytics]** mediante l&#39;apertura della ![altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) menu e selezione **[!UICONTROL Modifica]**

   ![Sovrascrivere lo stream di dati](assets/datastream-edit-analytics.png)

1. Seleziona la **[!UICONTROL Opzioni avanzate]** per aprire **[!UICONTROL Sostituzioni suite di rapporti]**

1. Seleziona le suite di rapporti da ignorare. In questo caso, `Web SDK Course Dev` e `Web SDK Course Stg`

1. Seleziona **[!UICONTROL Salva]**

   ![Sovrascrivere lo stream di dati](assets/analytics-datastreams-edit-adobe-analytics-configurations-report-suites.png)


### Configurare una regola per una sostituzione della suite di rapporti

Creiamo una regola per inviare una chiamata aggiuntiva di visualizzazione della pagina a una suite di rapporti diversa. Utilizza la funzione di sostituzione dello stream di dati per modificare la suite di rapporti per una pagina utilizzando **[!UICONTROL Invia evento]** Azione.

1. Crea una nuova regola, denominala `homepage - library loaded - AA report suite override - 51`

1. Seleziona il segno più sotto **[!UICONTROL Evento]** per aggiungere un nuovo trigger

1. Sotto **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Core]**

1. Sotto **[!UICONTROL Tipo di evento]**, seleziona **[!UICONTROL libreria caricata]**

1. Seleziona per aprire **[!UICONTROL Opzioni avanzate]**, digitare `51`. In questo modo la regola viene eseguita dopo il `all pages - library loaded - send event - 50` che imposta l&#39;XDM della linea di base con **[!UICONTROL Aggiorna variabile]** tipo di azione.

   ![Override suite di rapporti di Analytics](assets/set-up-analytics-rs-override.png)

1. Sotto **[!UICONTROL Condizioni]**, seleziona per **[!UICONTROL Aggiungi]**

1. Esci **[!UICONTROL Tipo di logica]** as **[!UICONTROL Normale]**

1. Esci **[!UICONTROL Estensioni]** as **[!UICONTROL Core]**

1. Seleziona **[!UICONTROL Tipo di condizione]** as **[!UICONTROL Percorso senza stringa di query]**

1. A destra, lascia il **[!UICONTROL Regex]** interruttore disabilitato

1. Sotto **[!UICONTROL path è uguale a]** set `/content/luma/us/en.html`. Per il sito di dimostrazione Luma, assicura che la regola venga attivata solo sulla pagina Home

1. Seleziona **[!UICONTROL Mantieni modifiche]**

   ![Condizione di esclusione suite di rapporti di Analytics](assets/set-up-analytics-override-condition.png)

1. Sotto **[!UICONTROL Azioni]** seleziona **[!UICONTROL Aggiungi]**

1. Come **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Come **[!UICONTROL Tipo di azione]**, seleziona **[!UICONTROL Invia evento]**

1. Come **[!UICONTROL Tipo]**, seleziona `web.webpagedetails.pageViews`

1. Come **[!UICONTROL Dati XDM]**, seleziona la `xdm.variable.content` elemento dati creato in [Creare elementi dati](create-data-elements.md) lezione

   ![Sostituzione dello stream di dati di Analytics](assets/set-up-analytics-datastream-override-1.png)

1. Scorri verso il basso fino a **[!UICONTROL Override delle configurazioni dello stream di dati]** sezione

1. Lascia **[!UICONTROL Sviluppo]** scheda selezionata.

   >[!TIP]
   >
   >    Questa scheda determina in quale ambiente di tag si verifica l’esclusione. Per questo estratto, specifichi solo l’ambiente di sviluppo, ma quando lo distribuisci in produzione ricorda di farlo anche nel **[!UICONTROL Produzione]** ambiente.


1. Seleziona la **[!UICONTROL Datastream]**, in questo caso `Luma Web SDK: Development Environment`

1. Sotto **[!UICONTROL Suite di rapporti]**, seleziona il sito di report che desideri utilizzare per la sostituzione. In questo caso, `tmd-websdk-course-stg`.

1. Seleziona **[!UICONTROL Mantieni modifiche]**

1. E **[!UICONTROL Salva]** regola

   ![Sostituzione dello stream di dati di Analytics](assets/analytics-tags-report-suite-override.png)


## Creare l’ambiente di sviluppo

Aggiungi nuovi elementi dati e regole al tuo `Luma Web SDK Tutorial` libreria di tag e ricreare l’ambiente di sviluppo.

Congratulazioni! Il passaggio successivo consiste nel convalidare l’implementazione di Adobe Analytics tramite Experienci Platform Web SDK.

## Convalidare Adobe Analytics con Debugger

Scopri come verificare che Adobe Analytics acquisisca ECID, visualizzazioni di pagina, la stringa di prodotto e gli eventi di e-commerce con la funzione Edge Trace di Experienci Platform Debugger.

In [Debugger](validate-with-debugger.md) lezione, hai imparato a verificare la richiesta XDM lato client con Platform Debugger e la console per sviluppatori del browser, in modo simile a come si esegue il debug di un’ `AppMeasurement.js` Implementazione di Analytics. Hai anche imparato a convalidare le richieste lato server di Edge Network di Platform inviate alle applicazioni Adobe e a visualizzare un payload completamente elaborato utilizzando Assurance.

Per verificare che Analytics acquisisca correttamente i dati tramite Experienci Platform Web SDK, devi effettuare due passaggi ulteriori:

1. Convalida il modo in cui i dati vengono elaborati dall’oggetto XDM nell’Edge Network di Platform, utilizzando la funzione Edge Trace di Experienci Platform Debugger
1. Convalidare il modo in cui i dati vengono completamente elaborati da Analytics utilizzando Adobe Experience Platform Assurance

### Convalida dell’ID Experience Cloud

1. Vai a [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}
1. Seleziona il pulsante di accesso in alto a destra e utilizza le credenziali u: test@adobe.com p: test per autenticare
1. Apri Experienci Platform Debugger e [modifica la proprietà tag sul sito con la tua proprietà di sviluppo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)


1. Per abilitare Edge Trace, passa a Debugger di Experienci Platform e, nel menu di navigazione a sinistra, seleziona **[!UICONTROL Registri]**, quindi seleziona la **[!UICONTROL Bordo]** e seleziona **[!UICONTROL Connetti]**

   ![Connetti traccia spigolo](assets/analytics-debugger-edgeTrace.png)

1. Per ora sarà vuoto

   ![Traccia bordi connessi](assets/analytics-debugger-edge-connected.png)

1. Aggiorna la pagina Luma e controlla di nuovo Debugger Experience Platform: dovresti vedere i dati arrivare. La riga che inizia con **[!UICONTROL Mappatura automatica di Analytics]** è il beacon di Adobe Analytics
1. Seleziona per aprire entrambi `[!UICONTROL mappedQueryParams]` e il secondo a discesa per visualizzare le variabili di Analytics

   ![Traccia Edge beacon di Analytics](assets/analytics-debugger-edge-analytics.png)

   >[!TIP]
   >
   >Il secondo elenco a discesa corrisponde all’ID suite di rapporti di Analytics a cui stai inviando i dati. Deve corrispondere alla tua suite di rapporti, non a quella nella schermata.

1. Scorri verso il basso per trovare `[!UICONTROL c.a.x.identitymap.ecid.[0].id]`. È una variabile di dati contestuali che acquisisce ECID
1. Continua a scorrere verso il basso fino a visualizzare il pannello Analytics `[!UICONTROL mid]` variabile. Entrambi gli ID corrispondono all’ID Experience Cloud del dispositivo.
1. Sul sito Luma,

   ![ECID di Analytics](assets/analytics-debugger-ecid.png)

   >[!NOTE]
   >
   >Dopo l&#39;accesso, attendere alcuni istanti per convalidare l&#39;ID autenticato `112ca06ed53d3db37e4cea49cc45b71e` per l’utente **`test@adobe.com`** viene acquisito anche in `[!UICONTROL c.a.x.identitymap.lumacrmid.[0].id]`

### Convalida dell’override della suite di rapporti

Sopra hai configurato una sostituzione dello stream di dati per [Home page Luma](https://luma.enablementadobe.com/content/luma/us/en.html).  Per convalidare questa configurazione

1. Cerca una riga con **[!UICONTROL Configurazione dello stream di dati dopo l’applicazione della sostituzione]**. Qui puoi trovare la suite di rapporti principale e le suite di rapporti aggiuntive configurate per le sostituzioni della suite di rapporti.

   ![Convalida elenco di sostituzione suite di rapporti di Analytics](assets/aep-debugger-datastream-override.png)

1. Scorri verso il basso fino alla riga che inizia con **[!UICONTROL Mappatura automatica di Analytics]**  e verifica che `[!UICONTROL reportSuiteIds]` mostra la suite di rapporti specificata nelle configurazioni di sostituzione

   ![Convalida della chiamata di sostituzione della suite di rapporti di Analytics](assets/aep-debugger-analytics-report-suite-override.png)

### Convalida delle visualizzazioni della pagina del contenuto

Vai a una pagina di prodotto come [Pagina prodotto Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02).  Verifica che le visualizzazioni della pagina di contenuto siano acquisite da Analytics.

1. Cerca `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`.
1. Scorri verso il basso per visualizzare `[!UICONTROL gn]` variabile. È la sintassi dinamica di Analytics per `[!UICONTROL s.pageName]` variabile. Acquisisce il nome della pagina dal livello dati.

   ![Stringa di prodotto di Analytics](assets/analytics-debugger-edge-page-view.png)

### Convalida della stringa di prodotto e degli eventi di e-commerce

Poiché ti trovi già in una pagina di prodotto, questo esercizio continua a utilizzare la stessa traccia Edge per convalidare i dati del prodotto acquisiti da Analytics. Sia la stringa di prodotto che gli eventi di e-commerce vengono mappati automaticamente le variabili XDM su Analytics. Se hai mappato al corretto `productListItem` Variabile XDM durante [configurazione di uno schema XDM per Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics), l’Edge Network di Platform si occupa della mappatura dei dati sulle variabili di analisi appropriate.

**Verifica innanzitutto che il `Product String` è impostato**

1. Cerca `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. La variabile acquisisce il valore dell&#39;elemento dati mappato al `productListItems.item1.sku` all&#39;inizio di questa lezione
1. Cerca anche `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL _experience.analytics.customdimensions.evars.evar1]`. La variabile acquisisce il valore dell’elemento dati su cui hai eseguito il mapping `productListItems.item1._experience.analytics.customdimensions.evars.evar1`
1. Scorri verso il basso per visualizzare `[!UICONTROL pl]` variabile. È la sintassi dinamica della variabile della stringa di prodotto Analytics
1. Il nome del prodotto dal livello dati è mappato sia al `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]` e `[!UICONTROL product]` parametro della stringa prodotti.  Inoltre, il titolo del prodotto dal livello dati viene mappato su evar1 merchandising nella stringa prodotti.

   ![Stringa di prodotto di Analytics](assets/analytics-debugger-prodstring.png)

   La traccia Edge tratta `commerce` eventi leggermente diversi rispetto a `productList` dimensioni. Non viene visualizzata una variabile di dati contestuali mappata nello stesso modo in cui viene visualizzato il nome del prodotto mappato a `[!UICONTROL c.a.x.productlistitem.[0].name]` sopra. La traccia Edge mostra invece la mappatura automatica finale dell’evento in Analytics `event` variabile. Platform Edge Network lo mappa di conseguenza, purché mappato sul modello XDM corretto `commerce` variabile durante [configurazione dello schema per Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics); in questo caso il `commerce.productViews.value=1`.

1. Nella finestra di Experienci Platform Debugger, scorri verso il basso fino a `[!UICONTROL events]` variabile, è impostato su `[!UICONTROL prodView]`

1. Nota anche `[!UICONTROL c.a.x.eventType]` è impostato su `commerce.productViews` da quando ti trovi su una pagina di prodotto.

   >[!TIP]
   >
   > Il `ecommerce - pdp library loaded - AA (order 20)` la regola sta sovrascrivendo il valore di `eventType` impostato da `all pages global content variables - library loaded - AA (order 1)` regola impostata per essere attivata successivamente nella sequenza


   ![Visualizzazione prodotto di Analytics](assets/analytics-debugger-prodView.png)

**Convalida che gli altri eventi di e-commerce e le stringhe di prodotto siano impostati per Analytics**

1. Aggiungi [Orologio Didi Sport](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) al carrello
1. Vai a [Pagina carrello](https://luma.enablementadobe.com/content/luma/us/en/user/cart.html), verifica traccia spigolo per

   * `eventType` imposta su `commerce.productListViews`
   * `[!UICONTROL events: "scView"]`, e
   * la stringa di prodotto è impostata

   ![Vista carrello di Analytics](assets/analytics-debugger-cartView.png)

1. Procedi con il pagamento, controlla Edge Trace per

   * `eventType` imposta su `commerce.checkouts`
   * `[!UICONTROL events: "scCheckout"]`, e
   * la stringa di prodotto è impostata

   ![Pagamento Analytics](assets/analytics-debugger-checkout.png)

1. Compila solo il **Nome** e **Cognome** campi nel modulo di spedizione e selezionare **Continua**. Nella pagina successiva, seleziona **Inserisci ordine**
1. Nella pagina di conferma, seleziona Edge Trace per

   * `eventType` imposta su `commerce.purchases`
   * Evento di acquisto in fase di impostazione `[!UICONTROL events: "purchase"]`
   * Variabile codice valuta impostata `[!UICONTROL cc: "USD"]`
   * ID acquisto impostato in `[!UICONTROL pi]`
   * Stringa di prodotto `[!UICONTROL pl]` impostazione del nome, della quantità e del prezzo del prodotto

   ![Acquisto Analytics](assets/analytics-debugger-purchase.png)



## Convalidare Adobe Analytics utilizzando Assurance

Adobe Experience Platform Assurance consente di ispezionare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze con il sito web e l’app mobile.

Nell’esercizio precedente hai verificato che Adobe Analytics acquisisce l’ECID, le visualizzazioni di pagina, la stringa di prodotto e gli eventi di e-commerce con la funzione Edge Trace di Experienci Platform Debugger.  Successivamente, convalida gli stessi eventi utilizzando Adobe Experience Platform Assurance, un’interfaccia alternativa per accedere agli stessi dati in Edge Trace.

Come hai imparato nella [Assurance](validate-with-assurance.md) In questa lezione sono disponibili diversi modi per avviare una sessione Assurance. Poiché hai già aperto un Adobe Experience Platform Debugger con una sessione Edge Trace avviata dall’ultimo esercizio, ti consigliamo di accedere ad Assurance tramite il debugger:
![Garanzia tramite la raccolta dati di Adobe Experience Platform](assets/assurance-open-aep-debugger.png)

All&#39;interno del **[!UICONTROL &quot;Esercitazione Web SDK 3&quot;]** Invio sessione di garanzia **[!UICONTROL &quot;hitdebugger&quot;]** nella barra di ricerca degli eventi per filtrare i risultati in base ai dati post-elaborati di Adobe Analytics.
![Dati post-elaborati di analisi dell’Adobe della garanzia](assets/assurance-hitdebugger.png)

### Convalida dell’ID Experience Cloud

Per verificare che Adobe Analytics acquisisca l’ECID, seleziona un beacon e apri il Payload.  Il fornitore per questo beacon deve essere **[!UICONTROL com.adobe.analytics.hitdebugger]**
![Convalida Adobe Analytics con Assurance](assets/assurance-hitdebugger-payload.png)

Quindi scorri verso il basso fino a **[!UICONTROL mcvisId]** per verificare che l’ECID sia stato acquisito correttamente
![Convalida dell’ID Experience Cloud con Assurance](assets/assurance-hitdebugger-mcvisId.png)

### Convalida delle visualizzazioni della pagina del contenuto

Utilizzando lo stesso beacon, verifica che le visualizzazioni della pagina di contenuto siano mappate sulla variabile Adobe Analytics corretta.
Scorri verso il basso fino a **[!UICONTROL pageName]** per verificare che `Page Name` viene acquisito correttamente
![Convalida del nome della pagina con Assurance](assets/assurance-hitdebugger-content-pagename.png)

### Convalida della stringa di prodotto e degli eventi di e-commerce

Seguendo gli stessi casi di utilizzo di convalida utilizzati per la convalida con Experienci Platform Debugger, continua a utilizzare lo stesso beacon per convalidare `Ecommerce Events` e `Product String`.

1. Cerca payload in cui **[!UICONTROL Eventi]** contain `prodView`
   ![Convalida della stringa di prodotto con Assurance](assets/assurance-hitdebugger-prodView-event.png)
1. Scorri verso il basso fino a **[!UICONTROL product-string]** per convalidare `Product String`.
   * Osserva `Product SKU` e `Merchandizing eVar1`.
1. Scorri verso il basso e verifica che `prop1`, configurato utilizzando le regole di elaborazione nella sezione precedente, contiene `Product SKU`\
   ![Stringa di prodotto con convalida delle variabili merchandizing con Assurance](assets/assurance-hitdebugger-prodView-productString-merchVar.png)

Continua a convalidare la tua implementazione rivedendo il carrello, gli eventi di pagamento e gli eventi di acquisto.

1. Cerca payload in cui **[!UICONTROL Eventi]** contain `scView` e convalida la stringa di prodotto.
   ![Convalida della stringa di prodotto con Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Cerca payload in cui **[!UICONTROL Eventi]** contain `scCheckout` e convalida la stringa di prodotto.
   ![Convalida della stringa di prodotto con Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Cerca payload in cui **[!UICONTROL Eventi]** contain `purchase`
   ![Convalida della stringa di prodotto con Assurance](assets/assurance-hitdebugger-purchase-event.png)
1. Durante la convalida del `purchase` evento, tieni presente che `Product String` deve contenere `Product SKU`, `Product Quantity` , e `Product Total Price`.
1. Inoltre, per `purchase` verificare che `purchase-id` e/o `purchaseId` sono impostati


Congratulazioni! Ce l&#39;hai fatta! Questa è la fine della lezione e ora sei pronto a implementare Adobe Analytics con Platform Web SDK per il tuo sito Web.

[Successivo: ](setup-audience-manager.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
