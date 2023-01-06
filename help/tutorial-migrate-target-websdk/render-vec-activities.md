---
title: Rendering delle attività del Compositore esperienza visivo | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come recuperare e applicare le attività del compositore esperienza visivo con un’implementazione SDK per web di Adobe Target.
feature: Visual Experience Composer (VEC),Implement Client-side,APIs/SDKs,at.js,AEP Web SDK, Web SDK,Implementation
source-git-commit: 7e6aa296429844552ad164ba209a504ddc908571
workflow-type: tm+mt
source-wordcount: '883'
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
1. Per utilizzare l&#39;estensione, fai clic sull&#39;icona dell&#39;estensione del browser Visual Editing Helper ![Icona dell’estensione di modifica visiva](assets/VEC-Helper.png) nella barra degli strumenti del browser Chrome in modalità VEC o QA.

L’estensione Helper per editing video viene attivata automaticamente quando un sito web viene aperto nel Compositore esperienza visivo di Target per l’authoring potente. L’estensione non dispone di impostazioni condizionali. L’estensione gestisce automaticamente tutte le impostazioni, incluse le impostazioni dei cookie SameSite.

Fai riferimento alla documentazione dedicata per ulteriori informazioni sui [Estensione Visual Editing Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) e [risoluzione dei problemi relativi al Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

## Richiedi e applica automaticamente il contenuto

Una volta configurato l’SDK per web di Platform nella pagina, puoi richiedere il contenuto da Target. A differenza di at.js che può essere configurato per richiedere automaticamente il contenuto al caricamento della libreria, l’SDK per web di Platform richiede l’esecuzione esplicita di un comando.

Se l’implementazione at.js dispone di `pageLoadEnabled` impostazione impostata su `true` che abilita il rendering automatico delle attività basate su VEC, esegui quanto segue `sendEvent` con Platform Web SDK:

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TIP]
>
> Quando si utilizza la funzione tag (precedentemente Launch) per implementare l’SDK per web, i comandi &quot;sendEvent&quot; per le attività VEC possono essere implementati in una regola utilizzando [!UICONTROL Invia evento] tipo di azione con [!UICONTROL Decisioni relative alla personalizzazione visiva del rendering] opzione selezionata.

Quando l’SDK per web di Platform esegue il rendering di un’attività sulla pagina con `renderDecisions` impostato su `true`, una chiamata di notifica aggiuntiva viene attivata automaticamente per incrementare un’impression e attribuire il visitatore all’attività. Questa chiamata utilizza un tipo di evento con il valore `decisioning.propositionDisplay`.

![Chiamata SDK per web di Platform che incrementa un’impression di Target](assets/target-impression-call.png)

## Richiedi e applica contenuto su richiesta

Alcune implementazioni at.js di Target possono avere `pageLoadEnabled` impostato su `false` e utilizza invece il `getOffers()` per eseguire una funzione `pageLoad` richiesta. Questo tipo di configurazione viene utilizzato se l’implementazione richiede un’elaborazione aggiuntiva dell’ `getOffers()` prima di applicare contenuto alla pagina o di richiedere contenuto per più posizioni in una singola chiamata.

Il codice seguente utilizza `getOffers()` e `applyOffers()` per applicare le attività basate sul Compositore esperienza visivo su richiesta anziché automaticamente al caricamento della libreria.

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

L’SDK per web di Platform non dispone di un `pageLoad` evento. Tutte le richieste di contenuto Target sono controllate con `decisionScopes` con l&#39;opzione `sendEvent` comando. La `__view__` l&#39;ambito di applicazione persegue lo scopo `pageLoad` richiesta. Un SDK web per Platform equivalente `sendEvent` l&#39;approccio è:

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

>[!NOTE]
>
>È possibile [rendering manuale delle modifiche](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) nel Compositore esperienza visivo. Il rendering manuale delle modifiche basate su VEC non è comune. Controlla se la tua implementazione at.js utilizza il `getOffers()` funzione per eseguire manualmente un target `pageLoad` richiesta senza utilizzare `applyOffers()` per applicare il contenuto alla pagina.

L’SDK per web di Platform offre agli sviluppatori una grande flessibilità nella richiesta e nel rendering dei contenuti. Fai riferimento a [documentazione dedicata sul rendering di contenuti personalizzati](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) per ulteriori opzioni e dettagli.

## Esempio di implementazione

L’implementazione dell’SDK web per Platform è ora completa. La nostra pagina di esempio di base con il rendering automatico del contenuto di Target abilitato deve essere simile alla seguente:

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

>[!TIP]
>
> Quando si utilizza la funzione tag (precedentemente Launch) per implementare l’SDK per web, il codice di incorporamento dei tag sostituisce le sezioni precedenti &quot;Codice di base SDK per web Platform&quot;, &quot;SDK per web Platform caricato in modo asincrono&quot; e &quot;Configura SDK per web Platform&quot;. Il comando &#39;sendEvent&#39; viene eseguito in una regola utilizzando [!UICONTROL Invia evento] tipo di azione con [!UICONTROL Decisioni relative alla personalizzazione visiva del rendering] opzione selezionata.

Quindi, scopri come richiedere e [eseguire il rendering di attività Target basate su moduli](render-form-based-activities.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
