---
title: Mappatura di Analytics
description: Scopri come raccogliere dati per Adobe Analytics in un’app mobile.
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Mappatura di Analytics

Scopri come mappare i dati mobili su Adobe Analytics.

La [event](events.md) i dati raccolti e inviati a Platform Edge Network nelle lezioni precedenti vengono inoltrati ai servizi configurati nel datastream, incluso Adobe Analytics. È sufficiente mappare i dati sulle variabili corrette nella suite di rapporti.

## Prerequisiti

* Informazioni sul tracciamento di ExperienceEvent.
* L’invio dei dati XDM nell’app di esempio è riuscito.
* Datastream configurato in Adobe Analytics

## Finalità di apprendimento

In questa lezione:

* Comprendere la mappatura automatica delle variabili di Analytics.
* Imposta le regole di elaborazione per mappare i dati XDM sulle variabili di Analytics.

## Mappatura automatica

Molti dei campi XDM standard vengono mappati automaticamente alle variabili di Analytics. Vedi l’elenco completo [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Esempio n. 1 - s.products

Un buon esempio è la [variabile dei prodotti](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) che non può essere compilata utilizzando le regole di elaborazione. Con un’implementazione XDM, trasmetti tutti i dati necessari in productListItems e s.products vengono compilati automaticamente tramite la mappatura Analytics.

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

Ne consegue quanto segue:

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>Attualmente `productListItems[N].SKU` viene ignorato dalla mappatura automatica.

### Esempio n. 2 - scAdd

Se osservi attentamente, tutti gli eventi hanno due campi `value` (obbligatorio) e `id` (facoltativo). La `value` viene utilizzato per incrementare il conteggio degli eventi. La `id` viene utilizzato per la serializzazione.

Questo oggetto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

Ne consegue quanto segue:

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

Ne consegue quanto segue:

```
s.events = "scAdd:321435"
```

## Convalida con affidabilità

Utilizzo della [Strumento Controllo di qualità](assurance.md) Puoi confermare che stai inviando un ExperienceEvent, che i dati XDM sono corretti e che la mappatura di Analytics avviene come previsto. Ad esempio:

1. Invia un evento productListAdd .

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

1. Visualizza l&#39;hit ExperienceEvent .

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

1. Consulta la sezione `analytics.mapping` evento.

   ![hit xdm di analytics](assets/mobile-analytics-assurance-mapping.png)

Tieni presente quanto segue nella mappatura di Analytics:

* &#39;events&#39; è stato popolato con &#39;scAdd&#39; in base a `commerce.productListAdds`.
* &#39;pl&#39; (variabile prodotti) è stato compilato con un valore concatenato basato su `productListItems`.
* Ci sono altre informazioni interessanti in questo evento, compresi tutti i dati contestuali.


## Mappatura con i dati contestuali

I dati XDM inoltrati ad Analytics vengono convertiti in [dati contestuali](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) inclusi i campi standard e personalizzati.

La chiave di dati contestuali viene costruita seguendo questa sintassi:

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
>I campi personalizzati vengono inseriti sotto l’identificatore dell’organizzazione Experience Cloud.
>
>&quot;_techmarketingdemos&quot; viene sostituito con il valore univoco dell&#39;organizzazione.

Esempio di una regola di elaborazione che utilizza questi dati:

![regole di elaborazione di analytics](assets/mobile-analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Alcune delle variabili mappate automaticamente potrebbero non essere disponibili per l’utilizzo nelle regole di elaborazione.
>
>
>La prima volta che esegui la mappatura su una regola di elaborazione, l’interfaccia utente non mostra le variabili di dati di contesto dall’oggetto XDM. Per correggere la selezione di qualsiasi valore, salvare e tornare alla modifica. Ora devono essere visualizzate tutte le variabili XDM.


È possibile trovare ulteriori informazioni sulle regole di elaborazione e i dati contestuali [qui](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>A differenza delle implementazioni precedenti dell’app mobile, non esiste alcuna distinzione tra le visualizzazioni di pagina/schermo e altri eventi. Invece puoi incrementare il **[!UICONTROL Visualizzazione a pagina]** impostando **[!UICONTROL Nome pagina]** in una regola di elaborazione. Poiché stai raccogliendo l&#39;oggetto personalizzato `screenName` nell’esercitazione, si consiglia vivamente di eseguire la mappatura su **[!UICONTROL Nome pagina]** in una regola di elaborazione.


Avanti: **[Experience Platform](platform.md)**

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)