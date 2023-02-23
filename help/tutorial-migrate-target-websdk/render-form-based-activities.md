---
title: Migrare Target da at.js 2.x all’SDK per web
description: Scopri come migrare un’implementazione Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK. Gli argomenti includono la panoramica della libreria, le differenze di implementazione e altri callout importanti.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# Eseguire il rendering delle attività Target che utilizzano il compositore basato su moduli

Alcune implementazioni di Target possono utilizzare mbox regionali (ora note come &quot;ambiti&quot;) per distribuire contenuti da attività che utilizzano il Compositore esperienza basato su moduli. Se l’implementazione di at.js Target utilizza mbox, è necessario effettuare le seguenti operazioni:

* Aggiornare i riferimenti dall’implementazione at.js che utilizzano `getOffer()` o `getOffers()` ai metodi SDK per web di Platform equivalenti.
* Aggiungi il codice per attivare un `propositionDisplay` in modo da conteggiare un&#39;impression.

## Richiedi e applica contenuto su richiesta

Le attività create utilizzando il compositore basato su moduli di Target e distribuite a mbox regionali non possono essere rese automaticamente dall’SDK per web di Platform. Analogamente a at.js, le offerte consegnate a posizioni Target specifiche devono essere sottoposte a rendering su richiesta.


Esempio di +++at.js utilizzando `getOffer()` e `applyOffer()`:

1. Esegui `getOffer()` per richiedere un&#39;offerta per una posizione
1. Esegui `applyOffer()` per eseguire il rendering dell’offerta su un selettore specifico
1. Un’impression di attività viene incrementata automaticamente al momento della `getOffer()` richiesta

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

+++

+++SDK per web di Platform che utilizza `applyPropositions` comando:

1. Esegui `sendEvent` comando per richiedere offerte (proposte) per una o più posizioni (ambiti)
1. Esegui `applyPropositions` comando con oggetto metadati che fornisce istruzioni su come applicare contenuto alla pagina per ogni ambito
1. Esegui `sendEvent` comando con eventType di `decisioning.propositionDisplay` tracciare un’impression

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": renderedPropositions
          }
        }
      }
    });
  });
});
```

+++

L’SDK per web di Platform offre un maggiore controllo per l’applicazione di attività basate su moduli alla pagina tramite l’ `applyPropositions` con un comando `actionType` specificato:

| `actionType` | Descrizione | at.js `applyOffer()` | SDK Web per Platform `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | Cancella il contenuto del contenitore, quindi aggiungi l’offerta al contenitore | Sì (utilizzato sempre) | Sì |
| `replaceHtml` | Rimuovi il contenitore e sostituiscilo con l’offerta | No | Sì |
| `appendHtml` | Aggiunge l’offerta dopo il selettore specificato | No | Sì |

Fai riferimento a [documentazione dedicata](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) informazioni sul rendering del contenuto tramite Platform Web SDK per ulteriori opzioni ed esempi di rendering.

## Esempio di implementazione

La pagina di esempio seguente si basa sull’implementazione descritta nella sezione precedente, aggiungendo solo ambiti aggiuntivi al `sendEvent` comando.

++Esempio di SDK per web Platform con più ambiti

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous deployment-->
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
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
          "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
              "decisioning": {
                "propositions": renderedPropositions
              }
            }
          }
        });
      });
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

Quindi, scopri come [trasmettere parametri Target tramite l’SDK per web di Platform](send-parameters.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).