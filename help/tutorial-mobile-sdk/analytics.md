---
title: Mappatura di Analytics
description: Scopri come raccogliere dati per Adobe Analytics in un’app mobile.
solution: Data Collection,Experience Platform,Analytics
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Mappatura di Analytics

Scopri come mappare i dati mobili su Adobe Analytics.

Il [evento](events.md) i dati raccolti e inviati a Platform Edge Network nelle lezioni precedenti vengono inoltrati ai servizi configurati nel flusso di dati, incluso Adobe Analytics. È sufficiente mappare i dati alle variabili corrette nella suite di rapporti.

## Prerequisiti

* Informazioni sul tracciamento ExperienceEvent.
* Invio dei dati XDM nell&#39;app di esempio completato.
* Stream di dati configurato per Adobe Analytics

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Comprendere la mappatura automatica delle variabili di Analytics.
* Imposta le regole di elaborazione per mappare i dati XDM sulle variabili di Analytics.

## Mappatura automatica

Molti dei campi XDM standard sono mappati automaticamente alle variabili di Analytics. Vedi l’elenco completo [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Esempio #1 - s.products

Un buon esempio è il [variabile dei prodotti](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) che non può essere compilato utilizzando le regole di elaborazione. Con un’implementazione XDM, trasmetti tutti i dati necessari in productListItems e s.products vengono compilati automaticamente tramite la mappatura di Analytics.

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

Si otterrebbe quanto segue:

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>Attualmente `productListItems[N].SKU` viene ignorato dalla mappatura automatica.

### Esempio #2 - scAdd

Se osservi attentamente, tutti gli eventi hanno due campi `value` (obbligatorio) e `id` (facoltativo). Il `value` per incrementare il conteggio degli eventi. Il `id` viene utilizzato per la serializzazione.

Questo oggetto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

Si otterrebbe quanto segue:

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

Si otterrebbe quanto segue:

```
s.events = "scAdd:321435"
```

## Convalida con garanzia

Utilizzo di [Strumento di controllo qualità Assurance](assurance.md) puoi confermare che stai inviando un ExperienceEvent, che i dati XDM sono corretti e che la mappatura di Analytics sta avvenendo come previsto. Ad esempio:

1. Invia un evento productListAdds.

   ```swift
   var xdmData: [String: Any] = [
     "eventType": "commerce.productListAdds",
     "commerce": [
       "productListAdds": [
         "value": 1
       ]
     ],
     "productListItems": [
       [
         "name": "neve studio dance jacket - (blue)",
         "SKU": "test-sku",
         "priceTotal": 69
       ]
     ]
   ]
   let addToCartEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: addToCartEvent)
   ```

1. Visualizza l’hit ExperienceEvent.

   ![hit xdm di analytics](assets/mobile-analytics-assurance-xdm.png)

1. Esamina la porzione XDM del JSON.

   ```json
     "xdm" : {
       "productListItems" : [ {
         "priceTotal" : 69,
         "SKU" : "test-sku",
         "name" : "neve studio dance jacket - (blue)"
       } ],
       "timestamp" : "2021-10-22T22:03:37Z",
       "commerce" : {
         "productListAdds" : {
           "value" : 1
         }
       },
       "eventType" : "commerce.productListAdds",
       //...
     }
   ```

1. Rivedi `analytics.mapping` evento.

   ![hit xdm di analytics](assets/mobile-analytics-assurance-mapping.png)

Osserva quanto segue nella mappatura di Analytics:

* &#39;events&#39; è stato popolato con &#39;scAdd&#39; basato su `commerce.productListAdds`.
* &#39;pl&#39; (variabile prodotti) è stato compilato con un valore concatenato basato su `productListItems`.
* In questo evento sono disponibili altre informazioni interessanti, inclusi tutti i dati contestuali.


## Mappatura con dati contestuali

I dati XDM inoltrati ad Analytics vengono convertiti in [dati contestuali](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) inclusi i campi standard e personalizzati.

La chiave dei dati contestuali è costruita seguendo questa sintassi:

```
a.x.[xdm path]
```

Ad esempio:

```
//Standard Field
a.x.commerce.saveforlaters.value

//Custom Field
a.x._techmarketingdemos.appinformationa.appstatedetails.screenname
```

>[!NOTE]
>
>I campi personalizzati si trovano sotto l’identificatore dell’organizzazione di Experience Cloud.
>
>&quot;_techmarketingdemos&quot; viene sostituito con il valore univoco della tua organizzazione.

Di seguito è riportato un esempio di regola di elaborazione che utilizza questi dati:

![regole di elaborazione di analytics](assets/mobile-analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Alcune delle variabili mappate automaticamente potrebbero non essere disponibili per l’utilizzo nelle regole di elaborazione.
>
>
>La prima volta che esegui il mapping a una regola di elaborazione, l’interfaccia utente non mostra le variabili di dati di contesto dall’oggetto XDM. Per risolvere il problema, seleziona un valore qualsiasi, Salva e torna per modificarlo. Verranno visualizzate tutte le variabili XDM.


Ulteriori informazioni sulle regole di elaborazione e sui dati contestuali sono disponibili [qui](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>A differenza delle precedenti implementazioni di app mobili, non esiste alcuna distinzione tra visualizzazioni pagina/schermata e altri eventi. È invece possibile incrementare **[!UICONTROL Visualizzazione pagina]** metrica impostando la **[!UICONTROL Nome pagina]** dimensione in una regola di elaborazione. Poiché stai raccogliendo il `screenName` nell’esercitazione, si consiglia vivamente di mappare questo campo su **[!UICONTROL Nome pagina]** in una regola di elaborazione.


Successivo: **[Experience Platform](platform.md)**

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)