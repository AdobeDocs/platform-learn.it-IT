---
title: Confronto tra at.js 2.x e SDK per web | Migrare Target da at.js 2.x all’SDK per web
description: Scopri le differenze tra at.js 2.x e Platform Web SDK, tra cui funzioni, funzioni, impostazioni e flusso di dati.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 8%

---

# Confronto tra at.js e SDK per web di Platform

La libreria Adobe Target at.js autonoma è molto diversa dall’SDK per web di Platform. Le tabelle seguenti sono un riferimento per aiutarti a valutare le aree dell’implementazione su cui potresti aver bisogno di concentrarsi durante il processo di migrazione.

Dopo aver esaminato le informazioni riportate di seguito e valutato l’implementazione tecnica di at.js, dovresti essere in grado di comprendere quanto segue:

- Quali funzioni di Target sono supportate da Platform Web SDK
- Quali funzioni di at.js hanno equivalenti SDK per web di Platform
- Applicazione delle impostazioni di Target con Platform Web SDK
- Differenze tra il flusso di dati di at.js e Platform Web SDK

Se hai poca esperienza con l’SDK per web di Platform, non preoccuparti; gli elementi riportati di seguito sono trattati in modo più dettagliato durante questa esercitazione.

## Confronto delle funzioni

|  | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Aggiornare il profilo di Target | Supportato | Supportato |
| Attiva la visualizzazione per SPA | Supportato | Supportato |
| Target Recommendations | Supportato | Supportato |
| Recupera offerte basate su moduli | Supportato | Supportato |
| Tracciare gli eventi | Supportato | Supportato |
| A4T: applicazione a pagina singola | Supportato | Supportato |
| A4T: Tracciamento dei clic | Supportato | Supportato |
| A4T: Registrazione lato client | Supportato | Supportato |
| A4T: Registrazione lato server | Supportato | Supportato |
| Applicare offerte | Supportato | Supportato |
| Esegui nuovamente il rendering della visualizzazione in SPA senza notifiche | Supportato | Supportato |
| Applicazioni ibride | Supportato | Supportato |
| URL di controllo qualità | Supportato | Supportato |
| ID di terze parti di mbox | Supportato | Supportato |
| Attributi del cliente | Supportato | Supportato |
| Offerte remote | Supportato | Supportato |
| Offerte di reindirizzamento | Supportati | Supportati. Tuttavia, non è supportato un reindirizzamento da una pagina con SDK per web di Platform a una pagina con at.js (e nella direzione opposta). |
| Decisioning su dispositivo | Supportati | Non supportato al momento |
| Mbox di preacquisizione | Supportati | Supportato parzialmente. Contatta l’assistenza clienti per abilitare questa funzione in quanto modifica il comportamento di preacquisizione dell’attività. |
| Eventi personalizzati | Supportati | Supportato parzialmente tramite [ganci di monitoraggio](https://github.com/adobe/alloy/wiki/Monitoring-Hooks) |
| Token di risposta | Supportati | Supportati. Fai riferimento a [documentazione dei token di risposta dedicati](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) per esempi di codice e differenze tra at.js e Platform Web SDK |
| Fornitori dati  | Supportati | Non supportati. Il codice personalizzato può essere utilizzato per attivare un SDK per web di Platform `sendEvent` dopo il recupero dei dati da un altro provider. |


## Callout nobili

|  | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Mitigazione dello sfarfallio | Il frammento pre-hiding per le implementazioni asincrone utilizza un ID di stile di `at-body-style`. at.js cerca questo ID elemento per rimuovere lo stile una volta ricevuta una risposta. | Il frammento pre-hiding predefinito utilizza un ID di stile di `alloy-prehiding`. L’SDK web non è compatibile con il frammento pre-hiding di at.js, pertanto deve essere modificato come parte del processo di migrazione. |
| Rendering automatico del contenuto al caricamento della pagina | Controllato con un&#39;impostazione globale di Target. Abilitato quando `pageLoadEnabled` è impostato su `true`. | Specificato nell’SDK per web della piattaforma `sendEvent` comando. Attivata impostando la variabile `renderDecisions` opzione per `true`. |
| Rendering manuale del contenuto | La `applyOffer()` e `applyOffers()` funzioni che supportano solo l’impostazione di HTML | La `applyPropositions` supporta l’impostazione, la sostituzione o l’aggiunta di HTML per una maggiore flessibilità |
| Tracciamento degli eventi personalizzati | Supportato con `trackEvent()` e `sendNotifications()` funzioni. Queste funzioni sono specifiche di Target e non hanno alcun impatto sulle metriche di Adobe Analytics. | Tutti i dati dall’SDK per web di Platform `sendEvent` le chiamate vengono inoltrate a Target. I dati supplementari necessari specificamente per Target devono essere inclusi nella `sendEvent` con un eventType di `decisioning.propositionDisplay` o `decisioning.propositionInteract` per evitare che le metriche di Adobe Analytics siano interessate. |
| CNAME di destinazione | Supportati. È separato dal CNAME utilizzato per Analytics e dal servizio Experience Cloud ID. | Non più rilevante. È possibile utilizzare un singolo CNAME per tutte le chiamate SDK per web di Platform. |
| Eseguire il debug di | La `mboxDisable`, `mboxDebug`e `mboxTrace` I parametri URL possono essere utilizzati per il debug con gli strumenti per sviluppatori del browser.<br><br>Adobe Experience Platform Debugger è anche uno strumento di debug supportato. | La `mboxDisable`, `mboxDebug`e `mboxTrace` I parametri URL non sono supportati.<br><br>Puoi attivare il debug dell’SDK web aggiungendo la variabile `alloy_debug=true` alla stringa di query o all&#39;esecuzione `alloy("setDebug", { "enabled": true });` nella console per sviluppatori.<br><br>L’estensione del browser Adobe Experience Platform Debugger può essere utilizzata per avviare una traccia Edge per il debug.<br><br>Fai riferimento a [debugging di Platform Web SDK](debugging.md) documentazione per ulteriori informazioni. |
| Analytics for Target (A4T) | Utilizza i valori SDID per unire le chiamate di Target e Analytics | Supporto nativo senza unione |

>[!NOTE]
>
>La migrazione di Target all’SDK web di Platform durante il mantenimento di un’implementazione AppMeasurement Adobe Analytics esistente per una determinata pagina non è supportata.
>
> È possibile migrare l’implementazione di at.js (e AppMeasurement.js) all’SDK per web di Platform una pagina alla volta. Se si adotta questo approccio, è meglio impostare la [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) opzioni per `true` con `configure` comando.

## Funzioni di at.js ed equivalenti SDK per web di Platform

Molte funzioni di at.js hanno un approccio equivalente tramite l’SDK per web di Platform descritto nella tabella seguente. Per ulteriori dettagli sulla [Funzioni di at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulta la Guida per gli sviluppatori di Adobe Target.

| funzione at.js 2.x | Equivalente dell’SDK per web di Platform |
| --- | --- | 
| `getOffer()` e `getOffers()` | Per richiedere e [rendering automatico](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) Esperienze basate su VEC di Target, utilizza `sendEvent` e impostare `renderDecisions` su true.<br><br>Per richiedere esperienze basate su moduli o a [rendering manuale](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) contenuto, specificare una matrice di `decisionScopes` (mbox) con `sendEvent` comando. |
| `applyOffer()` e `applyOffers()` | Utilizza la [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) per applicare il contenuto. È possibile scegliere di impostare, sostituire o aggiungere HTML a un selettore specifico. |
| `triggerView()` | Platform Web SDK attiva automaticamente un [modifica visualizzazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) ai fini del VEC SPA se il `web.webPageDetails.viewName` è impostata sotto la `xdm` opzione `sendEvent` comando. |
| `trackEvent()` e `sendNotifications()` | Utilizza la `sendEvent` con un comando [specifico `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) set:<br><br>`decisioning.propositionDisplay` segnala il rendering di un&#39;attività<br><br>`decisioning.propositionInteract` segnala l’interazione dell’utente con un’attività, ad esempio un clic del mouse. |
| `targetGlobalSettings()` | Nessun equivalente diretto. Fai riferimento a [Confronto delle impostazioni di Target](detailed-comparison.md) per ulteriori dettagli. |
| `targetPageParams()` e `targetPageParamsAll()` | Tutti i dati passati nel `xdm` opzione `sendEvent` è mappato ai parametri mbox di Target. Poiché i parametri mbox vengono denominati utilizzando la notazione del punto serializzato, la migrazione a Platform Web SDK potrebbe richiedere l’aggiornamento dei tipi di pubblico e delle attività esistenti per utilizzare i nuovi nomi dei parametri mbox. <br><br>Dati passati come parte di `data.__adobe.target` del `sendEvent` è mappato su [Parametri specifici del profilo di Target e di Recommendations](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| Eventi personalizzati at.js | Non supportati. Tuttavia, [token di risposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) sono esposti come parte del `propositions` nella risposta del `sendEvent` chiama. |

## Impostazioni di at.js ed equivalenti SDK per web di Platform

La libreria at.js può essere configurata e scaricata con varie impostazioni nell’interfaccia utente di Target. Queste impostazioni possono essere aggiornate anche con [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) funzione . La tabella seguente confronta queste impostazioni con quelle disponibili con Platform Web SDK.

| Impostazione at.js | Equivalente dell’SDK per web di Platform |
| --- | --- |
| `bodyHiddenStyle` | Imposta la [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) con `configure` command |
| `bodyHidingEnabled` | Se `prehidingStyle` è definito con `configure` questa funzione è quindi abilitata. Se uno stile non è definito, l’SDK per web di Platform non tenta di nascondere alcun contenuto. |
| `clientCode` | Configurazione automatica |
| `cookieDomain` | Non applicabile |
| `crossDomain` | Imposta la `thirdPartyCookiesEnabled` opzione per `true` con `configure` per abilitare i cookie di prima parte e di terze parti per i casi di utilizzo tra domini diversi |
| `cspScriptNonce` e `cspStyleNonce` | Consulta la documentazione per [configurazione di un CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | Non supportati |
| `decisioningMethod` | SDK Web per tutte le piattaforme `sendEvent` I comandi utilizzano le decisioni lato server. Le decisioni ibride e su dispositivo non sono supportate. |
| `defaultContentHiddenStyle` e `defaultContentVisibleStyle` | Applicabile solo con at.js 1.x. Simile a at.js 2.x, qualsiasi limitazione della visualizzazione momentanea di altri contenuti per esperienze basate su moduli può essere eseguita utilizzando un codice personalizzato. |
| `deviceIdLifetime` | Non supportati. Se `targetMigrationEnabled` è impostato su `true` con `configure` il comando `mbox` il cookie è impostato con la durata del dispositivo impostata su 2 anni. Questo valore non è configurabile. |
| `enabled` | La funzionalità di Target è abilitata o disabilitata con la configurazione del flusso di dati |
| `globalMboxAutoCreate` | Imposta la `renderDecisions` opzione per `true` con `sendEvent` per recuperare ed eseguire automaticamente il rendering delle esperienze basate su VEC.<br><br>Richiedere un `decisionScope` per `__view__` se preferisci eseguire manualmente il rendering delle esperienze basate su VEC. |
| `imsOrgId` | Imposta la `orgId` con `configure` command |
| `optinEnabled` e `optoutEnabled` | Consulta l’SDK per web di Platform [opzioni di privacy](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). La `defaultConsent` Questa opzione si applica a tutte le soluzioni Adobe supportate dall’SDK per web di Platform. |
| `overrideMboxEdgeServer` e `overrideMboxEdgeServerTimeout` | Non applicabile. Tutte le richieste SDK web di Platform utilizzano la rete Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Imposta la `renderDecisions` opzione per `true` con `sendEvent` command |
| `secureOnly` | Non supportati. L’SDK per web di Platform imposta tutti i cookie con `secure` e `sameSite="none"` attributi. |
| `selectorsPollingTimeout` | Non supportati. L’SDK per web di Platform utilizza un valore di 5 secondi. Il codice personalizzato può essere utilizzato per eseguire manualmente il rendering del contenuto, se necessario. |
| `serverDomain` | Utilizza la `edgeDomain` con `configure` command |
| `telemetryEnabled` | Non applicabile |
| `timeout` | Non supportati. È consigliabile assicurarsi che qualsiasi codice di mitigazione della visualizzazione momentanea di altri contenuti includa un timeout appropriato. |
| `viewsEnabled` | Non supportati. Il contenuto per le visualizzazioni di Target viene sempre recuperato sul primo `sendEvent()` chiama se `renderDecisions` è impostato su `true` o `__view__` DecisionScope è incluso nella richiesta. |
| `visitorApiTimeout` | Non applicabile |


## Confronto dei diagrammi di sistema

I seguenti diagrammi devono essere utili per comprendere le differenze di flusso di dati tra un’implementazione di Target utilizzando at.js e un’implementazione utilizzando l’SDK per web di Platform.

### Diagramma di sistema di at.js 2.x

![Comportamento di at.js 2.0 al caricamento della pagina](assets/target-at-js-2x-diagram.png)

| Effettua la chiamata | Dettagli |
| --- | --- |
| 1 | La chiamata restituisce Experience Cloud ID (ECID). Se l’utente è autenticato, un’altra chiamata sincronizza l’ID cliente. |
| 2 | La libreria at.js viene caricata in modo sincrono e nasconde il corpo del documento (at.js può anche essere caricato in modo asincrono con un frammento pre-hiding facoltativo implementato nella pagina). |
| 3 | Viene effettuata la richiesta di caricamento pagina, con tutti i parametri configurati, ECID, SDID e ID cliente. |
| 4 | Gli script di profilo vengono eseguiti e inseriti nell’archivio profili. L’archivio richiede tipi di pubblico idonei dalla libreria Pubblico (ad esempio, audience condivisi da Analytics, Audience Manager e così via). Gli attributi del cliente vengono inviati all’archivio profili in un processo batch. |
| 5 | In base all’URL, ai parametri di richiesta e ai dati di profilo, Target decide quali attività ed esperienze restituire al visitatore per la pagina corrente e le visualizzazioni future. |
| 6 | Contenuto di destinazione inviato nuovamente alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione.<br><br>Il contenuto mirato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br><br>Il contenuto mirato per le visualizzazioni future di un’applicazione a pagina singola viene memorizzato nella cache del browser, in modo che possa essere applicato immediatamente senza una chiamata al server aggiuntiva quando vengono attivate le visualizzazioni. (Vedi il diagramma seguente per il comportamento triggerView() ). |
| 7 | Dati di Analytics inviati dalla pagina ai server di raccolta dati. |
| 8 | I dati di Target vengono confrontati con i dati di Analytics tramite SDID e vengono elaborati nell’archivio dei rapporti di Analytics. È quindi possibile visualizzare i dati di Analytics sia in Analytics che in Target tramite i rapporti A4T. |

Per ulteriori informazioni su come fare riferimento alla guida per gli sviluppatori [implementare Target utilizzando at.js per le applicazioni a pagina singola](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Diagramma del sistema di Platform Web SDK

![Diagramma delle decisioni edge di Adobe Target con Platform Web SDK](assets/target-platform-web-sdk.png)

| Effettua la chiamata | Dettagli |
| --- | --- |
| 1 | Il dispositivo carica l’SDK per web della piattaforma. L’SDK per web di Platform invia una richiesta alla rete perimetrale con dati XDM, l’ID ambiente Datastreams, i parametri passati e l’ID cliente (facoltativo). La pagina (o i contenitori) è prenascosta. |
| 2 | La rete perimetrale invia la richiesta ai servizi perimetrali per arricchirla con l’ID visitatore, il consenso e altre informazioni contestuali, come la geolocalizzazione e i nomi descrittivi dei dispositivi. |
| 3 | La rete perimetrale invia la richiesta di personalizzazione arricchita al server Edge di Target con l’ID visitatore e i parametri passati. |
| 4 | Gli script di profilo vengono eseguiti e quindi inseriti nell’archivio dei profili di Target. L’archiviazione dei profili recupera i segmenti dalla libreria Pubblico (ad esempio, i segmenti condivisi da Adobe Analytics, Adobe Audience Manager e Adobe Experience Platform). |
| 5 | In base ai parametri di richiesta dell’URL e ai dati di profilo, Target determina quali attività ed esperienze visualizzare per il visitatore per la visualizzazione della pagina corrente e per le visualizzazioni preacquisite future. Target invia quindi questo messaggio alla rete perimetrale. |
| 6 | a) La rete perimetrale invia nuovamente la risposta di personalizzazione alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione. Il contenuto personalizzato sulla pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br><br>b) Il contenuto personalizzato per le visualizzazioni mostrate come risultato delle azioni dell’utente in un’applicazione a pagina singola (SPA) viene memorizzato nella cache per il rendering istantaneo senza ulteriori chiamate al server.<br><br>c. La rete perimetrale invia l’ID visitatore e altri valori nei cookie (ad esempio consenso, ID sessione, identità, controllo dei cookie, personalizzazione e così via). |
| 7 | La rete perimetrale inoltra i dettagli di Analytics for Target (A4T) (attività, esperienza e metadati di conversione) al server Edge di Analytics. |

Per ulteriori informazioni su come fare riferimento alla guida per gli sviluppatori [implementare Target utilizzando l’SDK per web della piattaforma per le applicazioni a pagina singola](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

Dopo aver acquisito una buona conoscenza tecnica dell’implementazione di Target corrente e delle funzioni utilizzate, il passaggio successivo consiste nell’eseguire le [configurazione iniziale](initial-setup.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
