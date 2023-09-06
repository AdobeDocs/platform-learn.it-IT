---
title: Confronto di at.js 2.x con Web SDK | Migrazione di Target da at.js 2.x a Web SDK
description: Scopri le differenze tra at.js 2.x e Platform Web SDK, incluse funzioni, impostazioni e flusso di dati.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 78f0dcc0aa4674eb071c5fd091b5df04eb971326
workflow-type: tm+mt
source-wordcount: '2152'
ht-degree: 8%

---

# Confronto di at.js con Platform Web SDK

La libreria autonoma di Adobe Target at.js è molto diversa da Platform Web SDK. Le tabelle seguenti sono un riferimento per valutare le aree dell’implementazione su cui potrebbe essere necessario concentrarsi durante il processo di migrazione.

Dopo aver esaminato le informazioni riportate di seguito e valutato l’implementazione tecnica di at.js in corso, dovresti essere in grado di comprendere quanto segue:

- Quali funzioni di Target sono supportate da Platform Web SDK
- Quali funzioni at.js hanno equivalenti all’SDK per web di Platform
- Applicazione delle impostazioni di Target con Platform Web SDK
- Differenze tra il flusso di dati di at.js e Platform Web SDK

Se hai poca esperienza con Platform Web SDK, non preoccuparti: gli elementi riportati di seguito vengono trattati più dettagliatamente in questa esercitazione.

## Confronto delle funzioni

| | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Aggiorna profilo Target | Supportato | Supportato |
| Visualizzazione attivatore per SPA | Supportato | Supportato |
| Recommendations di destinazione | Supportato | Supportato |
| Recuperare offerte basate su moduli | Supportato | Supportato |
| Tracciare gli eventi | Supportato | Supportato |
| A4T: applicazione a pagina singola | Supportato | Supportato |
| A4T: Tracciamento dei clic | Supportato | Supportato |
| A4T: registrazione lato client | Supportato | Supportato |
| A4T: registrazione lato server | Supportato | Supportato |
| Applicare le offerte | Supportato | Supportato |
| Visualizza di nuovo il rendering in SPA senza notifiche | Supportato | Supportato |
| Applicazioni ibride | Supportato | Supportato |
| URL di controllo qualità | Supportato | Supportato |
| ID di terze parti Mbox | Supportato | Supportato |
| Attributi del cliente | Supportato | Supportato |
| Offerte remote | Supportato | Supportato |
| Offerte di reindirizzamento | Supportati | Supportati. Tuttavia, non è supportato il reindirizzamento da una pagina con Platform Web SDK a una pagina con at.js (e nella direzione opposta). |
| Decisioning sul dispositivo | Supportati | Non attualmente supportato |
| Preacquisizione di Mbox | Supportato per ambiti personalizzati e Compositore esperienza visivo SPA | Attualmente non supportato per il Compositore esperienza visivo normale |
| Eventi personalizzati | Supportati | Non supportati. Consulta la [roadmap pubblica](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) per lo stato corrente. |
| Token di risposta | Supportati | Supportati. Consulta la sezione [documentazione dei token di risposta dedicati](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) per esempi di codice e differenze tra at.js e Platform Web SDK |
| Fornitori dati  | Supportati | Non supportati. Il codice personalizzato può essere utilizzato per attivare un Platform Web SDK `sendEvent` dopo il recupero dei dati da un altro provider. |


## Callout rilevanti

| | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Attenuazione dello sfarfallio | Il frammento pre-hiding per le implementazioni asincrone utilizza un ID di stile `at-body-style`. at.js cerca questo ID elemento per rimuovere lo stile una volta ricevuta una risposta. | Lo snippet predefinito per il pre-hiding utilizza un ID stile `alloy-prehiding`. L’SDK per web non è compatibile con il frammento pre-hiding di at.js, pertanto deve essere modificato come parte del processo di migrazione. |
| Rendering automatico del contenuto al caricamento della pagina | Controllato con un’impostazione globale di Target. Attivato quando `pageLoadEnabled` è impostato su `true`. | Specificato in Platform Web SDK `sendEvent` comando. Attivato impostando `renderDecisions` opzione per `true`. |
| Rendering manuale del contenuto | Il `applyOffer()` e `applyOffers()` funzioni che supportano l&#39;impostazione solo di HTML | Il `applyPropositions` supporta l&#39;impostazione, la sostituzione o l&#39;aggiunta di HTML per una maggiore flessibilità |
| Tracciamento degli eventi personalizzati | Supportato con `trackEvent()` e `sendNotifications()` funzioni. Queste funzioni sono specifiche di Target e non influiscono sulle metriche di Adobe Analytics. | Tutti i dati da Platform Web SDK `sendEvent` Le chiamate di vengono inoltrate a Target. I dati supplementari specificamente necessari per Target devono essere inclusi nel `sendEvent` con eventType impostato su `decisioning.propositionDisplay` o `decisioning.propositionInteract` per garantire che le metriche di Adobe Analytics non siano influenzate. |
| CNAME di destinazione | Supportati. Questo è separato dal CNAME utilizzato per Analytics e dal servizio ID Experience Cloud. | Non più rilevante. Un singolo CNAME può essere utilizzato per tutte le chiamate dell’SDK web di Platform. |
| Eseguire il debug di | Il `mboxDisable`, `mboxDebug`, e `mboxTrace` I parametri URL possono essere utilizzati per il debug con gli strumenti di sviluppo del browser.<br><br>L’Adobe Experience Platform Debugger è anche uno strumento di debug supportato. | Il `mboxDisable`, `mboxDebug`, e `mboxTrace` I parametri URL non sono supportati.<br><br>Puoi attivare il debug di Web SDK aggiungendo la `alloy_debug=true` nella stringa di query o nell’esecuzione `alloy("setDebug", { "enabled": true });` nella console per sviluppatori.<br><br>L’estensione del browser Adobi Experience Platform Debugger può essere utilizzata per avviare una traccia Edge per il debug.<br><br>Consulta la sezione [debug di Platform Web SDK](debugging.md) per ulteriori informazioni. |
| Analytics for Target (A4T) | Utilizza i valori SDID per unire le chiamate di Target e Analytics | Supportato in modalità nativa senza necessità di unione |

>[!NOTE]
>
>La migrazione di Target a Platform Web SDK durante il mantenimento di un’implementazione AppMeasurement Adobe Analytics esistente per una determinata pagina non è supportata.
>
> È possibile migrare l’implementazione at.js (e AppMeasurement.js) a Platform Web SDK una pagina alla volta. Se si utilizza questo approccio, è consigliabile impostare [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) opzioni per `true` con `configure` comando.

## Funzioni di at.js ed equivalenti di Platform Web SDK

Molte funzioni di at.js hanno un approccio equivalente utilizzando Platform Web SDK descritto nella tabella seguente. Per ulteriori dettagli su [Funzioni di at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulta la Guida per gli sviluppatori di Adobe Target.

| Funzione at.js 2.x | Equivalente di Platform Web SDK |
| --- | --- | 
| `getOffer()` e `getOffers()` | Per richiedere e [rendering automatico](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) Eseguire il targeting delle esperienze basate su VEC, utilizzare il `sendEvent` e impostare `renderDecisions` su true.<br><br>Per richiedere esperienze basate su moduli o per [rendering manuale](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) , specificare una matrice di `decisionScopes` (mbox) con `sendEvent` comando. |
| `applyOffer()` e `applyOffers()` | Utilizza il [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) per applicare il contenuto. Puoi scegliere di impostare, sostituire o aggiungere HTML a un selettore specifico. |
| `triggerView()` | Platform Web SDK attiva automaticamente un [modifica visualizzazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) ai fini del Compositore esperienza visivo dell’SPA se `web.webPageDetails.viewName` è impostata in `xdm` opzione del `sendEvent` comando. |
| `trackEvent()` e `sendNotifications()` | Utilizza il `sendEvent` comando con un [specifico `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) imposta:<br><br>`decisioning.propositionDisplay` segnala il rendering di un’attività<br><br>`decisioning.propositionInteract` segnala un’interazione dell’utente con un’attività, come un clic del mouse. |
| `targetGlobalSettings()` | Nessun equivalente diretto. Consulta la sezione [Confronto delle impostazioni di Target](detailed-comparison.md) per ulteriori dettagli. |
| `targetPageParams()` e `targetPageParamsAll()` | Tutti i dati trasmessi nel `xdm` opzione del `sendEvent` è mappato ai parametri mbox di Target. Poiché i parametri mbox sono denominati utilizzando la notazione con punto serializzato, la migrazione a Platform Web SDK potrebbe richiedere l’aggiornamento dei tipi di pubblico e delle attività esistenti per utilizzare i nuovi nomi dei parametri mbox. <br><br>Dati passati come parte di `data.__adobe.target` del `sendEvent` il comando è mappato a [Parametri specifici del profilo di Target e di Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| Eventi personalizzati at.js | Non supportati. Consulta la [roadmap pubblica](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) per lo stato corrente. [Token di risposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) sono esposti come parte del `propositions` nella risposta del `sendEvent` chiamare. |

## Impostazioni di at.js ed equivalenti di Platform Web SDK

La libreria at.js può essere configurata e scaricata con varie impostazioni nell’interfaccia utente di Target. Queste impostazioni possono anche essere aggiornate con [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) funzione. La tabella seguente confronta queste impostazioni con quelle disponibili con Platform Web SDK.

| Impostazione at.js | Equivalente di Platform Web SDK |
| --- | --- |
| `bodyHiddenStyle` | Imposta il [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) con `configure` comando |
| `bodyHidingEnabled` | Se un `prehidingStyle` è definito con `configure` , questa funzione è abilitata. Se non è definito uno stile, Platform Web SDK non tenta di nascondere alcun contenuto. |
| `clientCode` | Configurazione automatica |
| `cookieDomain` | Non applicabile |
| `crossDomain` | Imposta il `thirdPartyCookiesEnabled` opzione per `true` con `configure` comando per abilitare i cookie di prima parte e di terze parti per i casi di utilizzo tra domini |
| `cspScriptNonce` e `cspStyleNonce` | Consulta la documentazione per [configurazione di un CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | Non supportati |
| `decisioningMethod` | Tutti i Web SDK di Platform `sendEvent` I comandi utilizzano decisioning lato server. Le decisioni ibride e su dispositivo non sono supportate. |
| `defaultContentHiddenStyle` e `defaultContentVisibleStyle` | Applicabile solo con at.js 1.x. Simile a at.js 2.x, qualsiasi mitigazione della visualizzazione momentanea di altri contenuti per esperienze basate su moduli può essere ottenuta utilizzando un codice personalizzato. |
| `deviceIdLifetime` | Non supportati. Se `targetMigrationEnabled` è impostato su `true` con `configure` comando, il `mbox` il cookie è impostato con la durata del dispositivo impostata su 2 anni. Valore non configurabile. |
| `enabled` | La funzionalità di destinazione è abilitata o disabilitata con la configurazione del flusso di dati |
| `globalMboxAutoCreate` | Imposta il `renderDecisions` opzione per `true` con `sendEvent` per recuperare ed eseguire automaticamente il rendering delle esperienze basate sul Compositore esperienza visivo.<br><br>Richiedi `decisionScope` per `__view__` se preferisci eseguire manualmente il rendering di esperienze basate su Compositore esperienza visivo. |
| `imsOrgId` | Imposta il `orgId` con `configure` comando |
| `optinEnabled` e `optoutEnabled` | Consulta Platform Web SDK. [opzioni di privacy](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). Il `defaultConsent` L’opzione si applica a tutte le soluzioni di Adobe supportate da Platform Web SDK. |
| `overrideMboxEdgeServer` e `overrideMboxEdgeServerTimeout` | Non applicabile. Tutte le richieste di Platform Web SDK utilizzano la rete Edge di Adobe Experience Platform. |
| `pageLoadEnabled` | Imposta il `renderDecisions` opzione per `true` con `sendEvent` comando |
| `secureOnly` | Non supportati. Platform Web SDK imposta tutti i cookie con `secure` e `sameSite="none"` attributi. |
| `selectorsPollingTimeout` | Non supportati. Platform Web SDK utilizza un valore di 5 secondi. Se necessario, è possibile utilizzare il codice personalizzato per eseguire manualmente il rendering del contenuto. |
| `serverDomain` | Utilizza il `edgeDomain` impostazione con `configure` comando |
| `telemetryEnabled` | Non applicabile |
| `timeout` | Non supportati. È consigliabile assicurarsi che qualsiasi codice di mitigazione della visualizzazione momentanea di altri contenuti includa un timeout appropriato. |
| `viewsEnabled` | Non supportati. Il contenuto per le visualizzazioni di Target viene sempre recuperato dalla prima `sendEvent()` chiama se `renderDecisions` è impostato su `true` o `__view__` decisionScope è incluso nella richiesta. |
| `visitorApiTimeout` | Non applicabile |


## Confronto dei diagrammi di sistema

I seguenti diagrammi sono utili per comprendere le differenze di flusso di dati tra un’implementazione di Target con at.js e un’implementazione con Platform Web SDK.

### Diagramma del sistema di at.js 2.x

![Comportamento di at.js 2.0 al caricamento della pagina](assets/target-at-js-2x-diagram.png){zoomable=&quot;yes&quot;}

| Effettua la chiamata | Dettagli |
| --- | --- |
| 1 | La chiamata restituisce l’ID Experience Cloud (ECID). Se l&#39;utente è autenticato, un&#39;altra chiamata sincronizza l&#39;ID cliente. |
| 2 | la libreria at.js viene caricata in modo sincrono e nasconde il corpo del documento (at.js può anche essere caricato in modo asincrono con un eventuale snippet prenascosto implementato sulla pagina). |
| 3 | Viene effettuata una richiesta di caricamento della pagina, con tutti i parametri configurati, ECID, SDID e ID cliente. |
| 4 | Gli script di profilo vengono eseguiti e inseriti nell’archivio profili. L’archivio richiede un pubblico idoneo dalla libreria Pubblico (ad esempio, pubblico condiviso da Analytics, Audienci Manager e così via). Gli attributi del cliente vengono inviati all’archivio profili in un processo batch. |
| 5 | In base all’URL, ai parametri di richiesta e ai dati di profilo, Target decide quali attività ed esperienze restituire al visitatore per la pagina corrente e le viste future. |
| 6 | Contenuto di destinazione rinviato alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione.<br><br>Il contenuto mirato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br><br>Il contenuto mirato per le viste future di un’applicazione a pagina singola viene memorizzato nella cache del browser, in modo da applicarlo immediatamente senza una chiamata al server aggiuntiva quando si attivano le viste. |
| 7 | Dati di Analytics inviati dalla pagina ai server di raccolta dati. |
| 8 | I dati di Target vengono confrontati con i dati di Analytics tramite SDID e vengono elaborati nell’archivio dei rapporti di Analytics. È quindi possibile visualizzare i dati di Analytics sia in Analytics che in Target tramite i rapporti A4T. |

Fai riferimento alla guida per gli sviluppatori per ulteriori informazioni su come [Implementare Target utilizzando at.js per applicazioni a pagina singola](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagramma del sistema di Platform Web SDK

![Diagramma di Adobe Target Edge Decisioning con Platform Web SDK](assets/target-platform-web-sdk.png)

| Effettua la chiamata | Dettagli |
| --- | --- |
| 1 | Il dispositivo carica l’SDK web di Platform. Platform Web SDK invia una richiesta alla rete Edge con dati XDM, l’ID dell’ambiente Datastreams, i parametri immessi e l’ID cliente (facoltativo). La pagina (o i contenitori) è nascosta anticipatamente. |
| 2 | La rete Edge invia la richiesta ai servizi Edge di per arricchirla con l’ID visitatore, il consenso e altre informazioni contestuali sul visitatore, come la geolocalizzazione e i nomi descrittivi dei dispositivi. |
| 3 | La rete Edge invia la richiesta di personalizzazione arricchita al server Edge di Target con l’ID visitatore e i parametri immessi. |
| 4 | Gli script di profilo vengono eseguiti e quindi inseriti nell’archiviazione del profilo di Target. L’archiviazione dei profili recupera i segmenti dalla libreria Pubblico (ad esempio, i segmenti condivisi da Adobe Analytics, Adobe Audience Manager e Adobe Experience Platform). |
| 5 | In base ai parametri di richiesta dell’URL e ai dati di profilo, Target determina le attività ed esperienze da visualizzare per il visitatore per la visualizzazione della pagina corrente e per le visualizzazioni preacquisite future. Target quindi lo invia nuovamente alla rete Edge di. |
| 6 | a. La rete Edge invia nuovamente la risposta di personalizzazione alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione. Il contenuto personalizzato nella pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br><br>b. Il contenuto personalizzato per le viste mostrate come risultato delle azioni dell’utente in un’applicazione a pagina singola (SPA) viene memorizzato nella cache per il rendering immediato senza chiamate al server aggiuntive.<br><br>c. La rete Edge invia l’ID visitatore e altri valori nei cookie (ad esempio consenso, ID sessione, identità, controllo dei cookie, personalizzazione e così via). |
| 7 | La rete Edge inoltra i dettagli di Analytics for Target (A4T) (metadati di attività, esperienza e conversione) al server Edge di Analytics. |

Fai riferimento alla guida per gli sviluppatori per ulteriori informazioni su come [implementare Target utilizzando Platform Web SDK per applicazioni a pagina singola](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Dopo aver acquisito una buona conoscenza tecnica dell’implementazione corrente di Target e delle funzioni utilizzate, il passaggio successivo consiste nell’eseguire [configurazione iniziale](initial-setup.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontrate ostacoli durante la migrazione o ritenete che in questa guida manchino informazioni critiche, fatecelo sapere pubblicando [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
