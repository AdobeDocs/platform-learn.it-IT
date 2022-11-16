---
title: Implementare un livello di dati su una pagina di prodotto
description: Implementare un livello di dati su una pagina di prodotto
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Implementare un livello di dati su una pagina di prodotto

Per questa esercitazione, implementerai Adobe Client Data Layer per un tipico sito web di e-commerce. Se non lo hai già fatto, leggi [Come utilizzare Adobe Client Data Layer](how-to-use-the-adobe-client-data-layer.md) in primo luogo, per comprendere il funzionamento di Adobe Client Data Layer.

Supponiamo che l&#39;utente esplori i tuoi prodotti e clicchi su un rullo di schiuma per saperne di più. L&#39;utente arriva sulla pagina dei dettagli del prodotto del rullo di schiuma.

Ecco il HTML per la tua semplice pagina dei dettagli del prodotto:

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

Come avrete notato, all&#39;interno del `<head>` è presente un tag `<script>` tag . In questo punto inserirai il codice JavaScript. Non è necessario posizionare il `<script>` tag in `<head>`, ma l’invio dei dati al livello dati il prima possibile garantisce che sia rapidamente disponibile per l’addetto al marketing da inviare a Adobe Experience Platform prima che l’utente lasci la pagina.

Dentro `<script>` per iniziare, crea il `adobeDataLayer` e quindi inserire nell&#39;array le informazioni relative all&#39;evento e ai dati appropriati. I dati sono conformi allo schema XDM [creato in precedenza](../configure-the-server/create-a-schema.md).

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

In questo esempio, hai effettuato due passaggi al livello dati, ciascuno contenente un `event` chiave. Includere un `event` non solo comunica l’evento che si è verificato sulla pagina, ma rende anche più semplice per l’addetto al marketing creare regole appropriate all’interno dei tag Adobe Experience Platform.

Il primo push al livello dati notifica agli ascoltatori (regole dei tag) che l’utente ha visualizzato la pagina. Aggiunge inoltre il nome della pagina e la sezione del sito al livello dati.

Il secondo push al livello dati notifica agli ascoltatori (regole dei tag) che l’utente ha visualizzato un prodotto. Aggiunge anche informazioni sul prodotto al livello dati.

## Aggiungi al carrello

È inoltre probabile che si desideri tenere traccia di quando l&#39;utente fa clic sul [!UICONTROL Aggiungi al carrello] pulsante .

A questo scopo, crea una funzione che viene chiamata quando l&#39;utente fa clic sul pulsante [!UICONTROL Aggiungi al carrello] pulsante .

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

Quando questa funzione viene chiamata, controlla innanzitutto se esiste già un carrello per un utente. In genere, questo viene fatto controllando se esiste un particolare cookie o variabile. Se il carrello non esiste, invierai un push `cartOpened` nel livello dati. Successivamente, premi un `productAddedToCart` nel livello dati. Le informazioni sul prodotto esistono già nel livello dati, quindi non è necessario aggiungerle di nuovo.

Aggiungi un `onclick` attributo [!UICONTROL Aggiungi al carrello] pulsante che chiama il nuovo `onAddToCartClick` funzione .

Il risultato della pagina HTML deve essere il seguente:

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

Un&#39;ultima cosa da fare è tenere traccia di quando l&#39;utente fa clic sul pulsante _[!UICONTROL Scaricare l’app]_ link.

A questo scopo, crea una funzione che viene chiamata quando l&#39;utente fa clic sul pulsante _[!UICONTROL Scaricare l’app]_ link.

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

In questo caso, le informazioni sul collegamento sono racchiuse all’interno di un `eventInfo` chiave. Come discusso in [Come utilizzare Adobe Client Data Layer](how-to-use-the-adobe-client-data-layer.md), questo comunica al livello dati di comunicare questi dati insieme all’evento, ma a _not_ conserva i dati all’interno del livello dati. Per un clic su un collegamento, non è utile aggiungere informazioni sul collegamento selezionato al livello dati perché non riguarda la pagina nel suo complesso e non è applicabile ad altri eventi che possono verificarsi.

Aggiungi un `onclick` attributo [!UICONTROL Scaricare l’app] collegamento che chiama il nuovo `onDownloadAppClick` funzione .

Il risultato della pagina HTML deve essere il seguente:

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
