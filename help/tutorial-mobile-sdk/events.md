---
title: Tracciare i dati dell’evento nelle app mobili con Platform Mobile SDK
description: Scopri come tenere traccia dei dati evento in un’app mobile.
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: afb15c561179386e7846e8cd8963f67820af09f1
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---

# Tracciare i dati dell’evento

Scopri come tracciare gli eventi in un’app mobile.

L’estensione Edge Network fornisce un’API per inviare eventi Experience all’Edge Network Platform. Un Experience Event è un oggetto che contiene dati conformi alla definizione dello schema XDM ExperienceEvent. Più semplicemente, acquisiscono ciò che le persone fanno nella tua app mobile. Una volta ricevuti i dati dall’Edge Network di Platform, questi possono essere inoltrati alle applicazioni e ai servizi configurati nel flusso di dati, come Adobe Analytics e Experience Platform. Ulteriori informazioni su [Eventi esperienza](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) nella documentazione del prodotto.

## Prerequisiti

* Tutte le dipendenze del pacchetto sono presenti nel progetto Xcode.
* Estensioni registrate in **[!UICONTROL AppDelegate]**.
* Estensione MobileCore configurata per utilizzare il tuo sviluppo `appId`.
* SDK importati.
* L&#39;app è stata creata ed eseguita correttamente con le modifiche precedenti.

## Obiettivi di apprendimento

In questa lezione, potrai

* Scopri come strutturare i dati XDM in base a uno schema.
* Invia un evento XDM basato su un gruppo di campi standard.
* Invia un evento XDM basato su un gruppo di campi personalizzato.
* Invia un evento di acquisto XDM.
* Convalida con Assurance.

## Creazione di un evento esperienza

L’estensione Adobe Experience Platform Edge può inviare a Adobe Experience Platform Edge Network gli eventi che seguono uno schema XDM definito in precedenza.

Il processo è simile a questo...

1. Identifica l’interazione con l’app mobile che stai tentando di tracciare.

1. Esamina lo schema e identifica l’evento appropriato.

1. Esamina lo schema e identifica eventuali campi aggiuntivi da utilizzare per descrivere l’evento.

1. Costruisci e popola l’oggetto dati.

1. Crea e invia evento.

1. Convalida.


### Gruppi di campi standard

Per i gruppi di campi standard, il processo è simile al seguente:

* Nello schema, identifica gli eventi che stai tentando di raccogliere. In questo esempio stai tenendo traccia degli eventi di esperienza di e-commerce, ad esempio un evento di visualizzazione prodotto (**[!UICONTROL productViews]**).

  ![schema visualizzazione prodotto](assets/datacollection-prodView-schema.png)

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

   * `eventType`: descrive l&#39;evento che si è verificato. Utilizzare un [valore noto](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) quando possibile.
   * `commerce.productViews.value`: valore numerico o booleano dell&#39;evento. Se è un valore booleano (o &quot;Contatore&quot; in Adobe Analytics), il valore è sempre impostato su 1. Se è un evento numerico o di valuta, il valore può essere > 1.

* Nello schema, identifica eventuali dati aggiuntivi associati all’evento di visualizzazione del prodotto Commerce. In questo esempio, includi **[!UICONTROL productListItems]** che è un set standard di campi utilizzati con qualsiasi evento relativo a e-commerce:

  ![schema elementi elenco prodotti](assets/datacollection-prodListItems-schema.png)
   * **[!UICONTROL productListItems]** è un array e pertanto è possibile specificare più prodotti.

* Per aggiungere questi dati, espandere l&#39;oggetto `xdmData` per includere dati supplementari:

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

* È ora possibile utilizzare questa struttura dati per creare un `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* E invia l&#39;evento e i dati all&#39;Edge Network di Platform utilizzando l&#39;API `sendEvent`:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

L&#39;API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) è l&#39;SDK di AEP Mobile equivalente alle chiamate API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) e [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate). Per ulteriori informazioni, consulta [Migrare dall&#39;estensione per dispositivi mobili Analytics all&#39;Edge Network di Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/).

Ora stai per implementare effettivamente questo codice nel tuo progetto Xcode.
Nell’app sono presenti diverse azioni relative al prodotto commerce e desideri inviare eventi, in base alle azioni eseguite dall’utente:

* view: si verifica quando un utente visualizza un prodotto specifico,
* aggiungi al carrello: quando un utente tocca <img src="assets/addtocart.png" width="20"/> in una schermata dei dettagli del prodotto,
* salva per dopo: quando un utente tocca <img src="assets/saveforlater.png" width="15"/> in una schermata dei dettagli del prodotto,
* acquisto: quando un utente tocca <img src="assets/purchase.png" width="20"/> in una schermata dei dettagli del prodotto.

Per implementare l’invio di eventi di esperienza relativi al commercio in modo riutilizzabile, utilizza una funzione dedicata:

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel navigatore progetti Xcode e aggiungi quanto segue alla funzione `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

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
   * invia l&#39;evento esperienza utilizzando l&#39;API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** nel Navigator dei progetti Xcode e aggiungi varie chiamate alla funzione `sendCommerceExperienceEvent`:

   1. Nel modificatore `.task`, entro la chiusura di `ATTrackingManager.trackingAuthorizationStatus`. Questo modificatore `.task` viene chiamato quando la visualizzazione prodotto viene inizializzata e visualizzata, quindi si desidera inviare un evento di visualizzazione prodotto in quel momento specifico.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. Per ciascuno dei pulsanti (<img src="assets/saveforlater.png" width="15"/>, <img src="assets/addtocart.png" width="20"/> e <img src="assets/purchase.png" width="20"/>) nella barra degli strumenti, aggiungi la chiamata pertinente entro la chiusura di `ATTrackingManager.trackingAuthorizationStatus == .authorized`:

      1. Per <img src="assets/saveforlater.png" width="15"/>

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Per <img src="assets/addtocart.png" width="20"/>

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Per <img src="assets/purchase.png" width="20"/>

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
  >* I gruppi di campi standard iniziano sempre nella radice dell&#39;oggetto.
  >
  >* I gruppi di campi personalizzati iniziano sempre con un oggetto univoco per l&#39;organizzazione di Experienci Cloud, `_techmarketingdemos` in questo esempio.

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


* È ora possibile utilizzare questa struttura dati per creare un `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Invia l’evento e i dati all’Edge Network di Platform.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Di nuovo, possiamo implementare questo codice nel progetto Xcode.

1. Per comodità, puoi definire due funzioni in **[!UICONTROL MobileSDK]**. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel navigatore dei progetti Xcode.

   1. Uno per le interazioni tra app. Aggiungi questo codice alla funzione `func sendAppInteractionEvent(actionName: String)`:

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
      * invia l&#39;evento esperienza utilizzando l&#39;API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   1. E uno per il tracciamento dello schermo. Aggiungi questo codice alla funzione `func sendTrackScreenEvent(stateName: String) `:

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
      * invia l&#39;evento esperienza utilizzando l&#39;API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL Foglio di accesso]**.

   1. Aggiungi il seguente codice evidenziato alla chiusura del pulsante di accesso:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Aggiungi il seguente codice evidenziato al modificatore `onAppear`:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## Convalida

1. Consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo con Assurance.

   1. Sposta l’icona Assurance a sinistra.
   1. Seleziona **[!UICONTROL Home]** nella barra delle schede e verifica di visualizzare un **[!UICONTROL ECID]**, **[!UICONTROL E-mail]** e un **[!UICONTROL ID CRM]** nella schermata iniziale.
   1. Selezionare **[!DNL Products]** nella barra delle schede.
   1. Seleziona un prodotto.
   1. Seleziona <img src="assets/saveforlater.png" width="15"/>.
   1. Seleziona <img src="assets/addtocart.png" width="20"/>.
   1. Seleziona <img src="assets/purchase.png" width="15"/>.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. Nell&#39;interfaccia utente di Assurance, cerca gli eventi **[!UICONTROL hitReceived]** del fornitore **[!UICONTROL com.adobe.edge.konductor]**.
1. Seleziona l&#39;evento e controlla i dati XDM nell&#39;oggetto **[!UICONTROL messages]**. In alternativa, puoi utilizzare ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copia evento non elaborato]** e utilizzare un editor di testo o di codice di tua preferenza per incollare e ispezionare l&#39;evento.

   ![convalida raccolta dati](assets/datacollection-validation.png)


## Passaggi successivi

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere la raccolta dati all’app. Puoi aggiungere più informazioni sul modo in cui l’utente interagisce con i prodotti nell’app e più chiamate di interazione app e tracciamento dello schermo all’app:

* Implementa l’ordine, il pagamento, il carrello vuoto e altre funzionalità nell’app e aggiungi eventi di esperienza di e-commerce pertinenti a questa funzionalità.
* Ripetere la chiamata a `sendAppInteractionEvent` con il parametro appropriato per tenere traccia delle altre interazioni dell&#39;app da parte dell&#39;utente.
* Ripeti la chiamata a `sendTrackScreenEvent` con il parametro appropriato per tenere traccia delle schermate visualizzate dall&#39;utente nell&#39;app.

>[!TIP]
>
>Rivedi l&#39;[app completata](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) per altri esempi.


## Inviare eventi ad Analytics e Platform

Dopo aver raccolto gli eventi e averli inviati all&#39;Edge Network di Platform, vengono inviati alle applicazioni e ai servizi configurati nel [flusso di dati](create-datastream.md). Nelle lezioni successive, mappi questi dati a [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md) e altre soluzioni Adobe Experience Cloud come [Adobe Target](target.md) e Adobe Journey Optimizer.

>[!SUCCESS]
>
>Ora hai configurato l’app per tenere traccia degli eventi di e-commerce, interazione con l’app e tracciamento dello schermo nell’Edge Network di Adobe Experience Platform e in tutti i servizi definiti nello stream di dati.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Gestione visualizzazioni Web](web-views.md)**
