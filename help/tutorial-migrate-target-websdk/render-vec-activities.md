---
title: Rendering delle attività del Compositore esperienza visivo | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come recuperare e applicare le attività del compositore esperienza visivo con un’implementazione SDK per web di Adobe Target.
source-git-commit: 4b695b4578f0e725fc3fe1e455aa4886b9cc0669
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 5%

---

# Rendering delle attività del Compositore esperienza visivo di Adobe Target

Le attività di Target vengono configurate utilizzando il Compositore esperienza visivo o il Compositore esperienza basato su moduli. L’SDK per web di Platform può recuperare e applicare le attività basate su VEC alla pagina come at.js. Per questa parte della migrazione:

* Installare l’estensione del browser Visual Editing Helper
* Esegui un `sendEvent` chiama con Platform Web SDK per richiedere attività.
* Aggiornare i riferimenti dall’implementazione at.js che utilizzano `getOffers()` per eseguire un target `pageLoad` richiesta.

## Estensione di Visual Editing Helper per il browser

L’estensione Adobe Experience Cloud Visual Editing Helper per il browser Google Chrome consente di caricare i siti web in modo affidabile nel Compositore esperienza visivo di Adobe Target (VEC) per creare e verificare rapidamente le esperienze web.

L’estensione per browser di Visual Editing Helper funziona con siti web che utilizzano at.js o Platform Web SDK.

>[!IMPORTANT]
>
>La nuova estensione Visual Editing Helper sostituisce la precedente [Estensione del browser VEC Helper Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). Se è installata la vecchia estensione VEC Helper, devi rimuoverla o disattivarla prima di utilizzare l&#39;estensione Visual Editing Helper.

### Ottenere e installare Visual Editing Helper

1. Passa a [Estensione Adobe Experience Cloud Visual Editing Helper per browser in Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Fai clic su Aggiungi a **Chrome** > **Aggiungi estensione**.
1. Apri il Compositore esperienza visivo in Target.
1. Per utilizzare l&#39;estensione, fai clic sull&#39;icona dell&#39;estensione del browser Visual Editing Helper ![Icona dell’estensione di modifica visiva](assets/VEC-Helper.png){zoomable=&quot;yes&quot;} nella barra degli strumenti del browser Chrome durante il Compositore esperienza visivo o la modalità di controllo qualità.

L’estensione Helper per editing video viene attivata automaticamente quando un sito web viene aperto nel Compositore esperienza visivo di Target per l’authoring potente. L’estensione non dispone di impostazioni condizionali. L’estensione gestisce automaticamente tutte le impostazioni, incluse le impostazioni dei cookie SameSite.

Fai riferimento alla documentazione dedicata per ulteriori informazioni sui [Estensione Visual Editing Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) e [risoluzione dei problemi relativi al Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

## Richiedi e applica automaticamente il contenuto

Una volta configurato l’SDK per web di Platform nella pagina, puoi richiedere il contenuto da Target. A differenza di at.js che può essere configurato per richiedere automaticamente il contenuto al caricamento della libreria, l’SDK per web di Platform richiede l’esecuzione esplicita di un comando.

Se l’implementazione at.js dispone di `pageLoadEnabled` impostazione impostata su `true` che abilita il rendering automatico delle attività basate su VEC, esegui quanto segue `sendEvent` con Platform Web SDK:

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB Tag]

Nei tag, utilizza [!UICONTROL Invia evento] tipo di azione con [!UICONTROL Decisioni relative alla personalizzazione visiva del rendering] opzione selezionata:

![Invia un evento con le decisioni di rendering della personalizzazione visiva selezionate nei tag](assets/vec-sendEvent-renderTrue.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## Richiedi e applica contenuto su richiesta

Alcune implementazioni di Target richiedono un’elaborazione personalizzata delle offerte del Compositore esperienza visivo prima di applicarle alla pagina. Oppure richiedono più posizioni in una singola chiamata. In un’implementazione at.js, questo può essere fatto impostando `pageLoadEnabled` a `false` e utilizzando `getOffers()` per eseguire una funzione `pageLoad` richiesta.

+++ esempio at.js utilizzando `getOffers()` e `applyOffers()` per eseguire manualmente il rendering delle attività basate su VEC

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

L’SDK per web di Platform non dispone di un `pageLoad` evento. Tutte le richieste di contenuto Target sono controllate con `decisionScopes` con l&#39;opzione `sendEvent` comando. La `__view__` l&#39;ambito di applicazione persegue lo scopo `pageLoad` richiesta.

+++ Un SDK web per Platform equivalente `sendEvent` approccio:

1. Esegui un `sendEvent` che include `__view__` ambito decisionale
1. Applica il contenuto restituito alla pagina con il `applyPropositions` command
1. Esegui un `sendEvent` con il comando `decisioning.propositionDisplay` tipo di evento e dettagli della proposta per incrementare un’impression

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
>È possibile [rendering manuale delle modifiche](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) nel Compositore esperienza visivo. Il rendering manuale delle modifiche basate su VEC non è comune. Controlla se la tua implementazione at.js utilizza il `getOffers()` funzione per eseguire manualmente un target `pageLoad` richiesta senza utilizzare `applyOffers()` per applicare il contenuto alla pagina.

L’SDK per web di Platform offre agli sviluppatori una grande flessibilità nella richiesta e nel rendering dei contenuti. Fai riferimento a [documentazione dedicata sul rendering di contenuti personalizzati](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) per ulteriori opzioni e dettagli.

## Esempio di implementazione

L’implementazione dell’SDK web per Platform è ora completa.

>[!BEGINTABS]

>[!TAB JavaScript]

Esempio JavaScript con rendering automatico del contenuto Target:

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

Nei tag, aggiungi l’estensione Adobe Experience Platform Web SDK:

![Aggiungere l’estensione Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable=&quot;yes&quot;}

Aggiungi le configurazioni desiderate:
![configurazione delle opzioni di migrazione dell’estensione del tag SDK per web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}

Creare una regola con un [!UICONTROL Invia evento] e [!UICONTROL Decisioni relative alla personalizzazione visiva del rendering] selezionato:
![Invia un evento con le personalizzazioni di rendering selezionate nei tag](assets/vec-sendEvent-renderTrue.png){zoomable=&quot;yes&quot;}

>[!ENDTABS]

Quindi, scopri come richiedere e [eseguire il rendering di attività Target basate su moduli](render-form-based-activities.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
