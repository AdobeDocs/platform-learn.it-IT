---
title: Eventi
description: Scopri come raccogliere i dati evento in un’app mobile.
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Eventi

Scopri come tenere traccia degli eventi in un’app mobile.

L’estensione Edge Network fornisce un’API per l’invio di eventi Experience a Platform Edge Network. Un evento esperienza è un oggetto che contiene dati conformi alla definizione dello schema ExperienceEvent XDM. In modo più semplice, acquisiscono ciò che le persone fanno nella tua app mobile. Una volta ricevuti i dati da Platform Edge Network, possono essere inoltrati alle applicazioni e ai servizi configurati nel datastream, come Adobe Analytics e Experience Platform. Ulteriori informazioni sulle [Eventi esperienza](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk) nella documentazione del prodotto.

## Prerequisiti

* Aggiornamento di PodFile con gli SDK richiesti.
* Estensioni registrate in AppDelegate.
* MobileCore è stato configurato per utilizzare l&#39;AppId di sviluppo.
* SDK importati.
* Creazione ed esecuzione dell&#39;app con le modifiche precedenti.

## Finalità di apprendimento

In questa lezione:

* Scopri come strutturare i dati XDM in base a uno schema.
* Invia un evento XDM basato su un gruppo di campi standard.
* Invia un evento XDM basato su un gruppo di campi personalizzato.
* Invia un evento di acquisto XDM.
* Convalida con affidabilità.

## Creazione di un evento esperienza

L’estensione Adobe Experience Platform Edge può inviare eventi che seguono uno schema XDM definito in precedenza ad Adobe Experience Platform Edge Network.

Il processo è così...

1. Identifica l’interazione con l’app mobile che stai tentando di tracciare.

1. Rivedi lo schema e identifica l’evento appropriato.

1. Rivedi lo schema e identifica eventuali campi aggiuntivi da utilizzare per descrivere l’evento.

1. Crea e compila l’oggetto dati.

1. Crea e invia un evento.

1. Convalida.

Vediamo un paio di esempi.

### Esempio n. 1 - gruppi di campi standard

Rivedi l’esempio seguente senza provare a implementarlo nell’app di esempio:

1. Nello schema, identifica l’evento che stai tentando di raccogliere, in questo esempio stiamo monitorando una visualizzazione di prodotto.
   ![schema visualizzazione prodotto](assets/mobile-datacollection-prodView-schema.png)

1. Inizia a costruire l’oggetto:

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
       "commerce": [
           "productViews": [
           "value": 1
           ]
       ]
   ]
   ```

   * eventType: Descrive l&#39;evento che si è verificato, utilizza un [valore noto](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possibile.
   * commerce.productViews.value: Specifica il valore numerico dell&#39;evento. Se è un valore booleano (o &quot;Contatore&quot; in Adobe Analytics), il valore sarà sempre 1. Se si tratta di un evento numerico o valutario, il valore può essere > 1.

1. Nello schema, identifica eventuali dati aggiuntivi associati all’evento. In questo esempio, includi `productListItems` che è un set standard di campi utilizzati con eventi relativi all’e-commerce:
   ![schema voci elenco prodotti](assets/mobile-datacollection-prodListItems-schema.png)
   * Tieni presente che `productListItems` è un array che consente di fornire più prodotti.

1. Espandere l&#39;oggetto xdmData per includere dati supplementari:

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
           "commerce": [
           "productViews": [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name":  productName,
               "SKU": sku,
               "priceTotal": priceString,
               "quantity": 1
           ]
       ]
   ]
   ```

1. Utilizza la struttura dati per creare un `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Invia l’evento e i dati a Platform Edge Network:

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### Esempio n. 2 - gruppi di campi personalizzati

Rivedi l’esempio seguente senza provare a implementarlo nell’app di esempio:

1. Nello schema, identifica l&#39;evento che stai tentando di raccogliere. In questo esempio, tieni traccia di un’interazione con l’app costituita da un evento e un nome di Azione app.
   ![schema di interazione dell&#39;app](assets/mobile-datacollection-appInteraction-schema.png)

1. Inizia a costruire l’oggetto.

   >[!NOTE]
   >
   >  I gruppi di campi standard iniziano sempre nella directory principale dell’oggetto.
   >
   >  I gruppi di campi personalizzati iniziano sempre con un oggetto unico nell&#39;organizzazione di Experience Cloud, in questo esempio &quot;_techmarketingdemos&quot;.

   ```swift
   var xdmData: [String: Any] = [
   "_techmarketingdemos": [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
                   ]
               ]
           ]
       ]
   ]
   ```

   O in alternativa...

   ```swift
   var xdmData: [String: Any] = [:]
   xdmData["_techmarketingdemos"] = [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
               ]
           ]
       ]
   ]
   ```

1. Utilizza la struttura dati per creare un `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Invia l’evento e i dati a Platform Edge Network.

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### Aggiunta del tracciamento della visualizzazione a schermo all’app Luma

Gli esempi di cui sopra hanno, si spera, spiegato il processo di riflessione durante la costruzione di un oggetto dati XDM. Ora aggiungeremo il tracciamento della visualizzazione a schermo nell’app Luma.

1. Passa a `Home.swift`.
1. Aggiungi il codice seguente a `viewDidAppear(...)`.

   ```swift
           let stateName = "luma: content: ios: us: en: home"
           var xdmData: [String: Any] = [:]
           //Page View
           xdmData["_techmarketingdemos"] = [
               "appInformation": [
                   "appStateDetails": [
                       "screenType": "App",
                       "screenName": stateName,
                       "screenView": [
                           "value": 1
                       ]
                   ]
               ]
           ]
           let experienceEvent = ExperienceEvent(xdm: xdmData)
           Edge.sendEvent(experienceEvent: experienceEvent)
   ```

1. Ripeti per ogni schermata dell’app, aggiornamento `stateName` come vai.



### Convalida

1. Consulta la sezione [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo a Assurance.
1. Esegui l’azione e cerca il `hitReceived` evento dal `com.adobe.edge.konductor` fornitore.
1. Seleziona l’evento e rivedi i dati XDM nel `messages` oggetto.
   ![convalida della raccolta dati](assets/mobile-datacollection-validation.png)

### Esempio n. 3 - acquisto

In questo esempio, si supponga che l’utente abbia effettuato correttamente il seguente acquisto:

* Prodotto #1 - Tappetino Yoga.
   * $ 49,99 x1
   * SKU: 5829
* Prodotto #2 - Bottiglia d&#39;acqua.
   * $ 10,00 x3
   * SKU: 9841
* Totale ordine: $ 79,99
* Id Ordine Univoco: 298234720
* Tipo di pagamento: Carta di credito Visa
* Id Transazione Pagamento Univoco: 847361

#### Schema

Di seguito sono riportati i campi dello schema correlati da utilizzare:

* eventType: &quot;commerce.purchase&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails (personalizzato)

>[!TIP]
>
>I gruppi di campi personalizzati vengono sempre inseriti sotto l&#39;identificatore dell&#39;organizzazione Experience Cloud.
>
>&quot;_techmarketingdemos&quot; viene sostituito con il valore univoco dell&#39;organizzazione.

![schema di acquisto](assets/mobile-datacollection-purchase-schema.png)


#### Codice

Ecco come creare e inviare l’oggetto XDM nell’app.

```swift
let stateName = "luma: content: ios: us: en: orderconfirmation"
let currencyCode = "USD"
let orderTotal = "79.99"
let paymentType = "Visa Credit Card"
let orderId = "298234720"
let paymentTransactionId = "847361"
var xdmData: [String: Any] = [
  "eventType": "commerce.purchases",
  "commerce": [
    "purchases": [
      "value": 1
    ],
    "order": [
      "currencyCode": currencyCode,
      "priceTotal": orderTotal,
      "purchaseID": orderId,
      "purchaseOrderNumber": orderId,
      "payments": [ //Assuming only 1 payment type is used
        [
          "currencyCode": currencyCode,
          "paymentAmount": orderTotal,
          "paymentType": paymentType,
          "transactionID": paymentTransactionId
        ]
      ]
    ]
  ],
  "productListItems": [
      [
          "name":  "Yoga Mat",
          "SKU": "5829",
          "priceTotal": "49.99",
          "quantity": 1
      ],
      [
        "name":  "Water Bottle",
        "SKU": "9841",
        "priceTotal": "30.00",
        "quantity": 3
      ]
  ]
]

//Custom field group
xdmData["_techmarketingdemos"] = [
  "appInformation": [
    "appStateDetails": [
      "screenType": "App",
      "screenName": stateName,
      "screenView": [
        "value": 1
      ]
    ]
  ]
]
let experienceEvent = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: experienceEvent)
```

>[!NOTE]
>
>Per chiarezza, tutti i valori sono codificati in modo fisso. In una situazione reale, i valori verrebbero popolati in modo dinamico.


### Implementazione nell’app Luma

Dovresti disporre di tutti gli strumenti per iniziare ad aggiungere la raccolta dati all’app di esempio Luma. Di seguito è riportato un elenco dei requisiti di tracciamento ipotetici che puoi seguire.

* Monitora ogni visualizzazione schermo.
   * Campi dello schema: screenType, screenName, screenView
* Tieni traccia delle azioni non commerciali.
   * Campi dello schema: appInteraction.name, appAction
* Azioni commerciali:
   * Pagina di prodotto: productViews
   * Aggiungi al carrello: productListAdd
   * Rimuovi dal carrello: productListRemovals
   * Inizio pagamento: checkout
   * Visualizza carrello: productListViews
   * Aggiungi alla lista dei desideri: saveForLaters
   * Acquisto: acquisti, ordine

>[!TIP]
>
>Consulta la sezione [app completamente implementata](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) per ulteriori esempi.

### Convalida

1. Consulta la sezione [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo a Assurance.

1. Esegui l’azione e cerca il `hitReceived` evento dal `com.adobe.edge.konductor` fornitore.

1. Seleziona l’evento e rivedi i dati XDM nel `messages` oggetto.
   ![convalida della raccolta dati](assets/mobile-datacollection-validation.png)

## Inviare eventi ad Analytics e Platform

Dopo aver raccolto gli eventi e averli inviati a Platform Edge Network, questi verranno inviati alle applicazioni e ai servizi configurati nel tuo [datastream](create-datastream.md). Nelle lezioni successive, mapperai questi dati su [Adobe Analytics](analytics.md) e [Adobe Experience Platform](platform.md).

Avanti: **[WebViews](web-views.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)