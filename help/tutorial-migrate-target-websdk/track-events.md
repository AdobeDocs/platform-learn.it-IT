---
title: Tracciare gli eventi | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come tenere traccia degli eventi di conversione di Adobe Target utilizzando Experience Platform Web SDK.
source-git-commit: 43740912bc5a941aa21c5f38ed2c1aac74abffbc
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---


# Tracciare gli eventi di conversione di Target tramite SDK per web di Platform

Gli eventi di conversione per Target possono essere tracciati con l’SDK per web di Platform in modo simile a at.js. Gli eventi di conversione in genere rientrano nelle seguenti categorie:

* Eventi tracciati automaticamente che non richiedono alcuna configurazione
* Acquistare eventi di conversione che devono essere regolati in base alle best practice per l’implementazione dell’SDK per web di Platform
* Eventi di conversione non di acquisto che richiedono aggiornamenti del codice

>[!WARNING]
>
> Le implementazioni di Platform Web SDK iniziate dopo il 1° ottobre 2022 potrebbero dover utilizzare il [soluzione alternativa alla preacquisizione](prefetch-workaround.md) per tenere traccia di alcuni degli eventi descritti in questa pagina.

## Confronto del tracciamento degli obiettivi

Nella tabella seguente viene confrontato il modo in cui at.js e Platform Web SDK tengono traccia degli eventi di conversione

| Obiettivo dell’attività | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Conversione > Visualizzazione di una pagina | Tracciato automaticamente. In base al valore di `context.address.url` nel payload della richiesta at.js. | Tracciato automaticamente. In base al valore di `xdm.web.webPageDetails.URL` in `sendEvent` carico utile |
| Conversione > Visualizzazione di una mbox | Tracciato con la richiesta di una posizione mbox di visualizzazione o una notifica tramite `trackEvent()` o `sendNotifications()` con `type` valore `display`. | Tracciato con un SDK web per Platform `sendEvent` chiama con `eventType` di `decisioning.propositionDisplay`. |
| Conversione > Clic su un elemento | Monitorato automaticamente per attività basate su VEC. Viene visualizzato come una chiamata di rete at.js con un `notifications` oggetto nel payload della richiesta in e un `type` valore `click`. | Monitorato automaticamente per attività basate su VEC. Viene visualizzato come SDK per web di Platform `sendEvent` chiama con `eventType` di `decisioning.propositionInteract`. |
| Coinvolgimento > Visualizzazioni pagina | Tracciato automaticamente | Tracciato automaticamente |
| Coinvolgimento > Tempo sul sito | Tracciato automaticamente | Tracciato automaticamente |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Eventi tracciati automaticamente

I seguenti obiettivi di conversione non richiedono adeguamenti specifici all’implementazione:

* Conversione > Visualizzazione di una pagina
* Conversione > Clic su un elemento
* Coinvolgimento > Visualizzazioni pagina
* Coinvolgimento > Tempo sul sito

>[!NOTE]
>
>Platform Web SDK consente un maggiore controllo sui valori passati nel payload della richiesta. Per garantire il corretto funzionamento delle funzioni di Target come gli URL di controllo qualità e gli obiettivi di conversione &quot;Visualizzazione di una pagina&quot;, controlla che la `xdm.web.webPageDetails.URL` contiene l&#39;URL della pagina completa con il carattere maiuscolo/minuscolo corretto.

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

## Eventi con tracciamento personalizzato

Le implementazioni di Target generalmente utilizzano eventi di conversione personalizzati per tenere traccia dei clic per le attività basate su moduli, per indicare una conversione in un flusso o per trasmettere parametri senza richiedere nuovi contenuti.

La tabella seguente illustra l’approccio at.js e l’equivalente SDK per web di Platform per alcuni casi d’uso comuni di tracciamento delle conversioni.

| Caso d’uso | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Tracciare un evento di conversione clic per una posizione mbox (ambito) | Esegui `trackEvent()` o `sendNotifications()` con `type` valore `click` per una posizione mbox specifica | Esegui un `sendEvent` con un tipo di evento `decisioning.propositionInteract` |
| Monitora un evento di conversione personalizzato che può includere anche dati aggiuntivi, ad esempio parametri di profilo Target | Esegui `trackEvent()` o `sendNotifications()` con `type` valore `display` per una posizione mbox specifica | Esegui un `sendEvent` con un tipo di evento `decisioning.propositionDisplay` |

>[!NOTE]
>
>Nonostante `decisioning.propositionDisplay` viene utilizzato più comunemente per incrementare le impression per ambiti specifici; deve essere utilizzato anche come sostituzione diretta per at.js `trackEvent()` di solito. La `trackEvent()` viene impostato automaticamente su un tipo di `display` se non specificato. Controlla l’implementazione per assicurarti di utilizzare il tipo di evento corretto per eventuali conversioni personalizzate definite.

Per ulteriori informazioni su come utilizzare, consulta la documentazione dedicata di at.js . [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) e [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) per il tracciamento degli eventi Target.

esempio at.js utilizzando `trackEvent()` per tracciare un clic su una posizione mbox:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Con un’implementazione Platform Web SDK, puoi tenere traccia di eventi e azioni degli utenti chiamando il `sendEvent` comando, compilazione `_experience.decisioning.propositions` gruppo di campi XDM e impostazione `eventType` a uno dei due valori seguenti:

* `decisioning.propositionDisplay`: Segnala il rendering dell&#39;attività Target.
* `decisioning.propositionInteract`: Segnala un’interazione dell’utente con l’attività, ad esempio un clic del mouse.

La `_experience.decisioning.propositions` Il gruppo di campi XDM è una matrice di oggetti. Le proprietà di ciascun oggetto sono derivate dal `result.propositions` che viene restituito nel `sendEvent` comando: `{ id, scope, scopeDetails }`

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

Quindi, scopri come [abilitare la condivisione ID tra più domini](cross-domain.md) per profili visitatore coerenti.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).