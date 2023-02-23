---
title: Panoramica sulla migrazione | Migrare Target da at.js 2.x all’SDK per web
description: Scopri le differenze chiave tra at.js e Platform Web SDK e come pianificare il tuo sforzo di migrazione.=
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# Panoramica sulla migrazione dell’SDK per web di Target at.js in Platform

Il livello di impegno per la migrazione da at.js a Platform Web SDK dipende dalla complessità dell’implementazione corrente e dalle funzionalità di prodotto utilizzate.

Indipendentemente dalla semplicità o complessità dell&#39;implementazione, è importante comprendere appieno lo stato corrente prima di eseguire la migrazione. Questa guida ti aiuta a suddividere i componenti dell’implementazione corrente e a sviluppare un piano gestibile per migrare ogni pezzo.

Il processo di migrazione prevede i seguenti passaggi chiave:

1. Valutare l’implementazione corrente e determinare un approccio di migrazione
1. Configurare i componenti iniziali per la connessione a Adobe Experience Platform Edge Network
1. Aggiorna l’implementazione di base per sostituire at.js con Platform Web SDK
1. Migliora l’implementazione dell’SDK per web di Platform per i tuoi casi d’uso specifici. Ciò può richiedere il passaggio di parametri aggiuntivi, la contabilizzazione delle modifiche alla visualizzazione dell’app a pagina singola (SPA), l’utilizzo di token di risposta e altro ancora.
1. Aggiornare gli oggetti nell’interfaccia di Target, ad esempio script di profilo, attività e definizioni di pubblico
1. Convalida l’implementazione finale prima di effettuare lo switch nell’ambiente di produzione

## Differenze chiave tra at.js e Platform Web SDK

Prima di avviare il processo di migrazione, è importante comprendere le differenze tra at.js e l’SDK per web di Platform.

### Differenze operative

L’SDK per web di Platform combina le funzionalità di più applicazioni Adobe in un’unica libreria. Questo approccio unificato consente di prendere in considerazione le responsabilità e i processi di più team per garantire un’implementazione corretta.

|  | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Proprietà | La libreria at.js è indipendente dalle altre librerie di applicazioni. Le personalizzazioni e la proprietà di queste librerie diverse possono essere allineate a diversi team dell’organizzazione. | La libreria Platform Web SDK e i dati trasmessi sono unificati per tutte le applicazioni Adobe. La proprietà dell’implementazione dell’SDK per web di Platform deve rappresentare le parti interessate di tutte le applicazioni a valle. |
| Manutenzione | Team separati possono lavorare ai miglioramenti dell&#39;implementazione per ogni applicazione Adobe, come Target e Analytics. | Idealmente, un singolo team dovrebbe essere responsabile dei miglioramenti che influiscono sull’implementazione dell’SDK per web di Platform. |
| Processo | Le modifiche a un&#39;implementazione di Target possono seguire un processo che presenta requisiti di cadenza o di controllo qualità diversi rispetto ad altre applicazioni come Analytics. | Le modifiche all’implementazione di Platform Web SDK devono tenere conto di tutte le applicazioni downstream e il processo di controllo qualità e pubblicazione deve essere regolato di conseguenza. |
| Collaborazione | I dati specifici di Target possono essere trasmessi direttamente nelle chiamate di Target. A seconda dell’implementazione, potrebbero essere presenti chiamate Target aggiuntive. Questo non ha alcun impatto diretto sui dati di Adobe Analytics e il coordinamento con il team di analisi non è altrettanto critico. | I dati trasmessi nelle chiamate SDK per web di Platform possono essere inoltrati sia a Target che ad Analytics. È necessario un coordinamento tra i team per garantire che le modifiche non abbiano un impatto negativo su un’applicazione specifica. |

### Differenze tecniche

L’SDK per web di Platform non è un’evoluzione della libreria at.js di Target. Si tratta di un approccio nuovo e unificato per l&#39;implementazione di tutte le applicazioni Adobe per il canale web. Ci sono diverse differenze tecniche di cui tenere conto.

|  | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Funzionalità libreria | Funzionalità di Target fornita da at.js. Integrazioni con altre applicazioni fornite da Visitor.js e AppMeasurement.js | Funzionalità per tutte le applicazioni Adobe fornite da un’unica libreria SDK per web Platform: alloy.js |
| Prestazioni | at.js è una delle librerie multiple che devono essere caricate per la corretta integrazione tra le applicazioni. Questo comporta un tempo di carico inferiore a quello ottimale. | L’SDK per web di Platform è una singola libreria leggera che rimuove la necessità di più librerie specifiche per l’applicazione e migliora le prestazioni di caricamento delle pagine. |
| Richieste | Chiamate separate per ogni applicazione di Adobe. Le chiamate di Target sono in gran parte indipendenti dalle altre chiamate di rete. | Una singola chiamata per tutte le applicazioni Adobe. Le modifiche ai dati trasmessi in queste chiamate potrebbero avere un impatto su più applicazioni downstream. |
| Ordine di caricamento | Per una corretta integrazione con altre applicazioni Adobe è necessario un ordine di caricamento specifico delle librerie e delle chiamate di rete. | L&#39;integrazione corretta non si basa sull&#39;unione di dati da chiamate di rete specifiche per applicazioni diverse, pertanto l&#39;ordine di caricamento non rappresenta un problema. |
| Rete Edge | Utilizza Adobe Experience Cloud Edge Network (tt.omtrdc.net), facoltativamente con un CNAME specifico per Target. | Utilizza Adobe Experience Platform Edge Network (edge.adobedc.net), facoltativamente con un singolo CNAME. |
| Terminologia di base | Denominazione at.js: <br> - `mbox` <br> - `pageLoad` evento (mbox globale) <br> - `offer` | Equivalente SDK per web della piattaforma: <br> - `decisionScope` <br> - `__view__` DecisionScope <br> - `proposition` |

### Video introduttivo

Il video seguente offre una panoramica di Adobe Experience Platform Web SDK e Adobe Experience Platform Edge Network.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

Ora che conosci le differenze di alto livello tra at.js e l’SDK per web di Platform, puoi [pianifica la migrazione](plan-migration.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).