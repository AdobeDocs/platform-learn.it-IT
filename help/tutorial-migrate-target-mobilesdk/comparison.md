---
title: Confronto dell’estensione Target con l’estensione Decisioning
description: Scopri le differenze tra l’estensione Target e l’estensione Decisioning, incluse funzioni, funzioni, impostazioni e flusso di dati.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---

# Confronto dell’estensione Target con l’estensione Decisioning

L’estensione Adobe Journey Optimizer - Decisioning è diversa dall’estensione Adobe Target per le app mobili. Le tabelle seguenti sono un riferimento per valutare le aree dell’implementazione su cui potrebbe essere necessario concentrarsi durante il processo di migrazione.

Dopo aver esaminato le informazioni riportate di seguito e valutato l’implementazione corrente dell’estensione tecnica di Target, dovresti essere in grado di comprendere quanto segue:

- Quali funzioni di Target sono supportate da Adobe Journey Optimizer - Decisioning
- Quali funzioni di estensione di Adobe Target dispongono di equivalenti Adobe Journey Optimizer - Decisioning
- Applicazione delle impostazioni di Target con Adobe Journey Optimizer - Decisioning
- Flusso dei dati tramite l’estensione Adobe Journey Optimizer - Decisioning

## Differenze operative

| | Estensione Target | Estensione Decisioning |
|---|---|---|
| Processo | Le modifiche all’implementazione di un Target possono seguire un processo con una cadenza o requisiti di controllo qualità diversi rispetto ad altre applicazioni come Analytics. | Le modifiche all’implementazione di un’estensione Decisioning devono tenere conto di tutte le applicazioni a valle e il processo di controllo qualità e pubblicazione deve essere modificato di conseguenza. |
| Collaborazione | I dati specifici di Target possono essere trasmessi direttamente nelle chiamate di Target. Se l’origine per la generazione di rapporti di Target è Adobe Analytics (A4T), i dati specifici di Target possono anche essere passati ad Adobe Analytics quando vengono chiamati i metodi di tracciamento appropriati nell’estensione Target per la visualizzazione e l’interazione dei contenuti di Target. | I dati passati nelle chiamate di estensione di Decisioning possono essere inoltrati sia a Target che ad Analytics se l’origine per la generazione di rapporti di Target è Adobe Analytics (A4T), se Adobe Analytics è abilitato nel flusso di dati e se vengono chiamati i metodi di tracciamento appropriati nell’estensione di Decisioning quando il contenuto di Target viene visualizzato e interagito con. |

## Differenze di base

| | Estensione Target | Estensione Decisioning |
|---|---|---|
| Dipendenze | Dipende solo da Mobile Core SDK | Dipende da Mobile Core e Edge Network SDK |
| Funzionalità libreria | Supporta il recupero di contenuti solo da Adobe Target | Supporto per il recupero di contenuti da Adobe Target e Offer Decisioning |
| Richieste | Le chiamate di Target sono ampiamente indipendenti da altre chiamate di rete | Le chiamate di rete di Target vengono messe in coda insieme alle chiamate di rete per altre soluzioni basate su Edge, come la messaggistica nel SDK di Edge, ed eseguite in serie. |
| Edge Network | Utilizza il valore del server di Target o l&#39;Edge Network di Adobe Experience Cloud con il codice client (clientcode.tt.omtrdc.net), entrambi specificati nella [configurazione di Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) nell&#39;interfaccia utente di Data Collection | Utilizza il dominio di rete Edge specificato nella [configurazione Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) di Adobe Experience Platform nell&#39;interfaccia utente di Data Collection. |
| Terminologia di base | mbox, TargetParameters | DecisionScope, Map (Android)/dictionary (iOS) for Target parameters |
| Contenuto predefinito | Consente di trasmettere il contenuto predefinito lato client in TargetRequest restituito se la chiamata di rete non riesce o genera un errore. | Non consente il passaggio di contenuto predefinito lato client. Non restituisce alcun contenuto se la chiamata di rete non riesce o genera un errore. |
| Parametri di destinazione | Consente il passaggio di TargetParameters globali per richiesta e di diversi TargetParameters per mbox | Consente il passaggio di parametri di Target globali solo per richiesta |



## Confronto delle funzioni

| Funzione | Estensione Target | Estensione Decisioning (Target tramite Edge) |
|---|---|---|
| Modalità di preacquisizione | Supportato | Supportato |
| Modalità di esecuzione | Supportato | Non supportato |
| Parametri personalizzati | Supportato | Supportato* |
| Parametri del profilo | Supportato | Supportato* |
| Parametri di entità | Supportato | Supportato* |
| Tipi di pubblico di destinazione | Supportato | Supportato |
| Pubblico Real-Time CDP | Non supportato | Supportato |
| Attributi Real-Time CDP | Non supportato | Supportato |
| Metriche del ciclo di vita | Supportato | Supportato tramite regole di raccolta dati |
| thirdPartyId (mbox3rdPartyId) | Supportato | Supportato tramite Identity Map e Target Third Party ID Namespace nello stream di dati |
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
>Mantieni la configurazione e le impostazioni dei tag dell’estensione Target anche dopo aver migrato il codice dell’app all’estensione Decisioning. Questo aiuterà a garantire che Target continui a funzionare per i clienti che non hanno ancora aggiornato l’app alla nuova versione.
>
>Se utilizzi l’integrazione Analytics for Target (A4T), assicurati anche di migrare l’implementazione di Analytics con l’estensione Edge Bridge nello stesso momento in cui esegui la migrazione dell’implementazione di Target all’estensione Decisioning.





>[!IMPORTANT]
>
> Mantieni le impostazioni dell’estensione Target anche dopo aver eseguito la migrazione del codice dell’app all’estensione Decisioning. Questo aiuterà a garantire che Target continui a funzionare per gli utenti che non hanno ancora aggiornato la loro app.

## Diagramma del sistema di estensione Decisioning

Il diagramma seguente dovrebbe aiutarti a comprendere il flusso di dati utilizzando l’estensione Adobe Journey Optimizer - Decisioning.

![Adobe Target Edge Decisioning con Mobile SDK lato client](assets/diagram.png)


>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
