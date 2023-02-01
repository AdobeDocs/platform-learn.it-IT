---
title: Soluzione per il recupero preventivo | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come implementare una soluzione per trasmettere parametri con preacquisizione
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Soluzione per il recupero preventivo

Tutti i clienti Target che non erano in produzione con Experience Platform Web SDK prima del 1° ottobre 2022 effettuano una richiesta a Target da Experience Platform Edge Network utilizzando la modalità di preacquisizione. La preacquisizione consente al browser di precaricare e memorizzare nella cache le offerte Target in modo che siano pronte per essere applicate quando il visitatore raggiunge lo stato corretto della pagina. Ciò è vantaggioso nelle applicazioni a pagina singola (SPA) poiché l’esperienza utente desiderata può essere resa il più rapidamente possibile, senza richieste di rete aggiuntive. Tuttavia, vi sono importanti implicazioni sia per le implementazioni SPA che per quelle non SPA.

Invece di contare un visitatore in un&#39;attività quando il contenuto dell&#39;offerta viene consegnato nella richiesta di rete, i visitatori vengono ora conteggiati nelle attività quando un `propositionDisplay` La richiesta sendEvent viene effettuata dall&#39;SDK Web. Queste richieste vengono effettuate automaticamente dalle attività del Compositore esperienza visivo quando renderdecisions è impostato su true e quando l’esperienza viene riprodotta correttamente sulla pagina. Con ambiti personalizzati e quando renderdecisions è impostato su false, le richieste propositionDisplay devono essere iniziate intenzionalmente dall&#39;implementatore. Inoltre, _tutti i parametri utilizzati per scopi diversi dalla qualificazione immediata delle attività devono essere inviati attraverso un `propositionDisplay`  event_.

## Perché è necessaria la soluzione alternativa?

In molte implementazioni di Target, a volte vengono effettuate importanti richieste di rete senza aspettarsi che venga distribuita un&#39;attività. Ad esempio, possono essere richieste a:

* Conversioni ordine di record
* Impostare i parametri di profilo
* Script di profilo di attivazione
* Invia parametri di entità per compilare il catalogo Recommendations

Sfortunatamente, in modalità di preacquisizione, questi non si comportano come previsto. In modalità di preacquisizione, questi dati non vengono acquisiti a meno che non facciano parte di un `propositionDisplay`.

## Qual è la soluzione alternativa?

La soluzione alternativa è costituita da tre parti:

1. Definire un ambito personalizzato come parte del `sendEvent`
1. Utilizza l’ambito personalizzato in un’attività basata su moduli (l’attività può fornire contenuto predefinito)
1. Utilizzare un gestore di risposta per creare un altro `sendEvent` per propositionDisplay e includere i parametri necessari per acquisire l&#39;ordine, impostare i parametri del profilo, attivare lo script del profilo, inviare i parametri dell&#39;entità, ecc.

Ad esempio, di seguito è riportato un esempio di come è possibile utilizzare la soluzione per inviare un parametro di profilo:


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

Quando il profilo è impostato come parte di propositionDisplay, viene salvato nel profilo del visitatore ed è disponibile nelle richieste successive. Lo stesso approccio può essere utilizzato per riportare i dettagli di conversione dell’ordine e i parametri di entità.

Nei tag, utilizza il tipo di evento Send Event Complete per attivare un evento contenente l’oggetto sendEvent aggiuntivo.

## Come posso sapere se la mia implementazione utilizza la modalità di preacquisizione?

Devi aprire un ticket dell’Assistenza clienti per sapere se il tuo account utilizza la modalità di preacquisizione.


>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).