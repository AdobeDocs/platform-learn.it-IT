---
title: 'Attività di rendering di Target: migrazione da Adobe Target a Adobe Journey Optimizer, estensione Decisioning per dispositivi mobili'
description: Scopri come migrare un’implementazione di Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK. Gli argomenti includono panoramica della libreria, differenze di implementazione e altri callout degni di nota.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Attività di rendering di Target

Alcune implementazioni di Target possono utilizzare mbox regionali (ora noti come &quot;ambiti&quot;) per distribuire contenuti da attività che utilizzano il Compositore esperienza basato su moduli. Se l’implementazione di at.js Target utilizza mbox, devi effettuare le seguenti operazioni:

* Aggiorna eventuali riferimenti dall&#39;implementazione at.js che utilizzano `getOffer()` o `getOffers()` ai metodi Platform Web SDK equivalenti.
* Aggiungi il codice per attivare un evento `propositionDisplay` in modo che venga conteggiata un&#39;impression.

## Richiedere e applicare contenuti su richiesta

+++ Esempio di Android

>[!BEGINTABS]

>[!TAB SDK di destinazione]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ Esempio di iOS

>[!BEGINTABS]

>[!TAB SDK di destinazione]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++


Le attività create utilizzando il compositore basato su moduli di Target e distribuite a mbox regionali non possono essere sottoposte a rendering automatico da Platform Web SDK. Analogamente a at.js, le offerte distribuite a posizioni di Target specifiche devono essere sottoposte a rendering su richiesta.



Successivamente, scopri come [passare i parametri di Target utilizzando Platform Web SDK](send-parameters.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
