---
title: Confronto dell’estensione Target con l’estensione Offer Decisioning e Target
description: Scopri le differenze tra l’estensione Target per Offer Decisioning e l’estensione Target, incluse funzioni, funzioni, impostazioni e flusso di dati.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 1%

---

# Confronto dell’estensione Target con l’estensione Offer Decisioning e Target

L&#39;estensione Offer Decisioning e Target è diversa dall&#39;estensione Adobe Target per le app mobili. Le tabelle seguenti sono un riferimento per valutare le aree dell’implementazione su cui potrebbe essere necessario concentrarsi durante il processo di migrazione.

Dopo aver esaminato le informazioni riportate di seguito e valutato l’implementazione corrente dell’estensione tecnica di Target, dovresti essere in grado di comprendere quanto segue:

- Quali funzioni di Target sono supportate da Offer Decisioning e Target
- Quali funzioni di estensione di Adobe Target hanno equivalenti ad Offer Decisioning e Target
- Applicazione delle impostazioni di Target con Offer Decisioning e Target
- Flussi di dati tramite l’estensione Offer Decisioning e Target

## Differenze operative

| | Estensione Target | Estensione Offer Decisioning e Target |
|---|---|---|
| Processo | Le modifiche all’implementazione di un Target possono seguire un processo con una cadenza o requisiti di controllo qualità diversi rispetto ad altre applicazioni come Analytics. | Le modifiche apportate all’implementazione di un’estensione Offer Decisioning e Target devono tenere conto di tutte le applicazioni a valle e i processi di controllo qualità e pubblicazione devono essere adeguati di conseguenza. |
| Collaborazione | I dati specifici di Target possono essere trasmessi direttamente nelle chiamate di Target. Se l’origine per la generazione di rapporti di Target è Adobe Analytics (A4T), i dati specifici di Target possono anche essere passati ad Adobe Analytics quando vengono chiamati i metodi di tracciamento appropriati nell’estensione Target per la visualizzazione e l’interazione dei contenuti di Target. | I dati passati nelle chiamate di estensione di Offer Decisioning e Target possono essere inoltrati sia a Target che ad Analytics se l&#39;origine per la generazione di rapporti di Target è Adobe Analytics (A4T), Adobe Analytics è abilitato nel flusso di dati e vengono chiamati metodi di tracciamento appropriati in Offer Decisioning e nell&#39;estensione di Target quando il contenuto di Target viene visualizzato e interagito con. |

## Differenze di base

| | Estensione Target | Estensione Offer Decisioning e Target |
|---|---|---|
| Dipendenze | Dipende solo da Mobile Core SDK | Dipende da Mobile Core e Edge Network SDK |
| Funzionalità libreria | Supporta il recupero di contenuti solo da Adobe Target | Supporto per il recupero di contenuti da Adobe Target e Offer Decisioning |
| Richieste | Le chiamate di Target sono ampiamente indipendenti da altre chiamate di rete | Le chiamate di rete di Target vengono messe in coda insieme alle chiamate di rete per altre soluzioni basate su Edge, come la messaggistica nel SDK di Edge, ed eseguite in serie. |
| Edge Network | Utilizza il valore del server di Target o l&#39;Edge Network di Adobe Experience Cloud con il codice client (clientcode.tt.omtrdc.net), entrambi specificati nella [configurazione di Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) nell&#39;interfaccia utente di Data Collection | Utilizza il dominio di rete Edge specificato nella [configurazione Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) di Adobe Experience Platform nell&#39;interfaccia utente di Data Collection. |
| Terminologia di base | mbox, TargetParameters | DecisionScope, Map (Android)/dictionary (iOS) for Target parameters |
| Contenuto predefinito | Consente di trasmettere il contenuto predefinito lato client in TargetRequest restituito se la chiamata di rete non riesce o genera un errore. | Non consente il passaggio di contenuto predefinito lato client. Non restituisce alcun contenuto se la chiamata di rete non riesce o genera un errore. |
| Parametri di destinazione | Consente il passaggio di TargetParameters globali per richiesta e di diversi TargetParameters per mbox | Consente il passaggio di parametri di Target globali solo per richiesta |



## Confronto delle funzioni

| Funzione | Estensione Target | Estensione Offer Decisioning e Target (Target tramite Edge) |
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
| Anteprime per dispositivi mobili (modalità QA) | Supportato | Supporto limitato con Assurance |

>[!IMPORTANT]
>
> \* I parametri inviati in una richiesta si applicano a tutti gli ambiti della richiesta. Se devi impostare parametri diversi per ambiti diversi, devi effettuare richieste aggiuntive.



## Callout rilevanti

>[!NOTE]
>
>Mantieni la configurazione e le impostazioni dei tag dell’estensione Target anche dopo aver eseguito la migrazione del codice dell’app all’estensione Offer Decisioning e Target. Questo aiuterà a garantire che Target continui a funzionare per i clienti che non hanno ancora aggiornato l’app alla nuova versione.
>
>Se utilizzi l’integrazione Analytics for Target (A4T), assicurati anche di migrare l’implementazione di Analytics con l’estensione Edge Bridge e di migrare l’implementazione di Target all’estensione Offer Decisioning e Target.





>[!IMPORTANT]
>
> Mantieni le impostazioni di estensione Target anche dopo aver eseguito la migrazione del codice app all’estensione Offer Decisioning e Target. Questo aiuterà a garantire che Target continui a funzionare per gli utenti che non hanno ancora aggiornato la loro app.

## Diagramma del sistema di estensione di Offer Decisioning e Target

Il diagramma seguente dovrebbe aiutarti a comprendere il flusso di dati utilizzando l’estensione Offer Decisioning e Target.

![Adobe Target Edge Decisioning con Mobile SDK lato client](assets/diagram.png)


>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target per dispositivi mobili dall’estensione Target all’estensione Offer Decisioning e Target. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
