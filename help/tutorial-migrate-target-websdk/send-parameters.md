---
title: Parametri di invio | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come inviare parametri mbox, di profilo e di entità ad Adobe Target utilizzando Experience Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---

# Inviare parametri a Target tramite SDK per web di Platform

Le implementazioni di Target differiscono tra i siti web a causa dell’architettura del sito, dei requisiti aziendali e delle funzioni utilizzate. La maggior parte delle implementazioni di Target includono il passaggio di vari parametri per informazioni contestuali, tipi di pubblico e consigli sui contenuti.

Usiamo una semplice pagina dei dettagli del prodotto e una pagina di conferma dell’ordine per dimostrare le differenze tra le librerie quando trasmetti i parametri a Target.

Supponiamo che la pagina di esempio seguente utilizzi at.js:

<!--Assume the following two example pages using at.js:-->

Dettagli del prodotto:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Mbox parameters
        "siteSection": "product details",
        // Profile parameters
        "profile.gender": "male",
        "user.categoryId": "clothing",
        // Entity parameters for Target Recomendations
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL",
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

<!--

Order Confirmation:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>-->
<!--Target parameters -->
<!--  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Order confirmation parameters
        "orderId": "ABC123",
        "productPurchasedId": "SKU-00002,SKU-00003",
        "orderTotal": 1337.89,
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>-->
<!--Target at.js library loaded asynchonously-->
<!--  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```
-->


## Riepilogo della mappatura dei parametri

I parametri Target utilizzati in queste due pagine di esempio devono essere inviati in modo leggermente diverso utilizzando l’SDK per web di Platform. Esistono diversi modi per trasmettere parametri a Target utilizzando at.js:

- Imposta con `targetPageParams()` funzione per l’evento di caricamento della pagina
- Imposta con `targetPageParamsAll()` funzione per tutte le richieste Target nella pagina
- Invia i parametri direttamente con il `getOffer()` funzione per una singola posizione
- Invia i parametri direttamente con il `getOffers()` funzione per una o più posizioni

Ai fini del presente esempio, il `targetPageParams()` viene utilizzato l&#39;approccio .

L’SDK per web di Platform semplifica questa operazione fornendo un unico modo coerente di inviare i dati senza la necessità di ulteriori funzioni. Tutti i parametri devono essere passati nel payload con il `sendEvent` comando.

Parametri passati con l’SDK per web di Platform `sendEvent` il carico utile rientra in due categorie:

1. Mappata automaticamente dal `xdm` oggetto
1. Passati manualmente utilizzando `data.__adobe.target` oggetto

La tabella seguente illustra il modo in cui i parametri di esempio verranno rimappati utilizzando l’SDK per web di Platform:

| Esempio di parametro at.js | Opzione SDK per web di Platform | Note |
| --- | --- | --- |
| `at_property` | N/D | I token di proprietà sono configurati nel [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) e non può essere impostato nel `sendEvent` chiama. |
| `siteSection` | `xdm.web.webPageDetails.siteSection` | Tutti i parametri mbox di Target devono essere trasmessi come parte del `xdm` e sono conformi a uno schema utilizzando la classe ExperienceEvent XDM. I parametri mbox non possono essere passati come parte del `data` oggetto. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Tutti i parametri di profilo di Target devono essere passati come parte del `data` oggetto con prefisso `profile.` da mappare in modo appropriato. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parametro riservato utilizzato per la funzione di affinità tra categorie di Target che deve essere trasmesso come parte del `data` oggetto. |
| `entity.id` | `data.__adobe.target.entity.id` <br>O<br> `xdm.productListItems[0].SKU` | Gli ID di entità vengono utilizzati per i contatori comportamentali Recommendations di Target. Questi ID entità possono essere passati come parte del `data` oggetto o mappato automaticamente dal primo elemento nel `xdm.productListItems` se l&#39;implementazione utilizza quel gruppo di campi. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Gli ID delle categorie di entità possono essere passati come parte del `data` oggetto. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | I parametri di entità personalizzati vengono utilizzati per aggiornare il catalogo dei prodotti Recommendations. Questi parametri personalizzati devono essere passati come parte del `data` oggetto. |
| `cartIds` | `data.__adobe.target.cartIds` | Utilizzato per gli algoritmi di consigli basati su cart di Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Utilizzato per impedire la restituzione di ID entità specifici in una progettazione di consigli. |
| `mbox3rdPartyId` | Impostato in identityMap. Vedi [Sincronizzazione dei profili con un ID cliente](#synching-profiles-with-a-customer-id) | Utilizzato per sincronizzare i profili Target tra dispositivi e attributi cliente. Lo spazio dei nomi da utilizzare per l’ID cliente deve essere specificato nella variabile [Configurazione di destinazione del datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |

{style=&quot;table-layout:auto&quot;}

<!--
| `orderId` | `xdm.commerce.order.purchaseID` | Used for identifying a unique order for Target conversion tracking. | 
| `orderTotal` | `xdm.commerce.order.priceTotal` | Used for tracking order totals for Target conversion and optimization goals. | 
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>OR<br> `xdm.productListItems[0-n].SKU` | Used for Target conversion tracking and recommendations algorithms. Refer to the [entity parameters](#entity-parameters) section below for details. | 
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Used for the [custom scoring](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) activity goal. | -->


## Parametri personalizzati

Tutti i parametri mbox personalizzati devono essere trasmessi come dati XDM con `sendEvent` comando. È importante assicurarsi che lo schema XDM includa tutti i punti dati necessari per l’implementazione di Target.

esempio at.js utilizzando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "siteSection": "product detail"
  };
};
```

Esempio di SDK per web Platform tramite `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "siteSection": "product detail"
      }
    }
  }
});
```

>[!NOTE]
>
>Poiché i parametri mbox personalizzati devono essere inviati come parte di `xdm` nell&#39;oggetto `sendEvent` tutti i parametri mbox utilizzati nell’implementazione di at.js Target devono essere riassegnati a un equivalente XDM. Questo significa che devi aggiornare qualsiasi tipo di pubblico, attività o script di profilo che fa riferimento a questi parametri mbox.


## Parametri del profilo

I parametri di profilo di Target devono essere trasmessi sotto `data.__adobe.target` oggetto nell’SDK per web di Platform `sendEvent` payload del comando.

Analogamente a at.js, anche tutti i parametri di profilo devono essere preceduti da `profile.` affinché il valore sia correttamente memorizzato come attributo di profilo Target permanente. Riservato `user.categoryId` Il parametro per la funzionalità di affinità tra categorie di Target ha il prefisso `user.`.

esempio at.js utilizzando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

Esempio di SDK per web Platform tramite `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "male",
        "user.categoryId": "clothing"
      }
    }
  }
});
```

## Parametri entità

I parametri di entità vengono utilizzati per trasmettere dati comportamentali e informazioni di catalogo supplementari per Target Recommendations. Analogamente ai parametri di profilo, tutti i parametri di entità devono essere passati sotto `data.__adobe.target` oggetto nell’SDK per web di Platform `sendEvent` payload del comando.

I parametri di entità per un elemento specifico devono essere preceduti da `entity.` per una corretta acquisizione dei dati. Riservato `cartIds` e `excludedIds` i parametri per gli algoritmi di consigli non devono essere preceduti e il valore per ciascuno di essi deve contenere un elenco di ID di entità separati da virgole.

esempio at.js utilizzando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "entity.id": "SKU-00001-LARGE",
    "entity.categoryId": "clothing,shirts",
    "entity.customEntity": "some value",
    "cartIds": "SKU-00002,SKU-00003",
    "excludedIds": "SKU-00001-SMALL"
  };
};
```

Esempio di SDK per web Platform tramite `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts"
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

Tutto [parametri di entità](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) supportati da at.js sono anche supportati dall’SDK per web di Platform.

>[!NOTE]
>
>Se la `commerce` viene utilizzato il gruppo di campi e `productListItems` array è incluso nel payload XDM, quindi il primo `SKU` valore in questo array mappato a `entity.id` per incrementare una visualizzazione del prodotto.

<!-- 
## Purchase parameters

Purchase parameters are passed on an order confirmation page after a successful order and are used for Target conversion and optimization goals. With a Platform Web SDK implementation, these parameters and are automatically mapped from XDM data passed as part of the `commerce` field group.

at.js example using `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

Purchase information is passed to Target when the `commerce` field group has `puchases.value` set to `1`. The order ID and order total are automatically mapped from the `order` object. If the `productListItems` array is present, then the `SKU` values are use for `productPurchasedId`.

Platform Web SDK example using `sendEvent` command:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "ABC123",
        "priceTotal": 1337.89
      },
      "purchases": {
        "value": 1
      }
    },
    "productListItems": [{
      "SKU": "SKU-00002"
    }, {
      "SKU": "SKU-00003"
    }]
  }
});
```

>[!NOTE]
>
>The `productPurchasedId` value can also be passed as a comma-separated list of entity IDs under the `data` object.

-->

## Sincronizzazione dei profili con un ID cliente

Target consente la sincronizzazione dei profili tra dispositivi e sistemi utilizzando un singolo ID cliente. Con at.js, può essere impostato come `mbox3rdPartyId` nella richiesta Target o come primo ID cliente inviato al servizio Experience Cloud Identity. A differenza di at.js, un’implementazione SDK per web di Platform consente di specificare quale ID cliente usare come `mbox3rdPartyId` se ce ne sono più. Ad esempio, se la tua azienda dispone di un ID cliente globale e di ID cliente separati per diverse linee di business, puoi configurare quale ID Target deve utilizzare.

Sono disponibili alcuni passaggi per configurare la sincronizzazione ID per i casi di utilizzo tra dispositivi e attributi cliente di Target:

1. Crea un **[!UICONTROL spazio dei nomi identità]** per l&#39;ID cliente in **[!UICONTROL Identità]** schermata di raccolta dati o piattaforma
1. Assicurati che il **[!UICONTROL alias]** in Attributi del cliente corrisponde a **[!UICONTROL simbolo di identità]** dello spazio dei nomi
1. Specifica la **[!UICONTROL simbolo di identità]** come **[!UICONTROL Spazio dei nomi ID di terze parti di destinazione]** nella configurazione di Target del datastream
1. Esegui un `sendEvent` utilizzando il comando `identityMap` gruppo di campi

esempio at.js utilizzando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

Esempio di SDK per web Platform tramite `sendEvent` comando:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated"
      }]
    }
  }
});
```


## Esempio di SDK per web Platform

Ora che sai in che modo i diversi parametri di Target vengono mappati utilizzando l’SDK per web di Platform, le nostre due pagine di esempio possono essere migrate da at.js all’SDK per web di Platform, come illustrato di seguito. Le pagine di esempio includono quanto segue:

- Frammento pre-hiding di Target per un&#39;implementazione asincrona della libreria
- Codice di base dell’SDK per web di Platform
- Libreria JavaScript SDK per web Platform
- A `configure` comando per inizializzare la libreria
- A `sendEvent` invio di dati e richiesta di rendering del contenuto Target

Dettagli del prodotto:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "renderDecisions": true,
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "web": {
          "webPageDetails": {
            // Other attributes included according to XDM schema
            "siteSection": "product detail"
          }
        }
      },
      "data": {
        "__adobe": {
          "target": {
            "profile.gender": "male",
            "user.categoryId": "clothing",
            "entity.id": "SKU-00001-LARGE",
            "entity.categoryId": "clothing,shirts",
            "entity.customEntity": "some value",
            "cartIds": "SKU-00002,SKU-00003",
            "excludedIds": "SKU-00001-SMALL"
          }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

<!--
Order Confirmation:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>

-->
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<!--
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>
-->
<!--Platform Web SDK base code-->
<!--
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>
-->
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<!--  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
-->
<!--Configure Platform Web SDK and send event-->
<!--  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated"
          }]
        },
        "commerce": {
          "order": {
            "purchaseID": "ABC123",
            "priceTotal": 1337.89
          },
          "purchases": {
            "value": 1
          }
        },
        "productListItems": [{
          "SKU": "SKU-00002"
        }, {
          "SKU": "SKU-00003"
        }]
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```
-->

Quindi, scopri come [tenere traccia degli eventi di conversione di Target](track-events.md) con Platform Web SDK.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
