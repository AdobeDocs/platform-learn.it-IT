---
title: Confronto dell’estensione Target con l’estensione Decisioning
description: Scopri le differenze tra l’estensione Target e l’estensione Decisioning, incluse funzioni, funzioni, impostazioni e flusso di dati.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 05b0146256c6f8644e42f851498a0f49ff44bf68
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---

# Confronto dell’estensione Target con l’estensione Decisioning

L’estensione Adobe Journey Optimizer - Decisioning è diversa dall’estensione Adobe Target per le app mobili. Le tabelle seguenti sono un riferimento per valutare le aree dell’implementazione su cui potrebbe essere necessario concentrarsi durante il processo di migrazione.

Dopo aver esaminato le informazioni riportate di seguito e valutato l’implementazione corrente dell’estensione tecnica di Target, dovresti essere in grado di comprendere quanto segue:

- Quali funzioni di Target sono supportate da Adobe Journey Optimizer - Decisioning
- Quali funzioni di estensione di Adobe Target dispongono di equivalenti Adobe Journey Optimizer - Decisioning
- Applicazione delle impostazioni di Target con Adobe Journey Optimizer - Decisioning
- Differenze tra il flusso di dati dell’estensione Adobe Target e l’estensione Adobe Journey Optimizer - Decisioning

Se hai poca esperienza con Platform Web SDK, non preoccuparti: gli elementi riportati di seguito vengono trattati più dettagliatamente in questa esercitazione.

## Confronto delle funzioni

| Funzione | Estensione Target | Estensione Decisioning (Target tramite Edge) |
|---|---|---|
| Modalità di preacquisizione | Supportato | Supportato |
| Modalità di esecuzione | Supportato | Non supportato |
| Parametri personalizzati | Supportato | Supportato* |
| Parametri del profilo | Supportato | Supportato* |
| Parametri di entità | Supportato | Supportato* |
| Tipi di pubblico di destinazione | Supportato | Supportato |
| Pubblico Real-Time CDP | ??? | Supportato |
| Attributi Real-Time CDP | ??? | Supportato |
| Metriche del ciclo di vita | Supportato | Supportato tramite regole di raccolta dati |
| thirdPartyId (mbox3rdPartyId) | Supportato | Supportato tramite Identity Map e la configurazione dello spazio dei nomi nello stream di dati |
| Notifiche (visualizzazione, clic) | Supportato | Supportato |
| Token di risposta | Supportato | Supportato |
| Analytics for Target (A4T) | Solo lato client | Lato client e lato server |
| Anteprime per dispositivi mobili (modalità QA) | Supportato | Supporto limitato con Assurance |

>[!IMPORTANT]
>
> \* I parametri inviati in una richiesta si applicano a tutti gli ambiti della richiesta. Se devi impostare parametri diversi per ambiti diversi, devi effettuare richieste aggiuntive.



## Callout rilevanti

>[!NOTE]
>
>La migrazione di Target a Platform Web SDK durante il mantenimento di un’implementazione AppMeasurement Adobe Analytics esistente per una determinata pagina non è supportata.
>
> È possibile migrare l’implementazione at.js (e AppMeasurement.js) a Platform Web SDK una pagina alla volta. Se si utilizza questo approccio, è consigliabile impostare le opzioni [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) su `true` con il comando `configure`.

## Funzioni di estensione di Target ed equivalenti di estensione di Decisioning

Molte funzioni di estensione di Target hanno un approccio equivalente che utilizza l’estensione Decisioning descritta nella tabella seguente. Per ulteriori dettagli sulle [funzioni](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulta la Guida per gli sviluppatori di Adobe Target.

| Estensione Target | Estensione Decisioning | Note |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Quando si utilizza l&#39;API `getPropositions`, non viene effettuata alcuna chiamata remota per recuperare gli ambiti non memorizzati in cache nell&#39;SDK. |
| `displayedLocations` | Offerta -> `displayed()` | È inoltre possibile utilizzare il metodo di offerta `generateDisplayInteractionXdm` per generare XDM per la visualizzazione degli elementi. Successivamente, l’API sendEvent dell’SDK di rete Edge può essere utilizzata per allegare dati XDM aggiuntivi in formato libero e inviare un evento esperienza al remoto. |
| `clickedLocation` | Offerta -> `tapped()` | Inoltre, è possibile utilizzare il metodo di offerta `generateTapInteractionXdm` per generare XDM per il tocco dell&#39;elemento. Successivamente, l’API sendEvent dell’SDK di rete Edge può essere utilizzata per allegare dati XDM aggiuntivi in formato libero e inviare un evento esperienza al remoto. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` |  | Utilizza l&#39;API `removeIdentity` da Identity, ad Edge Network l&#39;estensione per l&#39;SDK, per interrompere l&#39;invio dell&#39;identificatore del visitatore alla rete Edge. Per ulteriori dettagli, consulta [la documentazione dell&#39;API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Nota: l&#39;API `resetIdentities` del core mobile cancella tutte le identità memorizzate nell&#39;SDK, incluso l&#39;ID Experience Cloud (ECID), e dovrebbe essere utilizzata con moderazione. |
| `getSessionId` |  | L&#39;handle di risposta `state:store` contiene informazioni relative alla sessione. L’estensione di rete Edge consente di gestirla allegando elementi dell’archivio di stato non scaduti alle richieste successive. |
| `setSessionId` |  | L&#39;handle di risposta `state:store` contiene informazioni relative alla sessione. L’estensione di rete Edge consente di gestirla allegando elementi dell’archivio di stato non scaduti alle richieste successive. |
| `getThirdPartyId` | n/d | Utilizza l’API updateIdentities da Identity, ad Edge Network l’estensione, per fornire il valore dell’ID di terze parti. Quindi, configura lo spazio dei nomi ID di terze parti nello stream di dati. Per ulteriori dettagli, consulta [la documentazione mobile sull&#39;ID di terze parti di Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/d | Utilizza l’API updateIdentities da Identity, ad Edge Network l’estensione, per fornire il valore dell’ID di terze parti. Quindi, configura lo spazio dei nomi ID di terze parti nello stream di dati. Per ulteriori dettagli, consulta [la documentazione mobile sull&#39;ID di terze parti di Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` |  | L&#39;handle di risposta `locationHint:result` contiene le informazioni dell&#39;hint di posizione di destinazione. Si presume che Target Edge sarà posizionato in modo congiunto con Experience Edge. <br> <br>L&#39;estensione di rete Edge utilizza l&#39;hint di posizione EdgeNetwork per determinare il cluster di rete Edge a cui inviare le richieste. Per condividere l&#39;hint della posizione di rete di Edge tra gli SDK (app ibride), utilizza le API `getLocationHint` e `setLocationHint` dell&#39;estensione Edge Network. Per ulteriori dettagli, consulta [la documentazione dell&#39;API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

## Impostazioni dell’estensione Target ed equivalenti dell’estensione Decisioning

L&#39;estensione Target può essere configurata e scaricata con varie impostazioni in ...

| Estensione Target | Estensione Decisioning |
| --- | --- | 
| |  |


## Confronto dei diagrammi di sistema

I seguenti diagrammi dovrebbero aiutarti a comprendere le differenze di flusso di dati tra un’implementazione di Target tramite l’estensione Adobe Journey Optimizer - Decisioning e un’implementazione tramite l’estensione Adobe Target.

### Diagramma del sistema di estensione di Target



### Diagramma del sistema di estensione Decisioning




>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
