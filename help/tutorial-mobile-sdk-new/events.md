---
title: Tracciare i dati dell’evento
description: Scopri come tenere traccia dei dati evento in un’app mobile.
hide: true
exl-id: b926480b-b431-4db8-835c-fa1db6436a93
source-git-commit: 4434bee35591d7cf79b7dddc03faba83d00b31f5
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 0%

---

# Tracciare i dati dell’evento

Scopri come tracciare gli eventi in un’app mobile.

L’estensione Edge Network fornisce un’API per inviare eventi esperienza a Platform Edge Network. Un Experience Event è un oggetto che contiene dati conformi alla definizione dello schema XDM ExperienceEvent. Più semplicemente, acquisiscono ciò che le persone fanno nella tua app mobile. Una volta ricevuti i dati da Platform Edge Network, questi possono essere inoltrati alle applicazioni e ai servizi configurati nel flusso di dati, come Adobe Analytics e Experienci Platform. Ulteriori informazioni su [Eventi esperienza](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) nella documentazione del prodotto.

## Prerequisiti

* Tutte le dipendenze del pacchetto sono presenti nel progetto Xcode.
* Estensioni registrate in **[!UICONTROL AppDelegate]**.
* Estensione MobileCore configurata per utilizzare il tuo sviluppo `appId`.
* SDK importati.
* L&#39;app è stata creata ed eseguita correttamente con le modifiche precedenti.

## Finalità di apprendimento

In questa lezione, potrai

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
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: descrive l’evento che si è verificato, utilizza un [valore noto](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possibile.
   * `commerce.productViews.value`: valore numerico o booleano dell’evento. Se è un valore booleano (o &quot;Contatore&quot; in Adobe Analytics), il valore è sempre impostato su 1. Se è un evento numerico o di valuta, il valore può essere > 1.

* Nello schema, identifica eventuali dati aggiuntivi associati all’evento di visualizzazione del prodotto Commerce. In questo esempio, includi **[!UICONTROL productListItems]** che è un set standard di campi utilizzati con qualsiasi evento correlato a commerce:

  ![schema elementi elenco prodotti](assets/datacollection-prodListItems-schema.png)
   * Tieni presente che **[!UICONTROL productListItems]** è un array che consente di fornire più prodotti.

* Per aggiungere questi dati, espandi il tuo `xdmData` oggetto da includere dati supplementari:

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

* Ora puoi utilizzare questa struttura dati per creare un’ `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* E invia evento e dati a Platform Edge Network utilizzando `sendEvent` API:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Il [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API è l&#39;SDK di AEP Mobile equivalente al [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) e [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate) Chiamate API. Consulta [Migrazione dall’estensione Analytics per dispositivi mobili a Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) per ulteriori informazioni.

Ora stai per implementare effettivamente questo codice nel tuo progetto Xcode.
Nell’app sono presenti diverse azioni relative al prodotto commerce e desideri inviare eventi, in base alle azioni eseguite dall’utente:

* view: si verifica quando un utente visualizza un prodotto specifico,
* aggiungi al carrello: quando un utente tocca <img src="assets/addtocart.png" width="20" /> in una schermata di dettaglio del prodotto,
* salva per dopo: quando un utente tocca <img src="assets/saveforlater.png" width="15" /> in una schermata di dettaglio del prodotto,
* acquisto: quando un utente tocca <img src="assets/purchase.png" width="20" /> in una schermata di dettaglio del prodotto.

Per implementare l’invio di eventi di esperienza relativi al commercio in modo riutilizzabile, utilizza una funzione dedicata:

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode e aggiungi quanto segue al `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)` funzione.

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
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
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   Questa funzione considera il tipo di evento e il prodotto dell’esperienza di e-commerce come parametri e

   * imposta il payload XDM come dizionario, utilizzando i parametri della funzione,
   * configura un evento esperienza utilizzando il dizionario,
   * invia l&#39;evento esperienza utilizzando [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** nel Navigatore progetti Xcode e aggiungere varie chiamate al `sendCommerceExperienceEvent` funzione:

   1. Alla `.task` modificatore, all&#39;interno del `ATTrackingManager.trackingAuthorizationStatus` chiusura. Questo `.task` il modificatore viene chiamato quando la visualizzazione prodotto viene inizializzata e visualizzata, quindi desideri inviare un evento di visualizzazione prodotto in quel momento specifico.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
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

>[!TIP]
>
>Se stai sviluppando per Android™, utilizza Map (`java.util.Map`) come interfaccia fondamentale per creare il payload XDM.


### Gruppi di campi personalizzati

Immagina di voler tenere traccia delle visualizzazioni a schermo e delle interazioni nell’app stessa. Ricorda di aver definito un gruppo di campi personalizzato per questo tipo di eventi.

* Nello schema, identifica gli eventi che stai tentando di raccogliere.
  ![schema interazione app](assets/datacollection-appInteraction-schema.png)

* Inizia a costruire l&#39;oggetto.

  >[!NOTE]
  >
  * I gruppi di campi standard iniziano sempre nella radice dell&#39;oggetto.
  >
  * I gruppi di campi personalizzati iniziano sempre sotto un oggetto univoco per la tua organizzazione Experience Cloud, `_techmarketingdemos` in questo esempio.

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

1. Per comodità, definisci due funzioni in **[!UICONTROL MobileSDK]**. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode.

   1. Uno per le interazioni tra app. Aggiungi questo codice al `func sendAppInteractionEvent(actionName: String)` funzione:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
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

      Questa funzione utilizza il nome dell’azione come parametro e

      * imposta il payload XDM come dizionario, utilizzando il parametro della funzione,
      * configura un evento esperienza utilizzando il dizionario,
      * invia l&#39;evento esperienza utilizzando [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.


   1. E uno per il tracciamento dello schermo. Aggiungi questo codice al `func sendTrackScreenEvent(stateName: String) ` funzione:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
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

      Questa funzione utilizza il nome dello stato come parametro e

      * imposta il payload XDM come dizionario, utilizzando il parametro della funzione,
      * configura un evento esperienza utilizzando il dizionario,
      * invia l&#39;evento esperienza utilizzando [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL FoglioAccesso]**.

   1. Aggiungi il seguente codice evidenziato alla chiusura del pulsante di accesso:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Aggiungi il seguente codice evidenziato a `onAppear` modificatore:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## Convalida

1. Rivedi [istruzioni di configurazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo con Assurance.

   1. Sposta l’icona Assurance a sinistra.
   1. Seleziona **[!UICONTROL Home]** nella barra delle schede e verificare di aver visualizzato **[!UICONTROL ECID]**, **[!UICONTROL E-mail]**, e **[!UICONTROL ID CRM]** nella schermata iniziale.
   1. Seleziona **[!DNL Products]** nella barra delle schede.
   1. Seleziona un prodotto.
   1. Seleziona <img src="assets/saveforlater.png" width="15" />.
   1. Seleziona <img src="assets/addtocart.png" width="20" />.
   1. Seleziona <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. Nell’interfaccia utente Assurance, cerca **[!UICONTROL hitReceived]** eventi da **[!UICONTROL com.adobe.edge.konductor]** fornitore.
1. Seleziona l’evento e rivedi i dati XDM nel **[!UICONTROL messaggi]** oggetto. In alternativa, puoi utilizzare ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copia evento non elaborato]** e utilizza un editor di testo o di codice della tua preferenza per incollare e ispezionare l’evento.

   ![convalida della raccolta dati](assets/datacollection-validation.png)


## Passaggi successivi

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere la raccolta dati all’app. Puoi aggiungere più informazioni sul modo in cui l’utente interagisce con i prodotti nell’app e più chiamate di interazione app e tracciamento dello schermo all’app:

* Implementa l’ordine, il pagamento, il carrello vuoto e altre funzionalità nell’app e aggiungi eventi di esperienza di e-commerce pertinenti a questa funzionalità.
* Ripeti la chiamata a `sendAppInteractionEvent` con il parametro appropriato per tenere traccia delle altre interazioni dell’app da parte dell’utente.
* Ripeti la chiamata a `sendTrackScreenEvent` con il parametro appropriato per tenere traccia delle schermate visualizzate dall’utente nell’app.

>[!TIP]
>
Rivedi [app completata](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) per ulteriori esempi.


## Inviare eventi ad Analytics e Platform

Ora che hai raccolto gli eventi e li hai inviati a Platform Edge Network, questi vengono inviati alle applicazioni e ai servizi configurati nel tuo [flusso di dati](create-datastream.md). Nelle lezioni successive, mappi questi dati su [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md)e altre soluzioni Adobe Experience Cloud come [Adobe Target](target.md) e Adobe Journey Optimizer.

>[!SUCCESS]
>
Ora hai configurato l’app per tenere traccia degli eventi di e-commerce, interazione con l’app e tracciamento dello schermo su Adobe Experience Platform Edge Network e su tutti i servizi definiti nello stream di dati.
>
Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Gestisci visualizzazioni Web](web-views.md)**
