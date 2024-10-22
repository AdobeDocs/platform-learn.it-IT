---
title: Confronto dell’estensione Target con l’estensione Decisioning
description: Scopri le differenze tra l’estensione Target e l’estensione Decisioning, incluse funzioni, funzioni, impostazioni e flusso di dati.
source-git-commit: 78d04d625aa55ce5eb76615c220b49aefd958431
workflow-type: tm+mt
source-wordcount: '469'
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
| Parametri personalizzati | Supportato | I parametri per mbox non sono supportati |
| Pubblico di ingresso | Supportato | Supportato |
| Segmentazione del pubblico utilizzando le metriche del ciclo di vita mobile | Supportato | Supportato tramite regole di raccolta dati |
| thirdPartyId (mbox3rdPartyId) | Supportato tramite Identity Map e la configurazione dello spazio dei nomi nello stream di dati |
| Notifiche (visualizzazione, clic) | Supportato | Supportato |
| Token di risposta | Supportato | Supportato |
| Offerte dinamiche | Supportato | Supportato |
| Analytics for Target (A4T) | Solo lato client | Lato client e lato server |
| Anteprime per dispositivi mobili (modalità QA) | Supportato | Supporto limitato |



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

I seguenti diagrammi dovrebbero aiutarti a comprendere le differenze di flusso di dati tra un’implementazione di Target tramite l’estensione Adobe Journey Optimizer - Decisioning e un’implementazione tramite l’estensione Adobe Target.

### Diagramma del sistema di estensione di Target



### Diagramma del sistema di estensione Decisioning




>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
