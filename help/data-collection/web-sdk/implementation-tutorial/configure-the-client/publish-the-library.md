---
title: Pubblicare la libreria
description: Pubblicare la libreria
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2fc072df-24f2-4fea-848f-0a973deca2f8
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 4%

---

# Pubblicare la libreria

Ora è il momento di distribuire la libreria di tag sul sito web.

## Creare una libreria

Innanzitutto, devi creare una libreria che includa le estensioni, le regole e gli elementi dati creati. Per creare una libreria, seleziona [!UICONTROL Flusso di pubblicazione] nel menu di sinistra.

Seleziona [!UICONTROL Aggiungi libreria].

Dovresti visualizzare la vista di creazione della libreria.

![creazione libreria tag](../../../assets/implementation-strategy/tags-library-creation.png)

Assegna un nome alla libreria, come _Demo_. Seleziona [!UICONTROL Sviluppo] nel [!UICONTROL Ambiente] a discesa. Quindi fai clic su [!UICONTROL Aggiungi tutte le risorse modificate].

Ora dovresti visualizzare tutte le tue estensioni, regole ed elementi dati elencati in [!UICONTROL Modifiche alle risorse]. Clic [!UICONTROL Salva e genera in sviluppo].

## Aggiungi il codice di incorporamento al tuo HTML

Ora devi aggiungere un tag script al HTML della pagina di prodotto che carica la libreria di tag appena creata.

Per iniziare, fai clic su [!UICONTROL Ambienti] nel menu di sinistra. Dovresti visualizzare tre ambienti diversi elencati.

![Ambienti di tag](../../../assets/implementation-strategy/tags-environments.png)

Fai clic sull’icona del pacchetto nella [!UICONTROL Sviluppo] riga ambiente. Dovresti vedere le istruzioni per installare lo script della libreria Launch nella pagina.

![Istruzioni per l’installazione dei tag](../../../assets/implementation-strategy/tags-installation-instructions.png)

Copia il tag script (per comodità, è disponibile un pulsante Copia negli Appunti). Apri il HTML della pagina di prodotto e inserisci il tag script prima del `</head>` tag. Il HTML finale dovrebbe essere il seguente:

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
    <!--Swap this script tag with your own-->
    <script src="https://assets.adobedtm.com/xxxxxxxxxxxx/xxxxxxxxxxxx/launch-xxxxxxxxxxxx-development.min.js" async></script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```

Consulta la sezione [pubblicazione della documentazione per i tag](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=it) per ulteriori informazioni sul processo di pubblicazione.

Ora testerai la tua nuova implementazione.
