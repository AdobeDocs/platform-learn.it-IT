---
title: Pianificare la migrazione - Migrare da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning per dispositivi mobili
description: Scopri le differenze principali tra at.js e Platform Web SDK e come pianificare le attività di migrazione.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Pianificare la migrazione

Il livello di impegno per la migrazione dall’estensione Target all’estensione Decisioning dipende dalla complessità dell’implementazione corrente e dalle funzioni del prodotto utilizzate.

Indipendentemente dalla semplicità o dalla complessità dell’implementazione, è importante comprendere appieno lo stato corrente prima di eseguire la migrazione. Questa guida ti aiuta a suddividere i componenti dell’implementazione corrente e a sviluppare un piano gestibile per migrare ogni elemento.

Il processo di migrazione prevede i seguenti passaggi chiave:

1. Valuta l’implementazione corrente e determina un approccio alla migrazione
1. Impostare i componenti iniziali per la connessione all&#39;Edge Network di Adobe Experience Platform
1. Aggiorna l’implementazione fondamentale per sostituire l’estensione Target e l’estensione Decisioning
1. Migliora l’implementazione Ottimizza SDK per casi d’uso specifici. Questo può comportare il passaggio di parametri aggiuntivi, l’utilizzo di token di risposta e altro ancora.
1. Aggiornare oggetti nell’interfaccia di Target, ad esempio script di profilo, attività e definizioni di pubblico
1. Convalidare l’implementazione finale prima di effettuare lo switch nell’ambiente di produzione

## Differenze chiave tra l’estensione Target e l’estensione Decisioning

Prima di avviare il processo di migrazione, è importante comprendere le differenze tra l’estensione Target e l’estensione Decisioning.

### Differenze operative

| | Target at.js 2.x | SDK Web per Platform |
|---|---|---|
| Processo | Le modifiche all’implementazione di un Target possono seguire un processo con una cadenza o requisiti di controllo qualità diversi rispetto ad altre applicazioni come Analytics. | Le modifiche all’implementazione di un’estensione Decisioning devono tenere conto di tutte le applicazioni a valle e il processo di controllo qualità e pubblicazione deve essere modificato di conseguenza. |
| Collaborazione | I dati specifici di Target possono essere trasmessi direttamente nelle chiamate di Target. Se l’origine per la generazione di rapporti di Target è Adobe Analytics, i dati specifici di Target possono essere passati ad Adobe Analytics anche quando vengono chiamati i metodi di tracciamento appropriati nell’estensione Target per la visualizzazione e l’interazione dei contenuti di Target. | I dati passati nelle chiamate di estensione di Decisioning possono essere inoltrati sia a Target che ad Analytics se l’origine per la generazione di rapporti di Target è Adobe Analytics, se Adobe Analytics è abilitato nel flusso di dati e se vengono chiamati metodi di tracciamento appropriati nell’estensione di Decisioning quando il contenuto di Target viene visualizzato e interagito con. |

### Differenze tecniche

| | Estensione Target | Estensione Decisioning |
|---|---|---|
| Dipendenze | Dipende solo da Mobile Core SDK | Dipende da Mobile Core e Edge Network SDK |
| Funzionalità libreria | Supporta il recupero di contenuti solo da Adobe Target | Supporto per il recupero di contenuti da Adobe Target e Offer decisioning |
| Richieste | Le chiamate di Target sono ampiamente indipendenti da altre chiamate di rete | Le chiamate di rete di Target vengono messe in coda insieme alle chiamate di rete per altre soluzioni basate su Edge, come la messaggistica nel SDK di Edge, ed eseguite in serie. |
| Edge Network | Utilizza il valore del server di Target o l&#39;Edge Network di Adobe Experience Cloud con il codice client (clientcode.tt.omtrdc.net), entrambi specificati nella [configurazione di Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) nell&#39;interfaccia utente di Data Collection | Utilizza il dominio di rete Edge specificato nella [configurazione Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) di Adobe Experience Platform nell&#39;interfaccia utente di Data Collection. |
| Terminologia di base | mbox, TargetParameters | DecisionScope, Map (Android)/dictionary (iOS) per i parametri di destinazione |
| Contenuto predefinito | Consente di trasmettere il contenuto predefinito lato client in TargetRequest restituito se la chiamata di rete non riesce o genera un errore. | Non consente il passaggio di contenuto predefinito lato client. Non restituisce alcun contenuto se la chiamata di rete non riesce o genera un errore. |
| Parametri di destinazione | Consente il passaggio di TargetParameters globali per richiesta e di diversi TargetParameters per mbox | Consente il passaggio di parametri di Target globali solo per richiesta |

Rivedi quindi il confronto dettagliato [tra l&#39;estensione Target e l&#39;estensione Decisioning](detailed-comparison.md) per comprendere meglio le differenze tecniche e identificare le aree che richiedono un&#39;attenzione aggiuntiva.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
