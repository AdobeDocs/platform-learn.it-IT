---
title: Implementare un livello di dati su una pagina di prodotto
description: Implementare un livello di dati su una pagina di prodotto
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Implementare un livello di dati su una pagina di prodotto

Per questo tutorial, implementerai Adobe Client Data Layer per un tipico sito web di e-commerce. Se non lo hai già fatto, leggi [Come utilizzare Adobe Client Data Layer](how-to-use-the-adobe-client-data-layer.md) innanzitutto per comprendere come funziona Adobe Client Data Layer.

Supponiamo che l’utente sfoglia i tuoi prodotti e faccia clic su un rullo di schiuma per saperne di più. L’utente arriva alla pagina dei dettagli del prodotto del rullo di schiuma.

Ecco le HTML per la pagina dei dettagli del prodotto:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

Come avrete notato, all&#39;interno del `<head>` tag esiste un `<script>` tag. Inserire qui il codice JavaScript. Non è necessario inserire `<script>` tag in `<head>`, ma inviare i dati al livello dati il prima possibile garantisce che siano rapidamente disponibili per l’addetto marketing per l’invio a Adobe Experience Platform prima che l’utente lasci la pagina.

All&#39;interno del `<script>` , si inizierà creando il tag `adobeDataLayer` e quindi di inserire nell&#39;array le informazioni appropriate su eventi e dati. I dati sono conformi allo schema XDM [creato in precedenza](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

In questo esempio, hai effettuato due push al livello dati, ciascuno contenente un `event` chiave. Inclusione di un `event` key non solo comunica quale evento si è verificato sulla pagina, ma semplifica anche la creazione di regole appropriate all’interno dei tag Adobe Experience Platform da parte dell’addetto marketing.

Il primo invio al livello dati avvisa i listener (regole per i tag) che l’utente ha visualizzato la pagina. Aggiunge anche il nome della pagina e la sezione del sito al livello dati.

Il secondo invio al livello dati avvisa i listener (regole per i tag) che l’utente ha visualizzato un prodotto. Aggiunge inoltre informazioni sul prodotto al livello dati.

## Aggiungi al carrello

Puoi anche voler tracciare quando l’utente fa clic sul pulsante [!UICONTROL Aggiungi al carrello] pulsante.

A questo scopo, crea una funzione denominata quando l’utente fa clic sul pulsante [!UICONTROL Aggiungi al carrello] pulsante.

```js
window.onAddToCartClick = function() {
  // In a real implementation, you would change this condition to 
  // only pass if a cart doesn't already exist. You would typically 
  // do this by checking a cookie or variable value.
  if (true) {
    window.adobeDataLayer.push({
      "event": "cartOpened",
    });
  }
  window.adobeDataLayer.push({
    "event": "productAddedToCart"
  });
};
```

Quando viene chiamata questa funzione, verifica innanzitutto se per un utente esiste già un carrello. In genere, questo può essere fatto verificando se esiste un cookie o una variabile particolare. Se il carrello non esiste, eseguirai un’operazione push `cartOpened` nel livello dati. Successivamente, eseguirai un’operazione push `productAddedToCart` nel livello dati. Le informazioni sul prodotto esistono già nel livello dati, quindi non è necessario aggiungerle nuovamente.

Aggiungi un `onclick` attribuire a [!UICONTROL Aggiungi al carrello] pulsante che chiama il nuovo `onAddToCartClick` funzione.

Il risultato della pagina HTML dovrebbe essere il seguente:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## Scaricare l’app

Un’ultima cosa da fare è tenere traccia di quando l’utente fa clic su _[!UICONTROL Scaricare l’app]_ collegamento.

A questo scopo, crea una funzione denominata quando l’utente fa clic sul pulsante _[!UICONTROL Scaricare l’app]_ collegamento.

```js
window.onDownloadAppClick = function(event) {
  window.adobeDataLayer.push({
    "event": "downloadAppClicked",
    "eventInfo": {
      "web": {
        "webInteraction": {
          "URL": "https://example.com/download",
          "name": "App Download",
          "type": "download"
        }
      }
    }
  });
};
```

In questo caso, le informazioni sul collegamento sono racchiuse in un `eventInfo` chiave. Come discusso in [Come utilizzare Adobe Client Data Layer](how-to-use-the-adobe-client-data-layer.md), questo comunica al livello dati di comunicare questi dati insieme all’evento, ma a _non_ conservare i dati all’interno del livello dati. Per un clic su un collegamento, non è utile aggiungere informazioni sul collegamento su cui è stato fatto clic al livello dati, perché non riguarda la pagina nel suo insieme e non è applicabile ad altri eventi che possono verificarsi.

Aggiungi un `onclick` attribuire a [!UICONTROL Scaricare l’app] collegamento che chiama il nuovo `onDownloadAppClick` funzione.

Il risultato della pagina HTML dovrebbe essere il seguente:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
        window.adobeDataLayer.push({
          "event": "downloadAppClicked",
          "eventInfo": {
            "web": {
              "webInteraction": {
                "URL": "https://example.com/download",
                "name": "App Download",
                "type": "download"
              }
            }
          }
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
