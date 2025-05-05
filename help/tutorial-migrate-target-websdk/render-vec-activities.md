---
title: Rendering delle attività del Compositore esperienza visivo - Migrazione di Target da at.js 2.x a Web SDK
description: Scopri come recuperare e applicare le attività del compositore esperienza visivo con un’implementazione Web SDK di Adobe Target.
exl-id: bbbbfada-e236-44de-a7bf-5c63ff840db4
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# Eseguire il rendering delle attività del Compositore esperienza visivo di Adobe Target

Le attività di Target vengono configurate utilizzando il Compositore esperienza visivo o il Compositore basato su moduli. Platform Web SDK può recuperare e applicare alla pagina le attività basate sul Compositore esperienza visivo proprio come at.js. Per questa parte della migrazione:

* Installare l’estensione del browser Helper per editing video
* Eseguire una chiamata `sendEvent` con Platform Web SDK per richiedere attività.
* Aggiorna eventuali riferimenti dall&#39;implementazione at.js che utilizzano `getOffers()` per eseguire una richiesta Target `pageLoad`.

## Estensione del browser Helper per editing video

L’estensione del browser Adobe Experience Cloud Visual Editing Helper per Google Chrome consente di caricare i siti web in modo affidabile all’interno del Compositore esperienza visivo di Adobe Target per creare e verificare rapidamente le esperienze web.

L’estensione del browser Helper per editing video funziona con siti web che utilizzano at.js o Platform Web SDK.

### Ottenere e installare Helper per editing video

1. Passare all&#39;estensione del browser [Adobe Experience Cloud Visual Editing Helper nel Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Fai clic su Aggiungi a **Chrome** > **Aggiungi estensione**.
1. Apri il Compositore esperienza visivo in Target.
1. Per utilizzare l&#39;estensione, fai clic sull&#39;icona dell&#39;estensione del browser Helper per editing video ![icona Estensione editing video](assets/VEC-Helper.png){zoomable="yes"} nella barra degli strumenti del browser Chrome quando sei nel Compositore esperienza visivo o in Modalità Controllo qualità.

L’Helper per editing video viene attivato automaticamente quando un sito web viene aperto nel Compositore esperienza visivo di Target per l’authoring potente. L&#39;estensione non dispone di impostazioni condizionali. L’estensione gestisce automaticamente tutte le impostazioni, incluse le impostazioni dei cookie SameSite.

Consulta la documentazione dedicata per ulteriori informazioni sull&#39;estensione [Helper per editing video](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html?lang=it) e sulla [risoluzione dei problemi relativi al Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html?lang=it).

>[!IMPORTANT]
>
>La nuova estensione [Helper per editing video](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca) sostituisce la precedente [estensione VEC Helper di Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=it). Se è installata l’estensione VEC Helper precedente, rimuoverla o disattivarla prima di utilizzare l’estensione Helper per editing video.

## Richiedi e applica automaticamente il contenuto

Dopo che Platform Web SDK è stato configurato nella pagina, puoi richiedere il contenuto da Target. A differenza di at.js, che può essere configurato per richiedere automaticamente il contenuto quando la libreria viene caricata, Platform Web SDK richiede di eseguire esplicitamente un comando.

Se l&#39;implementazione at.js ha l&#39;impostazione `pageLoadEnabled` impostata su `true` che abilita il rendering automatico delle attività basate sul Compositore esperienza visivo, è necessario eseguire il seguente comando `sendEvent` con Platform Web SDK:

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB Tag]

Nei tag, utilizza il tipo di azione [!UICONTROL Invia evento] con l&#39;opzione [!UICONTROL Esegui rendering delle decisioni di personalizzazione visiva] selezionata:

![Invia un evento con le decisioni di personalizzazione visiva di rendering selezionate nei tag](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## Richiedere e applicare contenuti su richiesta

Alcune implementazioni di Target richiedono un’elaborazione personalizzata delle offerte VEC prima di applicarle alla pagina. Oppure, richiedono più posizioni in una singola chiamata. In un&#39;implementazione at.js, è possibile impostare `pageLoadEnabled` su `false` e utilizzare la funzione `getOffers()` per eseguire una richiesta `pageLoad`.

+++ Esempio di at.js che utilizza `getOffers()` e `applyOffers()` per eseguire manualmente il rendering delle attività basate su Compositore esperienza visivo

```JavaScript
adobe.target.getOffers({
  request: {
    execute: {
      pageLoad: {}
    }
  }
}).
then(response => adobe.target.applyOffers({ response: response }));
```

+++

Platform Web SDK non dispone di un evento `pageLoad` specifico. Tutte le richieste di contenuto Target sono controllate con l&#39;opzione `decisionScopes` con il comando `sendEvent`. L&#39;ambito `__view__` soddisfa lo scopo della richiesta `pageLoad`.

+++ Un approccio equivalente di Platform Web SDK `sendEvent`:

1. Esegui un comando `sendEvent` che include l&#39;ambito di decisione `__view__`
1. Applica il contenuto restituito alla pagina con il comando `applyPropositions`
1. Esegui un comando `sendEvent` con il tipo di evento `decisioning.propositionDisplay` e i dettagli della proposta per incrementare un&#39;impression

```Javascript
alloy("sendEvent", {
  // Request the special "__view__" scope for target-global-mbox / pageLoad
  decisionScopes: ["__view__"]
}).then(function(result) {
  // Check if content (propositions) were returned
  if (result.propositions) {
    var retrievedPropositions = result.propositions;
    // Apply propositions to the page
    return alloy("applyPropositions", {
      propositions: retrievedPropositions
    }).then(function(applyPropositionsResult) {
      var renderedPropositions = applyPropositionsResult.propositions;
      // Send a display notification with the sendEvent command
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
  }
});
```

+++

>[!NOTE]
>
>È possibile [eseguire manualmente il rendering delle modifiche apportate](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=it#manually-rendering-content) nel Compositore esperienza visivo. Il rendering manuale delle modifiche basate sul Compositore esperienza visivo non è comune. Verifica se l&#39;implementazione di at.js utilizza la funzione `getOffers()` per eseguire manualmente una richiesta di Target `pageLoad` senza utilizzare `applyOffers()` per applicare il contenuto alla pagina.

Platform Web SDK offre agli sviluppatori una grande flessibilità nella richiesta e nel rendering dei contenuti. Per ulteriori opzioni e dettagli, consulta la [documentazione dedicata sul rendering dei contenuti personalizzati](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=it).

## Esempio di implementazione

L’implementazione dell’SDK web di Platform è stata completata.

>[!BEGINTABS]

>[!TAB JavaScript]

Esempio di JavaScript con rendering automatico del contenuto di Target:

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
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    
    // Send an event to the Adobe edge network and render Target content automatically 
    alloy("sendEvent", {
      "renderDecisions": true
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


>[!TAB Tag]

Pagina di esempio dei tag con rendering automatico del contenuto di Target:


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

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
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

In tag, aggiungi l’estensione Adobe Experience Platform Web SDK:

![Aggiungere l&#39;estensione Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable="yes"}

Aggiungi le configurazioni desiderate:
![configurazione delle opzioni di migrazione dell&#39;estensione tag Web SDK](assets/tags-config-migration.png){zoomable="yes"}

Crea una regola con un&#39;azione [!UICONTROL Invia evento] e [!UICONTROL Esegui rendering delle decisioni di personalizzazione visiva] selezionate:
![Invia un evento con le personalizzazioni di rendering selezionate nei tag](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

Quindi, scopri come richiedere ed eseguire il rendering di [attività Target basate su moduli](render-form-based-activities.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
