---
title: Confronto dell’estensione Target con l’estensione Decisioning
description: Scopri le differenze tra at.js 2.x e Platform Web SDK, incluse funzioni, impostazioni e flusso di dati.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Confronto dell’estensione Target con l’estensione Decisioning

La libreria autonoma di Adobe Target at.js è molto diversa da Platform Web SDK. Le tabelle seguenti sono un riferimento per valutare le aree dell’implementazione su cui potrebbe essere necessario concentrarsi durante il processo di migrazione.

Dopo aver esaminato le informazioni riportate di seguito e valutato l’implementazione tecnica di at.js in corso, dovresti essere in grado di comprendere quanto segue:

- Quali funzioni di Target sono supportate da Platform Web SDK
- Quali funzioni at.js hanno equivalenti all’SDK per web di Platform
- Applicazione delle impostazioni di Target con Platform Web SDK
- Differenze tra il flusso di dati di at.js e Platform Web SDK

Se hai poca esperienza con Platform Web SDK, non preoccuparti: gli elementi riportati di seguito vengono trattati più dettagliatamente in questa esercitazione.

## Confronto delle funzioni

| | Estensione Target | Estensione Decisioning (Target tramite Edge) | Esperienze basate su codice di AJO (SDK per la messaggistica) |
|---|---|---|---|
| Modalità di preacquisizione | Supportato | Supportato | Supportato |
| Modalità di esecuzione | Supportato | Non supportato | Non supportato |
| Parametri personalizzati | Supportato | I parametri per mbox non sono supportati | Non supportato |
| Pubblico di ingresso | Supportato | Supportato | Supportato tramite l’impostazione di sospensione di tipi di pubblico di Campaign e di esperimento |
| Segmentazione del pubblico utilizzando le metriche del ciclo di vita mobile | Supportato | Supportato tramite regole di raccolta dati | Il targeting delle esperienze non è al momento supportato |
| thirdPartyId (mbox3rdPartyId) | Supportato tramite Identity Map e la configurazione dello spazio dei nomi nello stream di dati | Non supportato |
| Notifiche (visualizzazione, clic) | Supportato | Supportato | Supportato |
| Token di risposta | Supportato | Supportato | Nessun equivalente per la restituzione di metadati specifici di Campaign al di fuori del contenuto |
| Offerte dinamiche | Supportato | Supportato | È supportato il rendering dei token correlati a profili e elementi decisionali nel contenuto |
| Analytics for Target (A4T) | Solo lato client | Lato client e lato server | Non supportato |
| Anteprime per dispositivi mobili (modalità QA) | Supportato | Supporto limitato | In corso |



## Callout rilevanti

>[!NOTE]
>
>La migrazione di Target a Platform Web SDK durante il mantenimento di un’implementazione AppMeasurement Adobe Analytics esistente per una determinata pagina non è supportata.
>
> È possibile migrare l’implementazione at.js (e AppMeasurement.js) a Platform Web SDK una pagina alla volta. Se si utilizza questo approccio, è consigliabile impostare le opzioni [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) e [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) su `true` con il comando `configure`.

## Funzioni di estensione di Target ed equivalenti di estensione di Decisioning

Molte funzioni di estensione di Target hanno un approccio equivalente che utilizza l’estensione Decisioning descritta nella tabella seguente. Per ulteriori dettagli sulle [funzioni](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consulta la Guida per gli sviluppatori di Adobe Target.

| Estensione Target | Estensione Decisioning |
| --- | --- | 
| |  |

## Impostazioni dell’estensione Target ed equivalenti dell’estensione Decisioning

L&#39;estensione Target può essere configurata e scaricata con varie impostazioni in ...

| Estensione Target | Estensione Decisioning |
| --- | --- | 
| |  |


## Confronto dei diagrammi di sistema

I seguenti diagrammi sono utili per comprendere le differenze di flusso di dati tra un’implementazione di Target con at.js e un’implementazione con Platform Web SDK.

### Diagramma del sistema di estensione di Target



### Diagramma del sistema di estensione Decisioning




>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
