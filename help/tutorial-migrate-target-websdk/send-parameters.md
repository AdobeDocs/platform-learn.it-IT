---
title: Parametri di invio | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come inviare parametri mbox, di profilo e di entità ad Adobe Target utilizzando Experience Platform Web SDK.
source-git-commit: 10dbc8ecbfee511a97e64cb571c43dbf05e3076c
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 1%

---

# Inviare parametri a Target tramite SDK per web di Platform

Le implementazioni di Target differiscono tra i siti web a causa dell’architettura del sito, dei requisiti aziendali e delle funzioni utilizzate. La maggior parte delle implementazioni di Target includono il passaggio di vari parametri per informazioni contestuali, tipi di pubblico e consigli sui contenuti.

Usiamo una semplice pagina dei dettagli del prodotto e una pagina di conferma dell’ordine per dimostrare le differenze tra le librerie quando trasmetti i parametri a Target.

Supponiamo di avere due pagine di esempio utilizzando at.js:

+++at.js in una pagina Dettagli prodotto:

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
        "pageName": "product detail",
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

+++


+++at.js in una pagina di conferma dell’ordine:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>-->
  <!--Target parameters -->
  <script>
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
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++


## Riepilogo della mappatura dei parametri

I parametri di Target per queste pagine vengono inviati in modo diverso utilizzando l’SDK per web di Platform. Esistono diversi modi per trasmettere parametri a Target utilizzando at.js:

- Imposta con `targetPageParams()` funzione per l’evento di caricamento della pagina
- Imposta con `targetPageParamsAll()` funzione per tutte le richieste Target nella pagina
- Invia i parametri direttamente con il `getOffer()` funzione per una singola posizione
- Invia i parametri direttamente con il `getOffers()` funzione per una o più posizioni

Per questi esempi, il `targetPageParams()` viene utilizzato l&#39;approccio .

L’SDK per web di Platform fornisce un unico modo coerente per inviare i dati senza la necessità di ulteriori funzioni. Tutti i parametri devono essere passati nel payload con il `sendEvent` comando.

Parametri passati con l’SDK per web di Platform `sendEvent` il carico utile rientra in due categorie:

1. Mappata automaticamente dal `xdm` oggetto
1. Passati manualmente utilizzando `data.__adobe.target` oggetto

La tabella seguente illustra il modo in cui i parametri di esempio verranno rimappati utilizzando l’SDK per web di Platform:

| Esempio di parametro at.js | Opzione SDK per web di Platform | Note |
| --- | --- | --- |
| `at_property` | N/D | I token di proprietà sono configurati nel [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) e non può essere impostato nel `sendEvent` chiama. |
| `pageName` | `xdm.web.webPageDetails.name` | Tutti i parametri mbox di Target devono essere trasmessi come parte del `xdm` e sono conformi a uno schema utilizzando la classe ExperienceEvent XDM. I parametri mbox non possono essere passati come parte del `data` oggetto. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Tutti i parametri di profilo di Target devono essere passati come parte del `data` oggetto con prefisso `profile.` da mappare in modo appropriato. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Parametro riservato utilizzato per la funzione di affinità tra categorie di Target che deve essere trasmesso come parte del `data` oggetto. |
| `entity.id` | `data.__adobe.target.entity.id` <br>O<br> `xdm.productListItems[0].SKU` | Gli ID di entità vengono utilizzati per i contatori comportamentali Recommendations di Target. Questi ID entità possono essere passati come parte del `data` oggetto o mappato automaticamente dal primo elemento nel `xdm.productListItems` se l&#39;implementazione utilizza quel gruppo di campi. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Gli ID delle categorie di entità possono essere passati come parte del `data` oggetto. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | I parametri di entità personalizzati vengono utilizzati per aggiornare il catalogo dei prodotti Recommendations. Questi parametri personalizzati devono essere passati come parte del `data` oggetto. |
| `cartIds` | `data.__adobe.target.cartIds` | Utilizzato per gli algoritmi di consigli basati su cart di Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Utilizzato per impedire la restituzione di ID entità specifici in una progettazione di consigli. |
| `mbox3rdPartyId` | Impostato in identityMap. Vedi [Sincronizzazione dei profili con un ID cliente](#synching-profiles-with-a-customer-id) | Utilizzato per sincronizzare i profili Target tra dispositivi e attributi cliente. Lo spazio dei nomi da utilizzare per l’ID cliente deve essere specificato nella variabile [Configurazione di destinazione del datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Utilizzato per identificare un ordine univoco per il tracciamento delle conversioni di Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Utilizzato per tenere traccia dei totali degli ordini per gli obiettivi di conversione e ottimizzazione di Target. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>O<br> `xdm.productListItems[0-n].SKU` | Utilizzato per il tracciamento delle conversioni di Target e gli algoritmi di consigli. Fai riferimento a [parametri di entità](#entity-parameters) per ulteriori informazioni. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Utilizzato per [punteggio personalizzato](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) obiettivo dell’attività. |

{style=&quot;table-layout:auto&quot;}

## Parametri personalizzati

Tutti i parametri mbox personalizzati devono essere trasmessi come dati XDM con `sendEvent` comando. È importante assicurarsi che lo schema XDM includa tutti i punti dati necessari per l’implementazione di Target.

esempio at.js utilizzando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "pageName": "product detail"
  };
};
```

Esempi JavaScript dell’SDK per web di Platform che utilizzano `sendEvent` comando:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "name": "product detail"
      }
    }
  }
});
```

>[!TAB Tag]

Nei tag, utilizza innanzitutto un [!UICONTROL Oggetto XDM] elemento dati da mappare al campo XDM:

![Mappatura a un campo XDM in un elemento dati oggetto XDM](assets/params-tags-pageName.png){zoomable=&quot;yes&quot;}

E poi includi il tuo [!UICONTROL Oggetto XDM] nel tuo [!UICONTROL Invia evento] [!UICONTROL action] (multiplo) [!UICONTROL Oggetti XDM] può [unito](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inclusione di un elemento dati oggetto XDM in un evento Send](assets/params-tags-sendEvent.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]


>[!NOTE]
>
>Poiché i parametri mbox personalizzati fanno parte di `xdm` oggetto è necessario aggiornare i tipi di pubblico, le attività o gli script di profilo che fanno riferimento a questi parametri mbox utilizzando i loro nuovi nomi. Consulta la sezione [Aggiornare i tipi di pubblico e gli script di profilo di Target per la compatibilità con l’SDK per web di Platform](update-audiences.md) per ulteriori informazioni.


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

Esempi SDK per web di Platform che utilizzano `sendEvent` comando:

>[!BEGINTABS]

>[!TAB JavaScript]

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

>[!TAB Tag]

Nei tag, crea prima un elemento dati per definire il `data.__adobe.target` oggetto:

![Definizione dell’oggetto dati in un elemento dati](assets/params-tags-dataObject.png){zoomable=&quot;yes&quot;}

e quindi includere l&#39;oggetto dati nel [!UICONTROL Invia evento] [!UICONTROL action] (multiplo) [!UICONTROL oggetti] può [unito](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inclusione di un oggetto dati in un evento Send](assets/params-tags-sendEvent-withData.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

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

Esempi SDK per web di Platform che utilizzano `sendEvent` comando:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

>[!TAB Tag]

Nei tag, crea prima un elemento dati per definire il `data.__adobe.target` oggetto:

![Definizione dell’oggetto dati in un elemento dati](assets/params-tags-dataObject-entities.png){zoomable=&quot;yes&quot;}

e quindi includere l&#39;oggetto dati nel [!UICONTROL Invia evento] [!UICONTROL action] (multiplo) [!UICONTROL oggetti] può [unito](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inclusione di un oggetto dati in un evento Send](assets/params-tags-sendEvent-withData.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]





Tutto [parametri di entità](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) supportati da at.js sono anche supportati dall’SDK per web di Platform.

>[!NOTE]
>
>Se la `commerce` viene utilizzato il gruppo di campi e `productListItems` array è incluso nel payload XDM, quindi il primo `SKU` valore in questo array mappato a `entity.id` per incrementare una visualizzazione del prodotto.


## Parametri di acquisto

I parametri di acquisto vengono passati in una pagina di conferma dell’ordine dopo un ordine eseguito correttamente e vengono utilizzati per gli obiettivi di conversione e ottimizzazione di Target. Con un’implementazione Platform Web SDK, questi parametri e vengono mappati automaticamente dai dati XDM trasmessi come parte del `commerce` gruppo di campi.

esempio at.js utilizzando `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

Le informazioni di acquisto vengono trasmesse a Target quando `commerce` gruppo di campi `purchases.value` impostato su `1`. L&#39;ID ordine e il totale dell&#39;ordine vengono mappati automaticamente dal `order` oggetto. Se la `productListItems` l&#39;array è presente, quindi il `SKU` vengono utilizzati per `productPurchasedId`.

Esempi SDK per web di Platform che utilizzano `sendEvent` comando:

>[!BEGINTABS]

>[!TAB JavaScript]

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

>[!TAB Tag]

Nei tag, utilizza innanzitutto un [!UICONTROL Oggetto XDM] elemento dati da mappare ai campi XDM:

![Mappatura a un campo XDM in un elemento dati oggetto XDM](assets/params-tags-purchase.png){zoomable=&quot;yes&quot;}

E poi includi il tuo [!UICONTROL Oggetto XDM] nel tuo [!UICONTROL Invia evento] [!UICONTROL action] (multiplo) [!UICONTROL Oggetti XDM] può [unito](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inclusione di un elemento dati oggetto XDM in un evento Send](assets/params-tags-sendEvent-purchase.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]


>[!NOTE]
>
>La `productPurchasedId` può anche essere passato come un elenco di ID di entità separati da virgole sotto `data` oggetto.


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

Esempi SDK per web di Platform che utilizzano `sendEvent` comando:

>[!BEGINTABS]

>[!TAB JavaScript]

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

>[!TAB Tag]

La [!UICONTROL ID] valore, [!UICONTROL Stato autenticato] e [!UICONTROL Namespace] vengono catturati in un [!UICONTROL Mappa identità] elemento dati:
![Elemento dati Identity Map che acquisisce l’ID cliente](assets/params-tags-customerIdDataElement.png){zoomable=&quot;yes&quot;}

La [!UICONTROL Mappa identità] viene quindi utilizzato per impostare [!UICONTROL identityMap] nel campo [!UICONTROL Oggetto XDM] elemento dati:
![Elemento dati Identity Map utilizzato nell’elemento dati oggetto XDM](assets/params-tags-customerIdInXDMObject.png){zoomable=&quot;yes&quot;}

La [!UICONTROL Oggetto XDM] viene quindi incluso nel [!UICONTROL Invia evento] azione di una regola:

![Inclusione di un elemento dati oggetto XDM in un evento Send](assets/params-tags-sendEvent-xdm.png){zoomable=&quot;yes&quot;}

Nel servizio Adobe Target del datastream, assicurati di impostare il [!UICONTROL Spazio dei nomi ID di terze parti di destinazione] allo stesso namespace utilizzato nel [!UICONTROL Mappa identità] elemento dati
![Impostare lo spazio dei nomi ID di terze parti di Target nel datastream](assets/params-tags-customerIdNamespaceInDatastream.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

## Esempio di SDK per web Platform

Ora che sai in che modo i diversi parametri di Target vengono mappati utilizzando l’SDK per web di Platform, le nostre due pagine di esempio possono essere migrate da at.js all’SDK per web di Platform, come illustrato di seguito. Le pagine di esempio includono quanto segue:

- Frammento pre-hiding di Target per un&#39;implementazione asincrona della libreria
- Codice di base dell’SDK per web di Platform
- Libreria JavaScript SDK per web Platform
- A `configure` comando per inizializzare la libreria
- A `sendEvent` invio di dati e richiesta di rendering del contenuto Target

+++SDK web in una pagina Dettagli prodotto:

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
            "pageName": "product detail"
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

+++

+++SDK web in una pagina di conferma dell’ordine:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>


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

+++

Quindi, scopri come [tenere traccia degli eventi di conversione di Target](track-events.md) con Platform Web SDK.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
