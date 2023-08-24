---
title: Eventi
description: Scopri come raccogliere i dati di un evento in un’app mobile.
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 1%

---

# Eventi

Scopri come tracciare gli eventi in un’app mobile.

L’estensione Edge Network fornisce un’API per inviare eventi esperienza a Platform Edge Network. Un Experience Event è un oggetto che contiene dati conformi alla definizione dello schema XDM ExperienceEvent. Più semplicemente, acquisiscono ciò che le persone fanno nella tua app mobile. Una volta ricevuti i dati da Platform Edge Network, questi possono essere inoltrati alle applicazioni e ai servizi configurati nel flusso di dati, come Adobe Analytics e Experienci Platform. Ulteriori informazioni su [Eventi esperienza](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) nella documentazione del prodotto.

## Prerequisiti

* Tutte le dipendenze del pacchetto presenti nel progetto Xcode.
* Estensioni registrate in AppDelegate.
* MobileCore configurato per utilizzare l&#39;appId di sviluppo.
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


### Gruppi di campi standard

Per i gruppi di campi standard, il processo è simile al seguente:

* Nello schema, identifica gli eventi che stai tentando di raccogliere. In questo esempio tieni traccia degli eventi di esperienza di e-commerce, ad esempio una visualizzazione di prodotto (**[!UICONTROL productViews]**).

  ![schema di visualizzazione prodotto](assets/datacollection-prodView-schema.png)

* Per creare un oggetto contenente i dati dell’evento esperienza nell’app, puoi utilizzare un codice come:

  ```swift
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "id": sku,
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: descrive l’evento che si è verificato, utilizza un [valore noto](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possibile.
   * `commerce.productViews.id`: valore stringa che rappresenta lo SKU del prodotto
   * `commerce.productViews.value`: specifica il valore numerico dell’evento. Se è un valore booleano (o &quot;Contatore&quot; in Adobe Analytics), il valore è sempre impostato su 1. Se è un evento numerico o di valuta, il valore può essere > 1.

* Nello schema, identifica eventuali dati aggiuntivi associati all’evento di visualizzazione del prodotto Commerce. In questo esempio, includi **[!UICONTROL productListItem]** che è un set standard di campi utilizzati con qualsiasi evento correlato a commerce:

  ![schema elementi elenco prodotti](assets/datacollection-prodListItems-schema.png)
   * Tieni presente che **[!UICONTROL productListItems]** è un array che consente di fornire più prodotti.

* Per aggiungere questi dati, espandi il tuo `xdmData` oggetto da includere dati supplementari:

```swift
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
        "commerce": [
        "productViews": [
            "id": sku,
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

* Ora puoi utilizzare questa struttura dati per creare un’ `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* E invia evento e dati a Platform Edge Network utilizzando `sendEvent` API:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Ora stai per implementare effettivamente questo codice nel tuo progetto Xcode.
Nell’app sono presenti diverse azioni relative al prodotto commerce e desideri inviare eventi in base a tali azioni, in base a quanto eseguito dall’utente:

* view: si verifica quando gli utenti visualizzano un prodotto specifico,
* aggiungi al carrello: quando l’utente tocca <img src="assets/addtocart.png" width="20" /> in una schermata di dettaglio del prodotto,
* salva per dopo: quando l&#39;utente tocca <img src="assets/saveforlater.png" width="15" /> nella schermata product detail,
* buyer: quando l’utente tocca il <img src="assets/purchase.png" width="20" /> nella schermata product detail.

Per strutturare gli eventi di esperienza di invio:

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utilità]** > **[!UICONTROL MobileSDK]** in Navigator del progetto Xcode e aggiungi quanto segue al `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)` funzione. Questa funzione considera l’evento e il prodotto dell’esperienza di e-commerce come parametri:

   ```swift
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
               "id": product.sku,
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name": product.name,
               "priceTotal": product.price,
               "SKU": product.sku
           ]
       ]
   ]
   
   Logger.viewCycle.info("About to send commerce experience event of type  \(commerceEventType)..."
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Prodotti]** > **[!UICONTROL ProductView]** e aggiungere diverse chiamate al `sendCommerceExperienceEvent` funzione:

   1. Alla `.task` modificatore, all&#39;interno del `ATTrackingManager.trackingAuthorizationStatus` chiusura. Questo `.task` il modificatore viene chiamato quando la visualizzazione prodotto viene inizializzata e visualizzata, quindi desideri inviare un evento di visualizzazione prodotto in quel momento specifico.

      ```swift
      // Send commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
      ```

   1. Per ciascuno dei pulsanti (<img src="assets/saveforlater.png" width="15" />, <img src="assets/addtocart.png" width="20" /> e <img src="assets/purchase.png" width="20" />) nella barra degli strumenti, aggiungi la chiamata pertinente all&#39;interno di `ATTrackingManager.trackingAuthorizationStatus == .authorized` chiusura:

      1. Per <img src="assets/saveforlater.png" width="15" />

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Per <img src="assets/addtocart.png" width="20" />

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Per <img src="assets/purchase.png" width="20" />

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

### Gruppi di campi personalizzati

Immagina di voler tenere traccia delle visualizzazioni a schermo e delle interazioni nell’app stessa. Ricorda di aver definito un gruppo di campi personalizzato per questo tipo di eventi.

* Nello schema, identifica gli eventi che stai tentando di raccogliere.
  ![schema interazione app](assets/datacollection-appInteraction-schema.png)

* Inizia a costruire l&#39;oggetto.

  >[!NOTE]
  >
  >* I gruppi di campi standard iniziano sempre nella radice dell&#39;oggetto.
  >
  >* I gruppi di campi personalizzati iniziano sempre sotto un oggetto univoco per la tua organizzazione Experience Cloud, `_techmarketingdemos` in questo esempio.

  Per l’evento di interazione dell’app, puoi costruire un oggetto come:

  ```swift
  let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
      "appInformation": [
          "appInteraction": [
              "name": "login",
              "appAction": [
                  "value": 1
                  ]
              ]
          ]
      ]
  ]
  ```

  Per l’evento di tracciamento dello schermo, puoi costruire un oggetto come:

  ```swift
  var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                    "screenName": "luma: content: ios: us: en: login",
                    "screenView": [
                        "value": 1
                    ]
                ]
            ] 
        ]
  ]
  ```


* Ora puoi utilizzare questa struttura dati per creare un’ `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Invia evento e dati a Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Di nuovo, possiamo implementare questo codice nel progetto Xcode.

1. Per comodità, definisci due funzioni in **[!UICONTROL MobileSDK]**. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utilità]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode.

   1. Uno per le interazioni tra app. Aggiungi questo codice al `func sendAppInteractionEvent(actionName: String)` funzione:

      ```swift
      let xdmData: [String: Any] = [
          "eventType": "application.interaction",
          tenant : [
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
      let appInteractionEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: appInteractionEvent)
      ```

   1. E uno per il tracciamento dello schermo. Aggiungi questo codice al `func sendTrackScreenEvent(stateName: String) ` funzione:

      ```swift
      let xdmData: [String: Any] = [
          "eventType": "application.scene",
          tenant : [
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
      ]
      let trackScreenEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: trackScreenEvent)
      ```

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Generale]** > **[!UICONTROL FoglioAccesso]**.

   1. Aggiungi il seguente codice evidenziato alla chiusura del pulsante di accesso:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      dismiss()
      ```

   1. Aggiungi il seguente codice evidenziato a `onAppear` modificatore:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

### Convalida

1. Rivedi [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo ad Assurance.
1. Esegui l’app per accedere e interagire con un prodotto.

   1. Sposta l’icona Assurance a sinistra.
   1. Seleziona **[!UICONTROL Home]** nella barra delle schede.
   1. Seleziona <img src="assets/login.png" width="15" /> per aprire il foglio di accesso.
   1. Seleziona <img src="assets/insert.png" width="15" /> per inserire un’e-mail casuale e un id cliente.
   1. Seleziona **[!UICONTROL Login]**.
   1. Seleziona **[!UICONTROL Prodotti]** nella barra delle schede.
   1. Seleziona un prodotto.
   1. Seleziona <img src="assets/saveforlater.png" width="15" />.
   1. Seleziona <img src="assets/addtocart.png" width="20" />.
   1. Seleziona <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. Nell’interfaccia utente Assurance, cerca **[!UICONTROL hitReceived]** eventi da **[!UICONTROL com.adobe.edge.konductor]** fornitore.
1. Seleziona l’evento e rivedi i dati XDM nel **[!UICONTROL messaggi]** oggetto.
   ![convalida della raccolta dati](assets/datacollection-validation.png)


### Implementazione nell’app Luma

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere la raccolta dati all’app Luma. Puoi aggiungere più informazioni sul modo in cui l’utente interagisce con i prodotti, nonché aggiungere all’app ulteriori chiamate di interazione e tracciamento dello schermo:

* Implementa l’ordine, il pagamento, il carrello vuoto e altre funzionalità nell’app e aggiungi un evento di esperienza di e-commerce rilevante a questa funzionalità.
* Ripeti la chiamata a `sendAppInteractionEvent` con il parametro appropriato per tenere traccia delle altre interazioni dell’app da parte dell’utente.
* Ripeti la chiamata a `sendTrackScreenEvent` con il parametro appropriato per tenere traccia delle schermate visualizzate dall’utente nell’app.

>[!TIP]
>
>Rivedi [app completamente implementata](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) per ulteriori esempi.


## Inviare eventi ad Analytics e Platform

Ora che hai raccolto gli eventi e li hai inviati a Platform Edge Network, questi vengono inviati alle applicazioni e ai servizi configurati nel tuo [flusso di dati](create-datastream.md). Nelle lezioni successive, mappi questi dati su [Adobe Analytics](analytics.md) e [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>Ora hai configurato l’app per tenere traccia degli eventi di e-commerce, interazione con l’app e tracciamento dello schermo su Adobe Experience Platform Edge Network e su tutti i servizi definiti nello stream di dati.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[WebViews](web-views.md)**
