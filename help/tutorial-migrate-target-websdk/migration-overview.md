---
title: Panoramica sulla migrazione | Migrazione di Target da at.js 2.x a Web SDK
description: Scopri le differenze principali tra at.js e Platform Web SDK e come pianificare le attività di migrazione.
exl-id: a8ed78e4-c8c2-4505-b4b5-e5d508f5ed87
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# Panoramica sulla migrazione da at.js a Platform Web SDK

Il livello di impegno per la migrazione da at.js a Platform Web SDK dipende dalla complessità dell’implementazione corrente e dalle funzioni del prodotto utilizzate.

Indipendentemente dalla semplicità o dalla complessità dell’implementazione, è importante comprendere appieno lo stato corrente prima di eseguire la migrazione. Questa guida ti aiuta a suddividere i componenti dell’implementazione corrente e a sviluppare un piano gestibile per migrare ogni elemento.

Il processo di migrazione prevede i seguenti passaggi chiave:

1. Valuta l’implementazione corrente e determina un approccio alla migrazione
1. Imposta i componenti iniziali per la connessione alla rete Edge di Adobe Experience Platform
1. Aggiornare l’implementazione di base per sostituire at.js con Platform Web SDK
1. Migliora l’implementazione di Platform Web SDK per i tuoi casi d’uso specifici. Questo può comportare il passaggio di parametri aggiuntivi, la considerazione delle modifiche di visualizzazione delle app a pagina singola (SPA), l’utilizzo di token di risposta e altro ancora.
1. Aggiornare oggetti nell’interfaccia di Target, ad esempio script di profilo, attività e definizioni di pubblico
1. Convalidare l’implementazione finale prima di effettuare lo switch nell’ambiente di produzione

## Differenze chiave tra at.js e Platform Web SDK

Prima di avviare il processo di migrazione, è importante comprendere le differenze tra at.js e Platform Web SDK.

### Differenze operative

Platform Web SDK combina le funzionalità di più applicazioni Adobe in un’unica libreria. Grazie a questo approccio unificato, è necessario prendere in considerazione le responsabilità e i processi tra i vari team per garantire un’implementazione sana.

| | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Proprietà | La libreria at.js è indipendente da altre librerie di applicazioni. Le personalizzazioni e la proprietà di queste diverse librerie possono essere allineate ai diversi team dell’organizzazione. | La libreria Web SDK di Platform e i dati trasmessi sono unificati per tutte le applicazioni Adobe. La proprietà dell’implementazione di Platform Web SDK deve rappresentare le parti interessate di tutte le applicazioni a valle. |
| Manutenzione | Team separati possono lavorare su miglioramenti dell’implementazione per ogni applicazione di Adobe, come Target e Analytics. | Idealmente, un singolo team dovrebbe essere responsabile dei miglioramenti che influiscono sull’implementazione di Platform Web SDK. |
| Processo | Le modifiche all’implementazione di un Target possono seguire un processo con una cadenza o requisiti di controllo qualità diversi rispetto ad altre applicazioni come Analytics. | Le modifiche all’implementazione di un SDK web per Platform devono tenere conto di tutte le applicazioni a valle e il processo di controllo qualità e pubblicazione deve essere modificato di conseguenza. |
| Collaborazione | I dati specifici di Target possono essere trasmessi direttamente nelle chiamate di Target. A seconda dell’implementazione, potrebbero esserci chiamate Target aggiuntive. Questo non ha un impatto diretto sui dati di Adobe Analytics e il coordinamento con il team di analisi non è così importante. | I dati trasmessi nelle chiamate all’SDK web di Platform possono essere inoltrati sia a Target che ad Analytics. È necessario il coordinamento tra i team per garantire che le modifiche non abbiano un impatto negativo su un’applicazione specifica. |

### Differenze tecniche

Platform Web SDK non è un’evoluzione della libreria at.js di Target. Si tratta di un approccio nuovo e unificato per l’implementazione di tutte le applicazioni Adobe per il canale web. Ci sono diverse differenze tecniche di cui essere consapevoli.

| | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Funzionalità libreria | Funzionalità di Target fornita da at.js. Integrazioni con altre applicazioni fornite da Visitor.js e AppMeasurement.js | Funzionalità per tutte le applicazioni Adobe fornite da una singola libreria Platform Web SDK: alloy.js |
| Prestazioni | at.js è una delle librerie multiple che devono essere caricate per la corretta integrazione tra le applicazioni. Questo determina un tempo di caricamento inferiore al ottimale. | Platform Web SDK è un’unica libreria leggera che elimina la necessità di utilizzare più librerie specifiche per l’applicazione, migliorando le prestazioni di caricamento delle pagine. |
| Richieste | Chiamate separate per ogni applicazione di Adobe. Le chiamate di Target sono in gran parte indipendenti da altre chiamate di rete. | Una singola chiamata per tutte le applicazioni Adobe. Le modifiche ai dati passati in queste chiamate potrebbero influire su più applicazioni a valle. |
| Ordine di caricamento | La corretta integrazione con altre applicazioni Adobe richiede un ordine di caricamento specifico delle librerie e delle chiamate di rete. | La corretta integrazione non si basa sull’unione di dati da diverse chiamate di rete specifiche per l’applicazione, pertanto l’ordine di caricamento non costituisce un problema. |
| Rete Edge | Utilizza Adobe Experience Cloud Edge Network (tt.omtrdc.net), facoltativamente con un CNAME specifico per Target. | Utilizza Adobe Experience Platform Edge Network (edge.adobedc.net), facoltativamente con un singolo CNAME. |
| Terminologia di base | Denominazione at.js: <br> - `mbox` <br> - `pageLoad` evento (mbox globale) <br> - `offer` | equivalente a Platform Web SDK: <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### Video introduttivo

Il video seguente offre una panoramica di Adobe Experience Platform Web SDK e Adobe Experience Platform Edge Network.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?learn=on)

Ora che conosci le differenze di alto livello tra at.js e Platform Web SDK, puoi [pianificare la migrazione](plan-migration.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontrate ostacoli durante la migrazione o ritenete che in questa guida manchino informazioni critiche, fatecelo sapere pubblicando [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
