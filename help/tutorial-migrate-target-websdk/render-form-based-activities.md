---
title: Migrare Target da at.js 2.x a Web SDK
description: Scopri come migrare un’implementazione di Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK. Gli argomenti includono panoramica della libreria, differenze di implementazione e altri callout degni di nota.
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# Attività di rendering di Target che utilizzano il compositore basato su moduli

Alcune implementazioni di Target possono utilizzare mbox regionali (ora noti come &quot;ambiti&quot;) per distribuire contenuti da attività che utilizzano il Compositore esperienza basato su moduli. Se l’implementazione di at.js Target utilizza mbox, devi effettuare le seguenti operazioni:

* Aggiorna eventuali riferimenti dall&#39;implementazione at.js che utilizzano `getOffer()` o `getOffers()` ai metodi Platform Web SDK equivalenti.
* Aggiungi il codice per attivare un evento `propositionDisplay` in modo che venga conteggiata un&#39;impression.

## Richiedere e applicare contenuti su richiesta

Le attività create utilizzando il compositore basato su moduli di Target e distribuite a mbox regionali non possono essere sottoposte a rendering automatico da Platform Web SDK. Analogamente a at.js, le offerte distribuite a posizioni di Target specifiche devono essere sottoposte a rendering su richiesta.


+++Esempio di at.js utilizzando `getOffer()` e `applyOffer()`:

1. Esegui `getOffer()` per richiedere un&#39;offerta per una posizione
1. Esegui `applyOffer()` per eseguire il rendering dell&#39;offerta su un selettore specificato
1. Un&#39;impression dell&#39;attività viene incrementata automaticamente al momento della richiesta `getOffer()`

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

+++Equivalente di Platform Web SDK utilizzando il comando `applyPropositions`:

1. Esegui il comando `sendEvent` per richiedere offerte (proposte) per una o più posizioni (ambiti)
1. Esegui il comando `applyPropositions` con l&#39;oggetto metadati che fornisce istruzioni su come applicare il contenuto alla pagina per ogni ambito
1. Esegui il comando `sendEvent` con eventType `decisioning.propositionDisplay` per tenere traccia di un&#39;impression

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

Platform Web SDK offre un controllo maggiore per l&#39;applicazione di attività basate su moduli alla pagina utilizzando il comando `applyPropositions` con `actionType` specificato:

| `actionType` | Descrizione | at.js `applyOffer()` | Platform Web SDK `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | Cancella il contenuto del contenitore, quindi aggiungi l’offerta al contenitore | Sì (sempre utilizzato) | Sì |
| `replaceHtml` | Rimuovere il contenitore e sostituirlo con l’offerta | No | Sì |
| `appendHtml` | Aggiunge l&#39;offerta dopo il selettore specificato | No | Sì |

Per ulteriori opzioni ed esempi di rendering, consulta la [documentazione dedicata](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) sul rendering del contenuto tramite Platform Web SDK.

## Esempio di implementazione

La pagina di esempio seguente si basa sull&#39;implementazione descritta nella sezione precedente, ma aggiunge ambiti aggiuntivi al comando `sendEvent`.

Esempio +++Platform Web SDK con più ambiti

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

Successivamente, scopri come [passare i parametri di Target utilizzando Platform Web SDK](send-parameters.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
