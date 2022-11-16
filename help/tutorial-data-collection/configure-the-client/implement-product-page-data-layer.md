---
title: Implementare un livello di dati su una pagina di prodotto
description: Implementare un livello di dati su una pagina di prodotto
exl-id: 0debf34a-48d4-4029-b790-7fd78865c334
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Implementare un livello di dati su una pagina di prodotto

Per questa esercitazione, implementa Adobe Client Data Layer per un tipico sito web di e-commerce. Se non lo hai già fatto, leggi [Come utilizzare Adobe Client Data Layer](how-to-use-the-adobe-client-data-layer.md) prima di tutto, comprendere l&#39;Adobe Client Data Layer.

Supponiamo che l&#39;utente esplori i tuoi prodotti e clicchi su un rullo di schiuma per saperne di più. L&#39;utente arriva sulla pagina dei dettagli del prodotto del rullo di schiuma.

## Creare una semplice pagina dei dettagli del prodotto

1. Copia e incolla il seguente codice in un nuovo file HTML e salvalo sul computer.

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

Dentro `<head>` è presente un tag `<script>` tag . In questo punto inserisci il codice JavaScript. Anche se non è necessario posizionare il `<script>` all’interno del tag `<head>` contenitore , è consigliato. Questo garantisce che i dati siano disponibili al livello di dati il prima possibile per supportare una serie di casi d’uso.

## Aggiungi il livello dati Adobe

1. Dentro `<script>` aggiungi questo codice che crea il tag `adobeDataLayer` e quindi invia informazioni appropriate sull&#39;evento e sui dati nell&#39;array. I dati sono conformi allo schema XDM [creato in precedenza](../configure-the-server/create-a-schema.md).

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

In questo esempio, hai effettuato due passaggi al livello dati, ciascuno contenente un `event` chiave. Includere un `event` key non comunica solo l’evento che si è verificato sulla pagina, ma rende anche più semplice per l’addetto al marketing creare regole appropriate all’interno dei tag.

Il primo push al livello dati notifica agli ascoltatori (regole di tag) che l’utente ha visualizzato la pagina. Aggiunge inoltre il nome della pagina e la sezione del sito al livello dati.

Il secondo push al livello dati notifica agli ascoltatori (regole dei tag) che l&#39;utente ha visualizzato un prodotto. Aggiunge anche informazioni sul prodotto al livello dati.

## Aggiungi il codice per il tracciamento aggiunto del carrello

Per questa esercitazione, tieni traccia di quando l’utente fa clic sul pulsante [!UICONTROL Aggiungi al carrello] pulsante .

1. Copia e incolla questo codice dopo il codice del livello dati. La funzione viene chiamata quando l&#39;utente fa clic sul pulsante [!UICONTROL Aggiungi al carrello] pulsante .

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

Questa funzione controlla inizialmente se un carrello esiste già per un utente.  Se il carrello non esiste, premi un `cartOpened` al livello dati. Successivamente, premi un `productAddedToCart` nel livello dati. Le informazioni sul prodotto esistono già nel livello dati, quindi non è necessario aggiungerle di nuovo.

## Aggiungi attributo da aggiungere al pulsante del carrello

1. Aggiungi un `onclick` attributo [!UICONTROL Aggiungi al carrello] pulsante che chiama il nuovo `onAddToCartClick` funzione .

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

## Aggiungi il codice per il tracciamento del download delle app

Un&#39;ultima cosa da tenere traccia è quando l&#39;utente fa clic sul pulsante _[!UICONTROL Scaricare l’app]_ link.

1. A questo scopo, copia e incolla questo codice sotto il carrello aggiungi il codice. Questa funzione viene chiamata quando l&#39;utente fa clic sul pulsante _[!UICONTROL Scaricare l’app]_ link.

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

## Aggiungi attributo al collegamento per scaricare l’app

1. Aggiungi un `onclick` attributo [!UICONTROL Scaricare l’app] collegamento che chiama il nuovo `onDownloadAppClick` funzione .

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

[Avanti: ](create-a-tags-property-and-install-extensions.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
