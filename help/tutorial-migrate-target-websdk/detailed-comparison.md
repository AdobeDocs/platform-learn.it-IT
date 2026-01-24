---
title: 'Confronto di at.js 2.x con Web SDK: migrazione di Target da at.js 2.x a Web SDK'
description: Scopri le differenze tra at.js 2.x e Platform Web SDK, incluse funzioni, impostazioni e flusso di dati.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 7d3c1728925e322f9313cf71f081500e0c0bac0b
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 2%

---

# Confronto di at.js con Platform Web SDK

La libreria autonoma at.js di Adobe Target differisce notevolmente da Platform Web SDK. Le tabelle seguenti sono un riferimento per valutare le aree dell’implementazione su cui potrebbe essere necessario concentrarsi durante il processo di migrazione.

Dopo aver esaminato le informazioni riportate di seguito e valutato l’implementazione tecnica di at.js in corso, dovresti essere in grado di comprendere quanto segue:

- Quali funzionalità di Target sono supportate da Platform Web SDK
- Quali funzioni at.js hanno equivalenti a Platform Web SDK
- Applicazione delle impostazioni di Target con Platform Web SDK
- Differenze tra il flusso di dati di at.js e Platform Web SDK

Se hai poca esperienza con Platform Web SDK, non preoccuparti: gli elementi riportati di seguito vengono trattati più dettagliatamente in questa esercitazione.

## Confronto delle funzioni

| | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Aggiorna profilo Target | Supportato | Supportato |
| Attiva visualizzazione per applicazioni a pagina singola | Supportato | Supportato |
| Consigli di Target | Supportato | Supportato |
| Recuperare offerte basate su moduli | Supportato | Supportato |
| Tracciare gli eventi | Supportato | Supportato |
| A4T: applicazione a pagina singola | Supportato | Supportato |
| A4T: Tracciamento dei clic | Supportato | Supportato |
| A4T: registrazione lato client | Supportato | Supportato |
| A4T: registrazione lato server | Supportato | Supportato |
| Applicare le offerte | Supportato | Supportato |
| Riesegui il rendering della vista nell’applicazione a pagina singola senza notifiche | Supportato | Supportato |
| Applicazioni ibride | Supportato | Supportato |
| URL di controllo qualità | Supportato | Supportato |
| ID di terze parti Mbox | Supportato | Supportato |
| Attributi del cliente | Supportato | Supportato |
| Offerte remote | Supportato | Parzialmente supportato. Offerte remote dinamiche non supportate. |
| Offerte di reindirizzamento | Supportato | Supportato. Tuttavia, non è supportato il reindirizzamento da una pagina con Platform Web SDK a una pagina con at.js (e nella direzione opposta). |
| Decisioning sul dispositivo | Supportato | Non attualmente supportato |
| Preacquisizione di Mbox | Supportato per ambiti personalizzati e Compositore esperienza visivo per applicazioni a pagina singola | Preacquisizione è la modalità predefinita per Web SDK |
| Eventi personalizzati | Supportato | Non supportato. Per informazioni sullo stato corrente, consulta la [roadmap pubblica](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"}). |
| Token di risposta | Supportato | Supportato. Consulta la [documentazione dedicata sui token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=it) per esempi di codice e differenze tra at.js e Platform Web SDK |
| Fornitori di dati | Supportato | Non supportato. Il codice personalizzato può essere utilizzato per attivare un comando Platform Web SDK `sendEvent` dopo il recupero dei dati da un altro provider. |


## Callout rilevanti

| | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Attenuazione dello sfarfallio | Il frammento pre-hiding per le implementazioni asincrone utilizza un ID di stile di `at-body-style`. at.js cerca questo ID elemento per rimuovere lo stile una volta ricevuta una risposta. | Lo snippet predefinito per il pre-hiding utilizza un ID di stile di `alloy-prehiding`. Il Web SDK non è compatibile con il frammento pre-hiding di at.js, pertanto deve essere modificato durante il processo di migrazione. |
| Rendering automatico del contenuto al caricamento della pagina | Controllato con un’impostazione globale di Target. Abilitato quando `pageLoadEnabled` è impostato su `true`. | Specificato nel comando `sendEvent` di Platform Web SDK. Attivato impostando l&#39;opzione `renderDecisions` su `true`. |
| Rendering manuale del contenuto | Le funzioni `applyOffer()` e `applyOffers()` supportano l&#39;impostazione solo di HTML | Il comando `applyPropositions` supporta l&#39;impostazione, la sostituzione o l&#39;aggiunta di HTML per una maggiore flessibilità |
| Tracciamento degli eventi personalizzati | Supportato con `trackEvent()` e `sendNotifications()` funzioni. Queste funzioni sono specifiche di Target e non influiscono sulle metriche di Adobe Analytics. | Tutti i dati dalle chiamate di Platform Web SDK `sendEvent` vengono inoltrati a Target. I dati supplementari necessari specificatamente per Target devono essere inclusi con il comando `sendEvent` con eventType `decisioning.propositionDisplay` o `decisioning.propositionInteract` per garantire che le metriche di Adobe Analytics non siano interessate. |
| CNAME di destinazione | Supportato. Questo è separato dal CNAME utilizzato per Analytics e dal servizio Experience Cloud ID. | Non più rilevante. Un singolo CNAME può essere utilizzato per tutte le chiamate di Platform Web SDK. |
| Debug | I parametri URL `mboxDisable`, `mboxDebug` e `mboxTrace` possono essere utilizzati per il debug con gli strumenti di sviluppo del browser.<br><br>Adobe Experience Platform Debugger è anche uno strumento di debug supportato. | I parametri URL `mboxDisable`, `mboxDebug` e `mboxTrace` non sono supportati.<br><br>Puoi attivare il debug di Web SDK aggiungendo `alloy_debug=true` alla stringa di query o eseguendo `alloy("setDebug", { "enabled": true });` nella console per sviluppatori.<br><br>L&#39;estensione del browser Adobe Experience Platform Debugger può essere utilizzata per avviare una traccia Edge per il debug.<br><br>Per ulteriori informazioni, consultare la [documentazione relativa al debug di Platform Web SDK](debugging.md). |
| Analytics for Target (A4T) | Utilizza i valori SDID per unire le chiamate di Target e Analytics | Supportato in modalità nativa senza necessità di unione |

>[!NOTE]
>
>La migrazione di Target a Platform Web SDK durante il mantenimento di un’implementazione AppMeasurement Adobe Analytics esistente per una determinata pagina non è supportata.
>
> È possibile migrare l’implementazione at.js (e AppMeasurement.js) a Platform Web SDK una pagina alla volta. Se si utilizza questo approccio, è consigliabile impostare le opzioni [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=it#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=it#targetMigrationEnabled) su `true` con il comando `configure`.

## Funzioni di at.js ed equivalenti di Platform Web SDK

Molte funzioni di at.js hanno un approccio equivalente che utilizza Platform Web SDK descritto nella tabella seguente. Per ulteriori dettagli sulle [funzioni at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulta la Guida per gli sviluppatori di Adobe Target.

| Funzione at.js 2.x | Equivalente di Platform Web SDK |
| --- | --- | 
| `getOffer()` e `getOffers()` | Per richiedere e [eseguire automaticamente il rendering](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=it#automatically-rendering-content) delle esperienze basate sul Compositore esperienza visivo di Target, utilizzare il comando `sendEvent` e impostare l&#39;opzione `renderDecisions` su true.<br><br>Per richiedere esperienze basate su moduli o per [eseguire manualmente il rendering del contenuto](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=it#manually-rendering-content), specifica una matrice di `decisionScopes` (mbox) con il comando `sendEvent`. |
| `applyOffer()` e `applyOffers()` | Utilizzare il comando [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=it#applypropositions) per applicare il contenuto. È possibile scegliere di impostare, sostituire o aggiungere HTML a un selettore specifico. |
| `triggerView()` | Platform Web SDK attiva automaticamente una [modifica della visualizzazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=it#how-to-trigger-a-view-change-in-a-single-page-application) ai fini del Compositore esperienza visivo per applicazioni a pagina singola se la proprietà `web.webPageDetails.viewName` è impostata nell&#39;opzione `xdm` del comando `sendEvent`. |
| `trackEvent()` e `sendNotifications()` | Utilizza il comando `sendEvent` con un set [`eventType` &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html?lang=it#how-to-track-events) specifico:<br><br>`decisioning.propositionDisplay` segnala il rendering di un&#39;attività<br><br>`decisioning.propositionInteract` segnala un&#39;interazione dell&#39;utente con un&#39;attività, come un clic del mouse. |
| `targetGlobalSettings()` | Nessun equivalente diretto. Per ulteriori dettagli, consulta il [confronto delle impostazioni di Target](detailed-comparison.md). |
| `targetPageParams()` e `targetPageParamsAll()` | Tutti i dati passati nell&#39;opzione `xdm` del comando `sendEvent` sono mappati ai parametri mbox di Target. Poiché i parametri mbox sono denominati utilizzando la notazione con punti serializzati, la migrazione a Platform Web SDK potrebbe richiedere l’aggiornamento dei tipi di pubblico e delle attività esistenti per l’utilizzo dei nuovi nomi di parametri mbox. <br><br>I dati passati come parte di `data.__adobe.target` del comando `sendEvent` sono mappati a [Parametri specifici del profilo di destinazione e della funzione Consigli](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=it#single-profile-update). |
| Eventi personalizzati at.js | Non supportato. Per informazioni sullo stato corrente, consulta la [roadmap pubblica](https://github.com/orgs/adobe/projects/18/views/1?pane=item&itemId=17372355{target="_blank"}). [I token di risposta](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html?lang=it) sono esposti come parte di `propositions` nella risposta della chiamata `sendEvent`. |

## Impostazioni di at.js ed equivalenti di Platform Web SDK

La libreria at.js può essere configurata e scaricata con varie impostazioni nell’interfaccia utente di Target. Queste impostazioni possono anche essere aggiornate con la funzione [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/). La tabella seguente confronta queste impostazioni con quelle disponibili con Platform Web SDK.

| Impostazione at.js | Equivalente di Platform Web SDK |
| --- | --- |
| `bodyHiddenStyle` | Imposta [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=it#prehidingStyle) con il comando `configure` |
| `bodyHidingEnabled` | Se un `prehidingStyle` è definito con il comando `configure`, questa funzione è abilitata. Se non è definito uno stile, Platform Web SDK non tenta di nascondere alcun contenuto. |
| `clientCode` | Configurazione automatica |
| `cookieDomain` | Non applicabile |
| `crossDomain` | Imposta l&#39;opzione `thirdPartyCookiesEnabled` su `true` con il comando `configure` per abilitare i cookie di prime e terze parti per i casi di utilizzo tra domini diversi |
| `cspScriptNonce` e `cspStyleNonce` | Consulta la documentazione per [configurazione di un CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html?lang=it) |
| `dataProviders` | Non supportato |
| `decisioningMethod` | Tutti i comandi di Platform Web SDK `sendEvent` utilizzano le decisioni lato server. Le decisioni ibride e su dispositivo non sono supportate. |
| `defaultContentHiddenStyle` e `defaultContentVisibleStyle` | Applicabile solo con at.js 1.x. Simile a at.js 2.x, qualsiasi mitigazione della visualizzazione momentanea di altri contenuti per esperienze basate su moduli può essere ottenuta utilizzando un codice personalizzato. |
| `deviceIdLifetime` | Non supportato. Se `targetMigrationEnabled` è impostato su `true` con il comando `configure`, il cookie `mbox` viene impostato con la durata del dispositivo impostata su 2 anni. Valore non configurabile. |
| `enabled` | La funzionalità di destinazione è abilitata o disabilitata con la configurazione del flusso di dati |
| `globalMboxAutoCreate` | Imposta l&#39;opzione `renderDecisions` su `true` con il comando `sendEvent` per recuperare ed eseguire automaticamente il rendering delle esperienze basate sul Compositore esperienza visivo.<br><br>Richiedi `decisionScope` per `__view__` se preferisci eseguire manualmente il rendering delle esperienze basate su Compositore esperienza visivo. |
| `imsOrgId` | Imposta `orgId` con il comando `configure` |
| `optinEnabled` e `optoutEnabled` | Consulta le [opzioni per la privacy](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=it) di Platform Web SDK. L&#39;opzione `defaultConsent` si applica a tutte le soluzioni Adobe supportate da Platform Web SDK. |
| `overrideMboxEdgeServer` e `overrideMboxEdgeServerTimeout` | Non applicabile. Tutte le richieste di Platform Web SDK utilizzano la rete Adobe Experience Platform Edge. |
| `pageLoadEnabled` | Imposta l&#39;opzione `renderDecisions` su `true` con il comando `sendEvent` |
| `secureOnly` | Non supportato. Platform Web SDK imposta tutti i cookie con gli attributi `secure` e `sameSite="none"`. |
| `selectorsPollingTimeout` | Non supportato. Platform Web SDK utilizza un valore di 5 secondi. Se necessario, è possibile utilizzare il codice personalizzato per eseguire manualmente il rendering del contenuto. |
| `serverDomain` | Utilizza l&#39;impostazione `edgeDomain` con il comando `configure` |
| `telemetryEnabled` | Non applicabile |
| `timeout` | Non supportato. È consigliabile assicurarsi che qualsiasi codice di mitigazione della visualizzazione momentanea di altri contenuti includa un timeout appropriato. |
| `viewsEnabled` | Non supportato. Il contenuto per le visualizzazioni di Target viene sempre recuperato alla prima chiamata `sendEvent()` se `renderDecisions` è impostato su `true` o se il decisionScope `__view__` è incluso nella richiesta. |
| `visitorApiTimeout` | Non applicabile |


## Confronto dei diagrammi di sistema

I seguenti diagrammi sono utili per comprendere le differenze di flusso di dati tra un’implementazione di Target con at.js e un’implementazione con Platform Web SDK.

### Diagramma del sistema di at.js 2.x

Comportamento di ![at.js 2.0 al caricamento della pagina](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| Chiamata | Dettagli |
| --- | --- |
| 1 | La chiamata restituisce Experience Cloud ID (ECID). Se l&#39;utente è autenticato, un&#39;altra chiamata sincronizza l&#39;ID cliente. |
| 2 | la libreria at.js viene caricata in modo sincrono e nasconde il corpo del documento (at.js può anche essere caricato in modo asincrono con un eventuale snippet prenascosto implementato sulla pagina). |
| 3 | Viene effettuata una richiesta di caricamento della pagina, con tutti i parametri configurati, ECID, SDID e ID cliente. |
| 4 | Gli script di profilo vengono eseguiti e inseriti nell’archivio profili. L’archivio richiede un pubblico idoneo dalla libreria Pubblico (ad esempio, pubblico condiviso da Analytics, Audience Manager e così via). Gli attributi del cliente vengono inviati all’archivio profili in un processo batch. |
| 5 | In base all’URL, ai parametri di richiesta e ai dati di profilo, Target decide quali attività ed esperienze restituire al visitatore per la pagina corrente e le viste future. |
| 6 | Contenuto di destinazione rinviato alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione.<br><br>Il contenuto di destinazione nella pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br><br>Il contenuto di destinazione per le viste future di un&#39;applicazione a pagina singola è memorizzato nella cache del browser, quindi può essere applicato immediatamente senza una chiamata al server aggiuntiva quando si attivano le viste. |
| 7 | Dati di Analytics inviati dalla pagina ai server di raccolta dati. |
| 8 | I dati di Target vengono confrontati con i dati di Analytics tramite SDID ed elaborati nell’archivio dei rapporti di Analytics. I dati di Analytics possono quindi essere visualizzati sia in Analytics che in Target tramite i rapporti A4T. |

Per ulteriori informazioni su come [implementare Target utilizzando at.js per applicazioni a pagina singola](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/), consulta la guida per sviluppatori.

### Diagramma del sistema di Platform Web SDK

![Diagramma di Adobe Target Edge Decisioning con Platform Web SDK](assets/target-platform-web-sdk.png)

| Chiamata | Dettagli |
| --- | --- |
| 1 | Il dispositivo carica Platform Web SDK. Platform Web SDK invia una richiesta alla rete Edge con dati XDM, l’ID ambiente Datastreams, i parametri immessi e l’ID cliente (facoltativo). La pagina (o i contenitori) è nascosta anticipatamente. |
| 2 | La rete Edge invia la richiesta ai servizi Edge di per arricchirla con l’ID visitatore, il consenso e altre informazioni contestuali sul visitatore, come la geolocalizzazione e i nomi descrittivi dei dispositivi. |
| 3 | La rete Edge invia la richiesta di personalizzazione arricchita al server Edge di Target con l’ID visitatore e i parametri immessi. |
| 4 | Gli script di profilo vengono eseguiti e quindi inseriti nell’archiviazione del profilo di Target. L’archiviazione dei profili recupera i segmenti dalla libreria Pubblico (ad esempio, i segmenti condivisi da Adobe Analytics, Adobe Audience Manager e Adobe Experience Platform). |
| 5 | In base ai parametri di richiesta dell’URL e ai dati di profilo, Target determina le attività ed esperienze da visualizzare per il visitatore per la visualizzazione della pagina corrente e per le visualizzazioni preacquisite future. Target quindi lo invia nuovamente alla rete Edge di. |
| 6 | a. La rete Edge invia nuovamente la risposta di personalizzazione alla pagina, includendo facoltativamente i valori di profilo per ulteriore personalizzazione. Il contenuto personalizzato nella pagina corrente viene mostrato il più rapidamente possibile senza che venga visualizzato momentaneamente il contenuto predefinito.<br><br> b. Il contenuto personalizzato per le viste mostrate come risultato delle azioni dell’utente in un’applicazione a pagina singola viene memorizzato nella cache per il rendering immediato senza chiamate al server aggiuntive.<br><br>c. La rete Edge invia l’ID visitatore e altri valori nei cookie (ad esempio consenso, ID sessione, identità, controllo dei cookie, personalizzazione e così via). |
| 7 | La rete Edge inoltra i dettagli di Analytics for Target (A4T) (metadati di attività, esperienza e conversione) al server Edge di Analytics. |

Per ulteriori informazioni su come [implementare Target utilizzando Platform Web SDK per applicazioni a pagina singola](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=it), consultare la guida per gli sviluppatori.

Dopo aver acquisito una buona conoscenza tecnica dell&#39;implementazione corrente di Target e delle funzionalità utilizzate, il passaggio successivo consiste nell&#39;eseguire la [configurazione iniziale](initial-setup.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=it#M463).
