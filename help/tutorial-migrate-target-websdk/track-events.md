---
title: Tracciare gli eventi - Migrazione di Target da at.js 2.x a Web SDK
description: Scopri come tenere traccia degli eventi di conversione di Adobe Target utilizzando Experience Platform Web SDK.
exl-id: 5da772bc-de05-4ea9-afbd-3ef58bc7f025
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# Tracciare gli eventi di conversione di Target tramite Platform Web SDK

È possibile tenere traccia degli eventi di conversione per Target con Platform Web SDK in modo simile a at.js. Gli eventi di conversione in genere rientrano nelle seguenti categorie:

* Tracciamento automatico degli eventi che non richiedono alcuna configurazione
* Acquistare eventi di conversione che devono essere regolati per un’implementazione della best practice Platform Web SDK
* Eventi di conversione non di acquisto che richiedono aggiornamenti del codice

## Confronto del tracciamento degli obiettivi

La tabella seguente confronta il modo in cui at.js e Platform Web SDK tengono traccia degli eventi di conversione

| Obiettivo attività | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Conversione > Visualizzazione di una pagina | Tracciato automaticamente. In base al valore di `context.address.url` nel payload della richiesta at.js. | Tracciato automaticamente. In base al valore di `xdm.web.webPageDetails.URL` nel payload `sendEvent` |
| Conversione > Visualizzazione di una mbox | Tracciato con la richiesta di un percorso mbox di visualizzazione o una notifica tramite `trackEvent()` o `sendNotifications()` con un valore `type` di `display`. | Tracciato con una chiamata Platform Web SDK `sendEvent` con `eventType` di `decisioning.propositionDisplay`. |
| Conversione > Clic su un elemento | Tracciato automaticamente per le attività basate sul Compositore esperienza visivo. Viene visualizzata come chiamata di rete at.js con un oggetto `notifications` nel payload della richiesta in e un valore `type` di `click`. | Tracciato automaticamente per le attività basate sul Compositore esperienza visivo. Viene visualizzata come chiamata Platform Web SDK `sendEvent` con `eventType` di `decisioning.propositionInteract`. |
| Coinvolgimento > Visualizzazioni pagina | Tracciato automaticamente | Tracciato automaticamente |
| Coinvolgimento > Tempo sul sito | Tracciato automaticamente | Tracciato automaticamente |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Eventi tracciati automaticamente

I seguenti obiettivi di conversione non richiedono alcun adeguamento specifico all’implementazione:

* Conversione > Visualizzazione di una pagina
* Conversione > Clic su un elemento
* Coinvolgimento > Visualizzazioni pagina
* Coinvolgimento > Tempo sul sito

>[!NOTE]
>
>Platform Web SDK consente un maggiore controllo sui valori trasmessi nel payload della richiesta. Per garantire il corretto funzionamento delle funzioni di Target, ad esempio gli URL di controllo qualità e gli obiettivi di conversione &quot;Visualizzazione di una pagina&quot;, verifica che il valore `xdm.web.webPageDetails.URL` contenga l&#39;URL della pagina intera con le maiuscole/minuscole appropriate.

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## Eventi tracciati personalizzati

Le implementazioni di Target solitamente utilizzano eventi di conversione personalizzati per tenere traccia dei clic per le attività basate su moduli, per indicare una conversione in un flusso o per trasmettere parametri senza richiedere nuovo contenuto.

La tabella seguente illustra l’approccio at.js e l’equivalente di Platform Web SDK per alcuni casi d’uso comuni di tracciamento delle conversioni.

| Caso d’uso | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Tracciare un evento di conversione dei clic per una posizione mbox (ambito) | Esegui `trackEvent()` o `sendNotifications()` con un valore `type` di `click` per un percorso mbox specifico | Esegui un comando `sendEvent` con tipo di evento `decisioning.propositionInteract` |
| Tracciare un evento di conversione personalizzato che può includere anche dati aggiuntivi, come i parametri del profilo di Target | Esegui `trackEvent()` o `sendNotifications()` con un valore `type` di `display` per un percorso mbox specifico | Esegui un comando `sendEvent` con tipo di evento `decisioning.propositionDisplay` |

>[!NOTE]
>
>Anche se `decisioning.propositionDisplay` viene utilizzato in genere per incrementare le impression per ambiti specifici, in genere deve essere utilizzato anche come sostituzione diretta per at.js `trackEvent()`. La funzione `trackEvent()` viene impostata automaticamente su un tipo di `display`, se non specificato. Controlla l’implementazione per assicurarti di utilizzare il tipo di evento corretto per tutte le conversioni personalizzate eventualmente definite.

Per ulteriori informazioni su come utilizzare [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) e [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) per il tracciamento degli eventi di Target, consulta l&#39;apposita documentazione di at.js.

Esempio di at.js che utilizza `trackEvent()` per tenere traccia di un clic su un percorso mbox:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Con un&#39;implementazione di Platform Web SDK, è possibile tenere traccia di eventi e azioni utente chiamando il comando `sendEvent`, popolando il gruppo di campi XDM `_experience.decisioning.propositions` e impostando `eventType` su uno dei due valori seguenti:

* `decisioning.propositionDisplay`: segnala il rendering dell&#39;attività Target.
* `decisioning.propositionInteract`: segnala un&#39;interazione dell&#39;utente con l&#39;attività, come un clic del mouse.

Il gruppo di campi XDM `_experience.decisioning.propositions` è un array di oggetti. Le proprietà di ciascun oggetto sono derivate da `result.propositions` restituito nel comando `sendEvent`: `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

Successivamente, scopri come [abilitare la condivisione ID tra domini](cross-domain.md) per profili visitatore coerenti.

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
