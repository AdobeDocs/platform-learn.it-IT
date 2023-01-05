---
title: Convalidare le implementazioni di Target con l’SDK per web | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come convalidare le attività ed eseguire il debug di un’implementazione Adobe Target utilizzando Adobe Experience Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 0%

---

# Convalidare l’implementazione dell’SDK per web di Platform

Dopo aver migrato l’implementazione di Target da at.js a Platform Web SDK, è importante convalidare il corretto funzionamento di tutto prima di pubblicare eventuali modifiche al sito di produzione. L’Adobe raccomanda quanto segue, che viene descritto in dettaglio in questa pagina:

* Esegui una convalida tecnica per verificare che l’implementazione di base e le richieste e le risposte SDK per web di Platform risultino corrette
* Assicurati che le attività di Target siano consegnate e rese correttamente
* Verifica che il reporting funzioni correttamente
* Controlla i tipi di pubblico e gli script di profilo per assicurarti che siano compatibili con Platform Web SDK
* Garantire il corretto funzionamento delle integrazioni con applicazioni di Adobe o di terze parti

Ogni implementazione di Target varia a seconda dell’architettura del sito e delle funzioni utilizzate. Puoi utilizzare le tabelle riportate di seguito come punto di partenza e aggiungere elementi unici all’implementazione. La [Pagina di debug](debugging.md) Questa esercitazione mostra gli strumenti che è possibile utilizzare per facilitare questa convalida.

## Convalida tecnica

| Elemento di convalida | Note |
|---|---|
| Il frammento pre-hiding di at.js non è più presente nella pagina | L’SDK per web di Platform non rimuove automaticamente lo stile con ID `at-body-style`. Lasciando questo vecchio frammento sulla pagina si ottiene contenuto nascosto fino a quando non viene raggiunto il timeout del frammento. |
| La libreria at.js non è più presente nella pagina | Verifica che non sia presente alcun oggetto &quot;adobe.target&quot; nella console degli strumenti per sviluppatori del browser. L’inclusione di Platform Web SDK e at.js determina un comportamento di rendering non intenzionale. |
| I parametri previsti si trovano in XDM e negli oggetti dati del `sendEvent` richiesta |  |
| Il catalogo Recommendations viene aggiornato come previsto se si utilizzano richieste di pagina per compilare il catalogo |  |
| I parametri del profilo vengono passati correttamente a Target | Visualizzare le tracce Edge nel debugger |
| I parametri mappati a XDM nel mappatore datastream vengono passati correttamente a Target | Convalida tramite la funzione Edge Trace del debugger e/o dell’affidabilità |
| Il contenuto di Target viene restituito nel `sendEvent` risposte | Previsto quando `renderDecisions` è impostata su `true` Gli ambiti o sono richiesti e l&#39;utente si qualifica per una particolare attività di Target |
| A `decisioning.propositionDisplay` l’evento viene attivato dopo il rendering delle attività basate su VEC | Le attività sottoposte a rendering automatico e on-demand devono disporre di chiamate evento separate |
| A `decisioning.propositionDisplay` l&#39;evento viene attivato dopo il rendering delle attività basate su moduli | Applicabile solo a determinate implementazioni. Richiede codice personalizzato per eseguire questa chiamata. |
| A `decisioning.propositionDisplay` l&#39;evento viene attivato quando un&#39;offerta viene applicata a una modifica della visualizzazione SPA | Applicabile solo per le implementazioni SPA |
| A `decisioning.propositionDisplay` L&#39;evento NON si attiva quando un componente SPA viene rieseguito per una visualizzazione specifica | Applicabile solo per le implementazioni SPA |
| A `decisioning.propsitionInteract` l&#39;evento viene attivato dopo una conversione di attività | Migrazione di &quot;un elemento selezionato&quot; e conversioni personalizzate da at.js `trackEvent` o `sendNotifications` devono avere chiamate evento separate |
| I token di risposta vengono restituiti nella variabile `sendEvent` response e dispone dei valori previsti | I token di risposta devono funzionare normalmente con l’SDK per web |
| Gli ECID sono coerenti tra le pagine con SDK per web e at.js | Si applica alle migrazioni pagina per pagina. Non è previsto che le offerte di reindirizzamento funzionino in questi tipi di migrazione |


## Consegna e rendering delle attività

| Elemento di convalida | Note |
|---|---|
| Le attività basate su VEC vengono renderizzate correttamente al caricamento della pagina | È meglio convalidare sia le modifiche al codice personalizzato che le modifiche di base, come la ridisposizione degli elementi o la sostituzione del testo |
| Le attività basate sul Compositore esperienza visivo vengono riprodotte correttamente in SPA modifiche della visualizzazione | Applicabile solo per le implementazioni SPA |
| Rendering corretto delle attività basate su moduli | Applicabile solo a determinate implementazioni. Il rendering delle attività basate su moduli richiede un codice personalizzato simile a at.js. |
| Le attività che utilizzano i reindirizzamenti funzionano correttamente | I reindirizzamenti sono supportati se la pagina di origine e quella di destinazione utilizzano l’SDK per web di Platform. Non è supportato un reindirizzamento di Target da una pagina at.js a una pagina SDK per web di Platform o in modo opposto. |
| Le attività che utilizzano offerte remote funzionano correttamente | Non comune, controlla l’inventario delle offerte di Target per le offerte remote |
| La visualizzazione momentanea di altri contenuti è opportunamente mitigata | La gestione della visualizzazione momentanea di altri contenuti è facoltativa, ma assicurati che tutte le tattiche di mitigazione installate funzionino come previsto per le prestazioni ottimali della pagina e l’esperienza utente. |
| I collegamenti QA funzionano come previsto | Se non funziona, verifica che web.webPageDetails.URL corrisponda esattamente all’URL nel browser |
| Viene eseguito il rendering di tutti i tipi di offerta comunemente utilizzati come previsto |  |

## Generazione rapporti

| Elemento di convalida | Note |
|---|---|
| I visitatori sono attribuiti ad attività basate su VEC | È meglio convalidare i rapporti funziona come previsto sia per le modifiche al caricamento delle pagine che per le modifiche alla visualizzazione SPA |
| I visitatori sono attribuiti ad attività basate su moduli | A seconda dell’approccio di rendering utilizzato, l’implementazione potrebbe richiedere un codice personalizzato per eseguire un `decisioning.propositionDisplay` event |
| Gli obiettivi di conversione standard vengono acquisiti correttamente | Si applica a Target o Analytics come origine per la generazione di rapporti |
| Le conversioni e i dettagli dell&#39;ordine vengono acquisiti correttamente | Controlla il rapporto di audit |
| Le conversioni di tracciamento dei clic vengono acquisite correttamente |  |
| Gli obiettivi di conversione personalizzati vengono acquisiti correttamente | Ad esempio, gli obiettivi di conversione migrati da at.js `trackEvent` o `sendNotifications` che vengono comunemente utilizzati con l’obiettivo &quot;visualizzato una mbox&quot; |

## Tipi di pubblico e script di profilo

| Elemento di convalida | Note |
|---|---|
| I tipi di pubblico utilizzati nelle attività live sono compatibili con Platform Web SDK | I tipi di pubblico che utilizzano il componente &quot;Personalizzato&quot; (parametro mbox) devono essere aggiornati per includere gli attributi XDM |
| Tutti gli script di profilo sono compatibili con Platform Web SDK | Eventuali script di profilo che utilizzano parametri mbox devono essere aggiornati per includere gli attributi XDM |
| Le attività restituiscono i tipi di pubblico di Target | È consigliabile eseguire una convalida end-to-end sui tipi di pubblico modificati per renderli compatibili con Platform Web SDK |
| Gli script di profilo vengono valutati come previsto | Visualizzare le tracce Edge nel debugger |

## Integrazioni con le applicazioni Adobe

| Elemento di convalida | Note |
|---|---|
| Le attività restituiscono ad Experience Cloud i tipi di pubblico | Ad esempio, un segmento pubblicato da Adobe Analytics |
| Le attività restituiscono ad Experience Platform i tipi di pubblico | Si applica solo se si dispone di una licenza per un&#39;applicazione basata su Experience Platform come RTCDP |
| Le attività restituiscono ad Audience Manager i tipi di pubblico | Ad esempio, un segmento basato sulla visita a una pagina specifica |
| I dati delle attività di Target vengono visualizzati in Analysis Workspace | Si applica alle attività che utilizzano Adobe Analytics come origine per la generazione di rapporti |

## Integrazioni con applicazioni di terze parti

| Elemento di convalida | Note |
|---|---|
| I dati del token di risposta vengono passati correttamente ad applicazioni di terze parti | Gli approcci di integrazione possono variare, ma un metodo comune consiste nell’utilizzare i token di risposta di Target per passare le informazioni sull’attività e sull’esperienza ad altri strumenti di analisi come Google Analytics |
| Le informazioni provenienti da terze parti vengono trasmesse come dati XDM o di profilo | Tutte le informazioni pertinenti provenienti da terzi devono essere trasmesse `sendEvent` chiamate a Target |

Dopo aver eseguito i passaggi di convalida descritti qui sopra, puoi essere sicuro che l’implementazione dell’SDK per web di Platform sia pronta per il passaggio alla produzione.

Quindi, scopri come [risolvere i problemi relativi all’implementazione di Target tramite SDK per web di Platform](debugging.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).