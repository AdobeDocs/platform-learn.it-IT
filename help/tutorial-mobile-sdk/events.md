---
title: Eventi
description: Scopri come raccogliere i dati di un evento in un’app mobile.
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 1%

---

# Eventi

Scopri come tracciare gli eventi in un’app mobile.

L’estensione Edge Network fornisce un’API per inviare eventi esperienza a Platform Edge Network. Un Experience Event è un oggetto che contiene dati conformi alla definizione dello schema XDM ExperienceEvent. Più semplicemente, acquisiscono ciò che le persone fanno nella tua app mobile. Una volta ricevuti i dati da Platform Edge Network, questi possono essere inoltrati alle applicazioni e ai servizi configurati nel flusso di dati, come Adobe Analytics e Experience Platform. Ulteriori informazioni su [Eventi esperienza](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) nella documentazione del prodotto.

## Prerequisiti

* PodFile aggiornato con gli SDK richiesti.
* Estensioni registrate in AppDelegate.
* MobileCore configurato per utilizzare l&#39;AppId di sviluppo.
* SDK importati.
* L&#39;app è stata creata ed eseguita correttamente con le modifiche precedenti.

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Scopri come strutturare i dati XDM in base a uno schema.
* Invia un evento XDM basato su un gruppo di campi standard.
* Invia un evento XDM basato su un gruppo di campi personalizzato.
* Invia un evento di acquisto XDM.
* Convalida con Assurance.

## Creazione di un evento esperienza

L’estensione Adobe Experience Platform Edge può inviare a Adobe Experience Platform Edge Network eventi che seguono uno schema XDM definito in precedenza.

Il processo è simile a questo...

1. Identifica l’interazione con l’app mobile che stai tentando di tracciare.

1. Esamina lo schema e identifica l’evento appropriato.

1. Esamina lo schema e identifica eventuali campi aggiuntivi da utilizzare per descrivere l’evento.

1. Costruisci e popola l’oggetto dati.

1. Crea e invia evento.

1. Convalida.

Vediamo un paio di esempi.

### Esempio #1: gruppi di campi standard

Rivedi l’esempio seguente senza provare a implementarlo nell’app di esempio:

1. Nello schema, identifica l’evento che stai tentando di raccogliere; in questo esempio stiamo tracciando una visualizzazione di prodotto.
   ![schema di visualizzazione prodotto](assets/mobile-datacollection-prodView-schema.png)

1. Inizia a costruire l&#39;oggetto:

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

   * eventType: descrive l’evento che si è verificato, utilizza un [valore noto](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possibile.
   * commerce.productViews.value: specifica il valore numerico dell’evento. Se è un valore booleano (o &quot;Contatore&quot; in Adobe Analytics), il valore sarà sempre 1. Se è un evento numerico o di valuta, il valore può essere > 1.

1. Nello schema, identifica eventuali dati aggiuntivi associati all’evento. In questo esempio, includi `productListItems` che è un set standard di campi utilizzati con eventi relativi al commercio:
   ![schema elementi elenco prodotti](assets/mobile-datacollection-prodListItems-schema.png)
   * Tieni presente che `productListItems` è un array che consente di fornire più prodotti.

1. Espandi l’oggetto xdmData per includere dati supplementari:

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

1. Utilizza la struttura dati per creare un’ `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Invia l’evento e i dati a Platform Edge Network:

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### Esempio #2: gruppi di campi personalizzati

Rivedi l’esempio seguente senza provare a implementarlo nell’app di esempio:

1. Nello schema, identifica l’evento che stai tentando di raccogliere. In questo esempio, tieni traccia di una &quot;Interazione app&quot; costituita da un nome e un evento di azione app.
   ![schema interazione app](assets/mobile-datacollection-appInteraction-schema.png)

1. Inizia a costruire l&#39;oggetto.

   >[!NOTE]
   >
   >  I gruppi di campi standard iniziano sempre nella radice dell&#39;oggetto.
   >
   >  I gruppi di campi personalizzati iniziano sempre sotto un oggetto univoco per l’organizzazione di Experienci Cloud, &quot;_techmarketingdemos&quot; in questo esempio.

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

   Oppure...

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

1. Utilizza la struttura dati per creare un’ `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Invia evento e dati a Platform Edge Network.

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### Aggiunta del tracciamento della visualizzazione schermata all’app Luma

Gli esempi precedenti hanno spiegato il processo mentale durante la costruzione di un oggetto dati XDM. Ora aggiungeremo il tracciamento della visualizzazione a schermo nell’app Luma.

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

1. Ripeti per ogni schermata nell’app, aggiornando `stateName` e così via.



### Convalida

1. Rivedi [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo ad Assurance.
1. Eseguire l&#39;azione e cercare `hitReceived` evento da `com.adobe.edge.konductor` fornitore.
1. Seleziona l’evento e rivedi i dati XDM nel `messages` oggetto.
   ![convalida della raccolta dati](assets/mobile-datacollection-validation.png)

### Esempio di #3 - acquisto

In questo esempio, supponiamo che l’utente abbia effettuato correttamente il seguente acquisto:

* #1 prodotto - Tappetino di yoga.
   * $ 49,99 x1
   * SKU: 5829
* #2 del prodotto - Bottiglia d&#39;acqua.
   * $ 10,00 x3
   * SKU: 9841
* Totale ordine: $ 79,99
* ID ordine univoco: 298234720
* Tipo di pagamento: Carta di credito Visa
* ID transazione pagamento univoco: 847361

#### Schema

Di seguito sono riportati i campi dello schema correlati da utilizzare:

* eventType: &quot;commerce.purchases&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails (personalizzato)

>[!TIP]
>
>I gruppi di campi personalizzati si trovano sempre sotto l’identificatore dell’organizzazione di Experience Cloud.
>
>&quot;_techmarketingdemos&quot; viene sostituito con il valore univoco della tua organizzazione.

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
>Per maggiore chiarezza, tutti i valori sono hardcoded. In una situazione reale, i valori sarebbero popolati in modo dinamico.


### Implementazione nell’app Luma

Devi disporre di tutti gli strumenti per iniziare ad aggiungere la raccolta dati all’app di esempio Luma. Di seguito è riportato un elenco di ipotetici requisiti di tracciamento che puoi seguire.

* Monitora ogni visualizzazione dello schermo.
   * Campi schema: screenType, screenName, screenView
* Tracciare le azioni non di e-commerce.
   * Campi dello schema: appInteraction.name, appAction
* Azioni Commerce:
   * Pagina prodotto: productViews
   * Aggiungi al carrello: productListAdds
   * Rimuovi dal carrello: productListRemovals
   * Inizio estrazione: estrazioni
   * Visualizza carrello: productListViews
   * Aggiungi alla lista dei desideri: saveForLaters
   * Acquisto: acquisti, ordine

>[!TIP]
>
>Rivedi [app completamente implementata](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) per ulteriori esempi.

### Convalida

1. Rivedi [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo ad Assurance.

1. Eseguire l&#39;azione e cercare `hitReceived` evento da `com.adobe.edge.konductor` fornitore.

1. Seleziona l’evento e rivedi i dati XDM nel `messages` oggetto.
   ![convalida della raccolta dati](assets/mobile-datacollection-validation.png)

## Inviare eventi ad Analytics e Platform

Ora che hai raccolto gli eventi e li hai inviati a Platform Edge Network, questi verranno inviati alle applicazioni e ai servizi configurati nel tuo [flusso di dati](create-datastream.md). Nelle lezioni successive mapperai questi dati su [Adobe Analytics](analytics.md) e [Adobe Experience Platform](platform.md).

Successivo: **[WebViews](web-views.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)