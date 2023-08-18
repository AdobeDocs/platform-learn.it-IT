---
title: Eventi
description: Scopri come raccogliere i dati di un evento in un’app mobile.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

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

  ```swift {highlight="2-8"}
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

* Nello schema, identifica eventuali dati aggiuntivi associati all’evento di visualizzazione del prodotto Commerce. In questo esempio, includi `productListItems` che è un set standard di campi utilizzati con qualsiasi evento correlato a commerce:

  ![schema elementi elenco prodotti](assets/datacollection-prodListItems-schema.png)
   * Tieni presente che `productListItems` è un array che consente di fornire più prodotti.

* Per aggiungere questi dati, espandi il tuo `xdmData` oggetto da includere dati supplementari:

```swift {highlight="9-16"}
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

* Puoi quindi utilizzare la struttura dati per creare un’ `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* E invia l’evento e i dati a Platform Edge Network utilizzando l’API sendEvent:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Ora, implementiamo questo codice nel tuo progetto Xcode.
Nell’app sono presenti diverse azioni relative al prodotto commerce (visualizzazione, aggiunta al carrello, salvataggio per un momento successivo, acquisto) e desideri inviare eventi in base a tali azioni, in base a quanto eseguito dall’utente.

1. Per strutturare l’invio di eventi esperienza, vai a `MobileSDK`e aggiungi quanto segue al `sendCommerceExperienceEvent` funzione. Questa funzione considera l’evento e il prodotto dell’esperienza di e-commerce come parametri:

   ```swift {highlight="2-22"}
   func sendCommerceExperienceEvent(commerceEventType: String, product: Product) {
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
   }
   ```

1. In entrata `ProductView` aggiungi varie chiamate al `sendCommerceExperienceEvent` funzione:

   1. Alla `.task` modificatore in `ATTrackingManager.trackingAuthorizationStatus` chiusura. Il `.task` il modificatore viene chiamato quando la visualizzazione prodotto viene inizializzata e visualizzata, quindi desideri inviare un evento di visualizzazione prodotto in quel momento specifico.

      ```swift {highlight="4-5"}
      .task {
          if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send commerce experience event
              MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
          }
      }
      ```

   1. Per ciascuno dei pulsanti (Salvato per un momento successivo, Aggiungi al carrello e Acquista) nella barra degli strumenti, disponibile nella visualizzazione Prodotto, aggiungi la chiamata pertinente.

      * Per salvare per dopo / Aggiungi alla lista dei desideri:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                // Send saveForLater commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
                }
            }
            showSaveForLaterDialog.toggle()
        } label: {
            Label("", systemImage: "heart")
        }
        .alert(isPresented: $showSaveForLaterDialog, content: {
            Alert(title: Text( "Saved for later"), message: Text("The selected item is saved to your wishlist…"))
        })
        ```

      * Per Aggiungi Al Carrello:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send productListAdds commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
                }
            }
            showAddToCartDialog.toggle()
        } label: {
                Label("", systemImage: "cart.badge.plus")
        }
        alert(isPresented: $showAddToCartDialog, content: {
            Alert(title: Text( "Added to basket"), message: Text("The selected item is added to your basket…"))
        })
        ```

      * Acquisto:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send purchase commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
                }
            }
            showPurchaseDialog.toggle()
        } label: {
            Label("", systemImage: "creditcard")
        }
        .alert(isPresented: $showPurchaseDialog, content: {
            Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
        })
        ```

### Gruppi di campi personalizzati

Immagina di voler tenere traccia delle visualizzazioni a schermo e delle interazioni nell’app stessa. Ricorda di aver definito un gruppo di campi personalizzato per questo tipo di eventi.

* Nello schema, identifica gli eventi che stai tentando di raccogliere.
  ![schema interazione app](assets/datacollection-appInteraction-schema.png)

* Inizia a costruire l&#39;oggetto.

  >[!NOTE]
  >
  >  I gruppi di campi standard iniziano sempre nella radice dell&#39;oggetto.
  >
  >  I gruppi di campi personalizzati iniziano sempre sotto un oggetto univoco per la tua organizzazione Experience Cloud, `_techmarketingdemos` in questo esempio.

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


* Quindi la struttura dati per creare un’ `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Invia evento e dati a Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Di nuovo, possiamo implementare questo codice nel progetto Xcode.

1. Per comodità, definisci due funzioni in `MobileSDK`.

   Uno per le interazioni tra app. Aggiungi il codice evidenziato al `sendAppInteractionEvent(actionName)` funzione in **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-16"}
   func sendAppInteractionEvent(actionName: String) {
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
   }
   ```

   E uno per il tracciamento dello schermo. Aggiungi il codice evidenziato `sendTrackScreenEvent(stateName)` funzione in **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-17"}
   func sendTrackScreenEvent(stateName: String) {
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
   }
   ```

1. Accedi a **[!UICONTROL FoglioAccesso]**.

   * Aggiungi il seguente codice evidenziato alla chiusura del pulsante di accesso:

     ```swift {highlight="3"}
     Button("Login") {                               
        // Send app interaction event
        MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
        dismiss()
     }
     .disabled(currentEmailId.isValidEmail == false)
     .buttonStyle(.bordered)
     ```

   * Aggiungi il seguente codice evidenziato a `onAppear` modificatore:

     ```swift {highlight="13"}
     .onAppear {
        Task {
            if currentEmailId == "testUser@gmail.com" || currentEmailId.isValidEmail == false {
                // still allow to log in
                disableLogin = false
            }
            else {
                disableLogin = true
            }
        }
        // Send track screen event
        MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
     }
     ```

### Convalida

1. Rivedi [istruzioni di configurazione](assurance.md) e collegare il simulatore o il dispositivo ad Assurance.
1. Esegui l’app per accedere e interagire con un prodotto.

   1. Sposta l’icona Assurance a sinistra.
   1. Seleziona **[!UICONTROL Home]** nella barra delle schede.
   1. Seleziona la **[!UICONTROL Login]** per aprire il foglio di accesso.
   1. Seleziona la **[!UICONTROL A|]** per inserire un’e-mail casuale e un id cliente.
   1. Seleziona **[!UICONTROL Login]**.
   1. Seleziona **[!UICONTROL Prodotti]** nella barra delle schede.
   1. Seleziona un prodotto.
   1. Seleziona **[!UICONTROL Salva per dopo]**.
   1. Seleziona **[!UICONTROL Aggiungi al carrello]**.
   1. Seleziona **[!UICONTROL Acquisto]**.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. Cerca **[!UICONTROL hitReceived]** eventi da **[!UICONTROL com.adobe.edge.konductor]** fornitore.
1. Seleziona l’evento e rivedi i dati XDM nel **[!UICONTROL messaggi]** oggetto.
   ![convalida della raccolta dati](assets/datacollection-validation.png)


### Implementazione nell’app Luma

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere la raccolta dati all’app Luma. Puoi aggiungere più informazioni sul modo in cui l’utente interagisce con i prodotti, nonché aggiungere all’app ulteriori chiamate di interazione e tracciamento dello schermo:

* Implementa l’ordine, il pagamento, il carrello vuoto e altre funzionalità nell’app e aggiungi un evento di esperienza di e-commerce rilevante a questa funzionalità.
* Ripeti la chiamata a `sendAppInteractionEvent` con il parametro appropriato per tenere traccia delle altre interazioni dell’app nell’app da parte dell’utente.
* Ripeti la chiamata a `sendTrackScreenEvent` con il parametro appropriato per tenere traccia di ogni schermata visualizzata dall’utente nell’app.

>[!TIP]
>
>Rivedi [app completamente implementata](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) per ulteriori esempi.


## Inviare eventi ad Analytics e Platform

Ora che hai raccolto gli eventi e li hai inviati a Platform Edge Network, questi vengono inviati alle applicazioni e ai servizi configurati nel tuo [flusso di dati](create-datastream.md). Nelle lezioni successive, mappi questi dati su [Adobe Analytics](analytics.md) e [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>Ora hai configurato l’app per tenere traccia degli eventi di e-commerce, interazione con l’app e tracciamento dello schermo su Adobe Experience Platform Edge Network e su tutti i servizi definiti nello stream di dati.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[WebViews](web-views.md)**
