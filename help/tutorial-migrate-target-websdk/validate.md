---
title: 'Convalidare le implementazioni di Target con Web SDK: migrazione di Target da at.js 2.x a Web SDK'
description: Scopri come convalidare le attività ed eseguire il debug di un’implementazione di Adobe Target utilizzando Adobe Experience Platform Web SDK.
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: 070fc02801d3403bf65ca732323338481e25b581
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# Convalidare l’implementazione di Platform Web SDK

Dopo aver migrato l’implementazione di Target da at.js a Platform Web SDK, è importante verificare che tutto funzioni correttamente prima di pubblicare eventuali modifiche al sito di produzione. Adobe consiglia quanto segue, descritto in dettaglio in questa pagina:

* Esegui una convalida tecnica per verificare che l’implementazione di base e le richieste e le risposte di Platform Web SDK siano corrette
* Assicurati che le attività Target siano consegnate e renderizzate correttamente
* Verifica che la generazione rapporti funzioni correttamente
* Rivedi tipi di pubblico e script di profilo per assicurarti che siano compatibili con Platform Web SDK
* Garantire il corretto funzionamento delle integrazioni con le applicazioni Adobe o di terze parti

Ogni implementazione di Target è diversa a seconda dell’architettura del sito e delle funzioni utilizzate. Puoi utilizzare le tabelle seguenti come punto di partenza e aggiungere qualsiasi elemento univoco alla tua implementazione. La [pagina Debug](debugging.md) di questo tutorial mostra gli strumenti che puoi utilizzare per facilitare la convalida.

## Convalida tecnica

| Elemento di convalida | Note |
|---|---|
| Il frammento pre-hiding di at.js non è più presente nella pagina | Platform Web SDK non rimuove automaticamente lo stile con ID `at-body-style`. Se si lascia questo vecchio frammento nella pagina, il contenuto risulterà nascosto fino al raggiungimento del timeout del frammento. |
| La libreria at.js non è più presente nella pagina | Verifica che non sia presente alcun oggetto &quot;adobe.target&quot; nella console degli strumenti per sviluppatori del browser in uso. L’inclusione sia di Platform Web SDK che di at.js determina un comportamento di rendering non desiderato |
| I parametri previsti sono in XDM e negli oggetti dati della richiesta `sendEvent` | |
| Il catalogo Consigli viene aggiornato come previsto se si utilizzano le richieste di pagina per compilare il catalogo | |
| I parametri del profilo sono stati passati correttamente a Target | Visualizzare le tracce di Edge nel debugger |
| I parametri mappati a XDM nel mappatore dello stream di dati vengono passati correttamente a Target | Convalida utilizzando la funzione Edge Trace di Debugger e/o Assurance |
| Il contenuto di destinazione restituisce le risposte `sendEvent` applicabili | Previsto quando l&#39;opzione `renderDecisions` è impostata su `true` o sono richiesti ambiti e l&#39;utente è idoneo per una particolare attività di Target |
| Un evento `decisioning.propositionDisplay` viene attivato dopo il rendering delle attività basate sul Compositore esperienza visivo | Le attività sottoposte a rendering automaticamente e on-demand devono avere chiamate evento separate |
| Un evento `decisioning.propositionDisplay` viene attivato dopo il rendering delle attività basate su moduli | Applicabile solo per alcune implementazioni. Richiede un codice personalizzato per eseguire questa chiamata. |
| Un evento `decisioning.propositionDisplay` viene attivato quando un&#39;offerta viene applicata a una modifica della visualizzazione di un&#39;applicazione a pagina singola | Applicabile solo per le implementazioni di applicazioni a pagina singola |
| Un evento `decisioning.propositionDisplay` NON viene attivato quando si esegue nuovamente il rendering di un componente SPA per una determinata visualizzazione | Applicabile solo per le implementazioni di applicazioni a pagina singola |
| Un evento `decisioning.propsitionInteract` viene attivato dopo una conversione di attività | La migrazione di &quot;Clic su un elemento&quot; e conversioni personalizzate da at.js `trackEvent` o `sendNotifications` deve avere chiamate evento separate |
| I token di risposta vengono restituiti nella risposta `sendEvent` e presentano i valori previsti | I token di risposta devono funzionare normalmente con Web SDK |
| Gli ECID sono coerenti tra le pagine con Web SDK e at.js | Si applica alle migrazioni pagina per pagina. Non si prevede che le offerte di reindirizzamento funzionino in questi tipi di migrazioni |


## Consegna e rendering delle attività

| Elemento di convalida | Note |
|---|---|
| Le attività basate sul Compositore esperienza visivo vengono riprodotte correttamente al caricamento della pagina | È consigliabile convalidare sia le modifiche al codice personalizzato che le modifiche di base, ad esempio la ridisposizione degli elementi o la sostituzione del testo |
| Le attività basate sul Compositore esperienza visivo vengono riprodotte correttamente in seguito alle modifiche della vista da applicazione a pagina singola | Applicabile solo per le implementazioni di applicazioni a pagina singola |
| Le attività basate su moduli vengono riprodotte correttamente | Applicabile solo per alcune implementazioni. Il rendering delle attività basate su moduli richiede un codice personalizzato simile a at.js. |
| Le attività che utilizzano i reindirizzamenti funzionano correttamente | I reindirizzamenti sono supportati se sia la pagina di origine che quella di destinazione utilizzano Platform Web SDK. Non è supportato il reindirizzamento di Target da una pagina at.js a una pagina Platform Web SDK o viceversa. |
| Le attività che utilizzano le offerte remote funzionano correttamente | Non comune, controlla l’inventario delle offerte Target per le offerte remote |
| Lo sfarfallio è mitigato in modo appropriato | La gestione dello sfarfallio è facoltativa, ma assicurati che tutte le tattiche di mitigazione implementate funzionino come previsto per prestazioni di pagina e esperienza utente ottimali |
| I collegamenti di controllo qualità funzionano come previsto | Se non funziona, verifica che web.webPageDetails.URL corrisponda esattamente all’URL nel browser |
| Tutti i tipi di offerta comunemente utilizzati vengono visualizzati come previsto |  |

## Generazione dei rapporti

| Elemento di convalida | Note |
|---|---|
| I visitatori vengono attribuiti alle attività basate sul Compositore esperienza visivo | È consigliabile verificare che il reporting funzioni come previsto sia per le modifiche al caricamento delle pagine che per le modifiche alla visualizzazione dell’applicazione a pagina singola |
| I visitatori vengono attribuiti alle attività basate su moduli | A seconda dell&#39;approccio di rendering utilizzato, l&#39;implementazione potrebbe richiedere codice personalizzato per eseguire un evento `decisioning.propositionDisplay` |
| Gli obiettivi di conversione standard vengono acquisiti correttamente | Applicabile a Target o Analytics come origine per la generazione di rapporti |
| Le conversioni degli ordini e i dettagli vengono acquisiti correttamente | Controlla il rapporto di audit |
| Le conversioni di tracciamento dei clic vengono acquisite correttamente |  |
| Gli obiettivi di conversione personalizzati vengono acquisiti correttamente | Ad esempio, gli obiettivi di conversione sono stati migrati da at.js `trackEvent` o `sendNotifications` che vengono comunemente utilizzati con l&#39;obiettivo &quot;visualizzato in una mbox&quot; |

## Tipi di pubblico e script di profilo

| Elemento di convalida | Note |
|---|---|
| I tipi di pubblico utilizzati nelle attività live sono compatibili con Platform Web SDK | Il pubblico che utilizza il componente &quot;Personalizzato&quot; (parametro mbox) deve essere aggiornato per includere gli attributi XDM |
| Tutti gli script di profilo sono compatibili con Platform Web SDK | Tutti gli script di profilo che utilizzano parametri mbox devono essere aggiornati per includere gli attributi XDM |
| Attività restituite per il pubblico Target | È consigliabile eseguire una convalida end-to-end sui tipi di pubblico modificati per renderli compatibili con Platform Web SDK |
| Gli script di profilo valutano come previsto | Visualizzare le tracce di Edge nel debugger |

## Integrazioni con le applicazioni Adobe

| Elemento di convalida | Note |
|---|---|
| Attività restituite per il pubblico di Experience Cloud | Ad esempio, un segmento pubblicato da Adobe Analytics |
| Attività restituite per il pubblico di Experience Platform | Applicabile solo se disponi di una licenza per un’applicazione basata su Experience Platform come RTCDP |
| Attività restituite per il pubblico di Audience Manager | Ad esempio, un segmento in base alla visita di una pagina specifica |
| I dati delle attività di Target vengono visualizzati in Analysis Workspace | Si applica alle attività che utilizzano Adobe Analytics come origine per la generazione di rapporti |

## Integrazioni con applicazioni di terze parti

| Elemento di convalida | Note |
|---|---|
| I dati del token di risposta vengono passati correttamente alle applicazioni di terze parti | Gli approcci all’integrazione possono variare, ma un metodo comune consiste nell’utilizzare i token di risposta di Target per trasmettere informazioni sulle attività e sulle esperienze ad altri strumenti di analisi come Google Analytics |
| Le informazioni provenienti da terze parti vengono trasmesse come XDM o come dati di profilo | Tutte le informazioni rilevanti da terze parti devono essere trasmesse in `sendEvent` chiamate a Target |

Dopo aver eseguito i passaggi di convalida descritti in precedenza, puoi essere certo che l’implementazione di Platform Web SDK sia pronta per il passaggio alla produzione.

Successivamente, scopri come [risolvere i problemi relativi a un&#39;implementazione di Target utilizzando Platform Web SDK](debugging.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
