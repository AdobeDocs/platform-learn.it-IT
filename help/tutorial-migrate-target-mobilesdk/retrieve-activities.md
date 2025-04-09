---
title: 'Recuperare le attività di Target: migrazione dell’implementazione di Adobe Target nell’app mobile a Adobe Journey Optimizer - Estensione Decisioning'
description: Scopri come recuperare le attività di Adobe Target durante la migrazione da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning per dispositivi mobili.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 2ebad2014d4c29a50af82328735258958893b42c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Recuperare le attività Target

Le implementazioni mobili di Target utilizzano mbox regionali (ora noti come &quot;ambiti&quot;) per distribuire contenuti da attività che utilizzano il Compositore esperienza basato su moduli di Target. È necessario aggiornare l’app mobile per includere gli ambiti nelle chiamate di rete.

Il contenuto restituito da Target, noto anche come &quot;offerte&quot;, in genere è costituito da testo o json che devi utilizzare nell’applicazione per riprodurre l’esperienza finale del cliente. Le offerte di Target vengono spesso utilizzate per:

* Abilitare i flag di funzione nell’applicazione
* Distribuisci testo o immagini alternativi

Se hai attività che devono essere eseguite sia nelle versioni di estensione Target che nelle versioni di estensione Decisioning dell’applicazione, assicurati di eseguire il test completo. Se devi utilizzare offerte diverse per versioni diverse dell’app, puoi utilizzare le opzioni di targeting nell’interfaccia per distribuire offerte diverse alle diverse versioni.

Assicurati sempre di includere la gestione degli errori per visualizzare le esperienze appropriate in condizioni di errore.


## Richiedere e applicare contenuti su richiesta

>[!IMPORTANT]
>
>Dopo aver applicato il contenuto all&#39;app, è fondamentale attivare l&#39;API `displayed` per comunicare a Target che il visitatore ha visto il contenuto alternativo o predefinito specificato nell&#39;attività. Per ulteriori dettagli, consulta la pagina [Traccia eventi di conversione Target](track-events.md).


+++ Esempio di Android

>[!BEGINTABS]

>[!TAB Ottimizza SDK]

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

>[!TAB Ottimizza SDK]

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



Successivamente, scopri come [passare i parametri di Target utilizzando l&#39;estensione Decisioning](send-parameters.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
