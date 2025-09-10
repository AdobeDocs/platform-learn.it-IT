---
title: Mappatura dei dati raccolti con Platform Mobile SDK su Adobe Analytics
description: Scopri come raccogliere e mappare dati per Adobe Analytics in un’app mobile.
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Raccogliere e mappare dati di Analytics

Scopri come mappare i dati mobili su Adobe Analytics.

I dati [event](events.md) che hai raccolto e inviato a Platform Edge Network nelle lezioni precedenti vengono inoltrati ai servizi configurati nel flusso di dati, incluso Adobe Analytics. Mappa i dati alle variabili corrette nella suite di rapporti.

![Architettura](assets/architecture-aa.png){zoomable="yes"}

## Prerequisiti

* Informazioni sul tracciamento ExperienceEvent.
* Invio dei dati XDM nell&#39;app di esempio completato.
* Una suite di rapporti di Adobe Analytics che puoi utilizzare per questa lezione.

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Configura lo stream di dati con il servizio Adobe Analytics.
* Comprendere la mappatura automatica delle variabili di Analytics.
* Imposta le regole di elaborazione per mappare i dati XDM sulle variabili di Analytics.

## Aggiungere il servizio dello stream di dati di Adobe Analytics

Per inviare i dati XDM da Edge Network ad Adobe Analytics, configura il servizio Adobe Analytics allo stream di dati configurato come parte di [Creare uno stream di dati](create-datastream.md).

1. Nell&#39;interfaccia utente di Data Collection, seleziona **[!UICONTROL Datastreams]** e il tuo datastream.

1. Quindi selezionare ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi servizio]**.

1. Aggiungi **[!UICONTROL Adobe Analytics]** dall&#39;elenco [!UICONTROL Service],

1. Immetti il nome della suite di rapporti di Adobe Analytics che desideri utilizzare in **[!UICONTROL ID suite di rapporti]**.

1. Abilitare il servizio attivando **[!UICONTROL Enabled]**.

1. Seleziona **[!UICONTROL Salva]**.

   ![Aggiungi Adobe Analytics come servizio di stream di dati](assets/datastream-service-aa.png){zoomable="yes"}


## Mappatura automatica

Molti dei campi XDM standard sono mappati automaticamente alle variabili di Analytics. Vedi l&#39;[elenco completo](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping).

### Esempio #1 - s.products

Un buon esempio è la [variabile dei prodotti](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/products) che non può essere compilata utilizzando le regole di elaborazione. Con un&#39;implementazione XDM, si passano tutti i dati necessari in `productListItems` e `s.products` vengono compilati automaticamente tramite la mappatura di Analytics.

Questo oggetto:

```swift
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
```

risultati in:

```
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>Se `productListItems[].SKU` e `productListItems[].name` contengono entrambi dati, viene utilizzato il valore in `productListItems[].SKU`. Per ulteriori informazioni, vedi [Mappatura delle variabili di Analytics in Adobe Experience Edge](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping).


### Esempio #2 - scAdd

Se si guarda attentamente, tutti gli eventi hanno due campi: `value` (obbligatorio) e `id` (facoltativo). Il campo `value` viene utilizzato per incrementare il conteggio degli eventi. Il campo `id` viene utilizzato per la serializzazione.

Questo oggetto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

risultati in:

```
s.events = "scAdd"
```

Questo oggetto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

risultati in:

```
s.events = "scAdd:321435"
```

## Convalidare con Assurance

Utilizzando [Assurance](assurance.md) puoi confermare che stai inviando un evento esperienza, che i dati XDM sono corretti e che la mappatura di Analytics sta avvenendo come previsto.

1. Consulta la sezione [istruzioni di installazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.

1. Invia un evento **[!UICONTROL productListAdds]** (aggiungi un prodotto al carrello).

1. Visualizza l’hit ExperienceEvent.

   ![hit xdm di analytics](assets/analytics-assurance-experiencevent.png){zoomable="yes"}

1. Esamina la porzione XDM del JSON.

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "value" : 1
     }
   }
   // ...
   ```

1. Rivedi l&#39;evento **[!UICONTROL analytics.mapping]**.

   ![hit xdm di analytics](assets/analytics-assurance-mapping.png){zoomable="yes"}

Osserva quanto segue nella mappatura di Analytics:

* **[!UICONTROL gli eventi]** sono compilati con `scAdd` in base a `commerce.productListAdds`.
* **[!UICONTROL pl]** (variabile prodotti) è compilato con un valore concatenato basato su `productListItems`.
* In questo evento sono disponibili altre informazioni interessanti, inclusi tutti i dati contestuali.


## Mappatura con dati contestuali

I dati XDM inoltrati ad Analytics vengono convertiti in [dati contestuali](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/getting-started/proc-rules.md?lang=en), inclusi i campi standard e personalizzati.

La chiave dei dati contestuali è costruita seguendo questa sintassi:

```
a.x.[xdm path]
```

Ad esempio:

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>I campi personalizzati si trovano sotto l’identificatore dell’organizzazione Experience Cloud.
>
>Il nome tenant `_techmarketingdemos` è sostituito con il valore univoco dell&#39;organizzazione.



Per mappare questi dati contestuali XDM sui dati di Analytics nella suite di rapporti, puoi:

### Utilizza un gruppo di campi

* Aggiungi il gruppo di campi **[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent]** allo schema.

  ![Gruppo di campi FullExtension di Analytics ExperienceEvent](assets/schema-analytics-extension.png){zoomable="yes"}

* Crea payload XDM nell&#39;app, in conformità al gruppo di campi Estensione completa Adobe Analytics ExperienceEvent, in modo simile a quanto fatto nella lezione [Tracciare dati evento](events.md), oppure
* Crea regole nella proprietà Tags che utilizzano azioni regola per allegare o modificare dati al gruppo di campi Estensione completa Adobe Analytics ExperienceEvent. Per ulteriori dettagli, vedere [Allega dati a eventi SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) o [Modifica dati in eventi SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### eVar per merchandising

Se utilizzi [eVar di merchandising](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars) nella configurazione di Analytics, devi estendere il payload XDM definito in [Traccia dati evento](events.md) per acquisire tali informazioni di merchandising. Esempio di var merchandising: `evar1` dove desideri acquisire il colore dei prodotti, ad esempio `&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`

* In JSON:

  ```json
  {
    "productListItems": [
        {
            "SKU": "LLWS05.1-XS",
            "name": "Desiree Fitness Tee",
            "priceTotal": 24,
            "_experience": {
                "analytics": {
                    "events1to100": {
                        "event10": {
                            "value": 50
                        }
                    },
                    "customDimensions": {
                        "eVars": {
                            "eVar1": "red",
                        }
                    }
                }
            }
        }
    ],
    "eventType": "commerce.productListAdds",
    "commerce": {
        "productListAdds": {
            "value": 1
        }
    }
  }
  ```

* Nel codice:

  ```swift
  var xdmData: [String: Any] = [
    "productListItems": [
      [
        "name":  productName,
        "SKU": sku,
        "priceTotal": priceString,
        "_experience" : [
          "analytics": [
            "events1to100": [
              "event10": [
                "value:": value
              ]
            ],
            "customDimensions": [
              "eVars": [
                "eVar1": color
              ]
            ]
          ]
        ]
      ]
    ],
    "eventType": "commerce.productViews",
    "commerce": [
      "productViews": [
        "value": 1
      ]
    ]
  ]
  ```


### Utilizzare le regole di elaborazione

Di seguito è riportato un esempio di regola di elaborazione che utilizza questi dati:

* **[!UICONTROL Sovrascrivi il valore di]** (1) **[!UICONTROL Nome schermo app (eVar2)]** (2) con il valore di **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) se **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL è impostato]** (5).

* **[!UICONTROL Imposta evento]** (6) **[!UICONTROL Aggiungi alla lista dei desideri (evento 3)]** (7) in **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) se **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL è impostato]** (10).

![regole di elaborazione di analytics](assets/analytics-processing-rules.png){zoomable="yes"}

>[!IMPORTANT]
>
>
>Alcune delle variabili mappate automaticamente potrebbero non essere disponibili per l’utilizzo nelle regole di elaborazione.
>
>
>La prima volta che esegui il mapping a una regola di elaborazione, l’interfaccia non mostra le variabili di dati di contesto dall’oggetto XDM. Per risolvere il problema, seleziona un valore qualsiasi, Salva e torna per modificarlo. Verranno visualizzate tutte le variabili XDM.


Vedi [Mappare le variabili contextData in prop ed eVar con regole di elaborazione](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules).

>[!TIP]
>
>A differenza delle precedenti implementazioni di app mobili, non esiste alcuna distinzione tra visualizzazioni di pagina/schermo e altri eventi. È invece possibile incrementare la metrica **[!UICONTROL Visualizzazione pagina]** impostando la dimensione **[!UICONTROL Nome pagina]** in una regola di elaborazione. Poiché stai raccogliendo il campo `screenName` personalizzato nell&#39;esercitazione, si consiglia vivamente di mappare il nome della schermata a **[!UICONTROL Nome pagina]** in una regola di elaborazione.

## Migrare dall’estensione Analytics per dispositivi mobili

Se hai sviluppato la tua app mobile utilizzando l&#39;[estensione per dispositivi mobili Adobe Analytics](https://developer.adobe.com/client-sdks/solution/adobe-analytics/#add-analytics-to-your-application), probabilmente hai utilizzato [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackaction) e [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackstate) chiamate API.

Se decidi di eseguire la migrazione per utilizzare l’Edge Network consigliato, puoi scegliere:

* Implementa l&#39;estensione [Edge Network](configure-tags.md#extension-configuration) e utilizza le API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent), come illustrato nella lezione su come [tenere traccia dei dati evento](events.md). Questa esercitazione si concentra su questa implementazione.
* Implementa l&#39;estensione [Edge Bridge](https://developer.adobe.com/client-sdks/solution/adobe-analytics/migrate-to-edge-network/#implement-the-edge-bridge-extension) e continua a utilizzare le tue chiamate API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackaction) e [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackstate). Consulta [Implementare l&#39;estensione Edge Bridge](https://developer.adobe.com/client-sdks/solution/adobe-analytics/migrate-to-edge-network/#implement-the-edge-bridge-extension) per ulteriori dettagli e un&#39;esercitazione separata.




>[!SUCCESS]
>
>Hai configurato l’app per mappare gli oggetti XDM di Experience Edge alle variabili di Adobe Analytics abilitando il servizio Adobe Analytics nello stream di dati. E utilizzando le regole di elaborazione, se del caso.<br/> Grazie per aver dedicato il tuo tempo all&#39;apprendimento di Adobe Experience Platform Mobile SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Invia dati ad Experience Platform](platform.md)**
