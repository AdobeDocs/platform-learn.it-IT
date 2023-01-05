---
title: Debug | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come eseguire il debug di un’implementazione Adobe Target utilizzando Adobe Experience Platform Web SDK. Gli argomenti includono le opzioni di debug, le estensioni del browser e le differenze tra at.js e Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 4%

---

# Eseguire il debug di Target con l’SDK per web di Platform

Verifica delle attività di Target e debug dell’SDK web per la risoluzione dei problemi di implementazione, distribuzione dei contenuti o qualificazione dell’audience. Questa pagina della guida alla migrazione spiega le differenze tra il debug con at.js e Platform Web SDK.

La tabella seguente riepiloga le funzioni e il supporto per gli approcci di test e debug.

| Funzione o strumento | Supporto at.js | Supporto per l’SDK per web di Platform |
| --- | --- | --- |
| URL di controllo qualità delle attività | Sì | Sì |
| `mboxDisable` Parametro URL | Sì | Fai riferimento alle informazioni seguenti per [disattivare la funzionalità di Target](#disable-target-functionality) |
| `mboxDebug` Parametro URL | Sì | Utilizzo `alloy_debug` parametro per informazioni di debug simili |
| `mboxTrace` Parametro URL | Sì | Utilizzare l’estensione del browser Experience Platform Debugger |
| Estensione Adobe Experience Platform Debugger | Sì | Sì |
| `alloy_debug` Parametro URL | Non applicabile | Sì |
| Adobe Experience Platform Assurance | Non applicabile | Sì |

## Estensione Adobe Experience Platform Debugger del browser

L’estensione Adobe Experience Platform Debugger per Chrome e Firefox esamina le pagine web e ti aiuta a convalidare le implementazioni Adobe Experience Cloud.

Puoi eseguire Platform Debugger su qualsiasi pagina web e l’estensione ha accesso ai dati pubblici. Per accedere ai dati non pubblici utilizzando l’estensione, ad esempio le informazioni di traccia di Target, devi eseguire l’autenticazione per Experience Cloud tramite l’ **[!UICONTROL Accedere]** link.

### Recuperare e installare Adobe Experience Platform Debugger

Adobe Experience Platform Debugger può essere installato nei browser Google Chrome o Mozilla Firefox. Segui il collegamento appropriato riportato di seguito per installare l’estensione sul browser preferito:

- [Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
- [Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/)

Dopo aver installato l’estensione Chrome o il componente aggiuntivo Firefox, un’icona (![](assets/start-icon.jpg)) viene aggiunto alla barra delle estensioni. Seleziona questa icona per aprire l&#39;estensione.

Fai riferimento alla guida dedicata per ulteriori informazioni sui [Estensione Adobe Experience Platform Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html) e come eseguire il debug di tutte le applicazioni web Adobe.

## Anteprima delle attività di Target con URL di controllo qualità

Sia at.js che Platform Web SDK consentono di visualizzare in anteprima le attività Target utilizzando gli URL di controllo qualità di Target; entrambi i metodi di implementazione supportano le stesse funzioni di controllo qualità.

Gli URL di controllo qualità di Target funzionano istruendo at.js o Platform Web SDK a scrivere un cookie specifico nel browser denominato `at_qa_mode`. Questo cookie viene utilizzato per forzare la qualificazione per una particolare attività ed esperienza.

>[!CAUTION]
>
>La funzionalità della modalità di controllo qualità di Target è supportata dall’SDK per web di Platform versione 2.13.0 o successiva. La modalità di controllo qualità di Target è abilitata in base a `xdm.web.webPageDetails.URL` passato nel `sendEvent` chiama. Qualsiasi modifica a questo valore, ad esempio l’eliminazione di tutti i caratteri, potrebbe impedire il corretto funzionamento della modalità di controllo qualità di Target.

Per ulteriori informazioni, consulta la guida dedicata [Controllo di qualità delle attività di Target](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).

## Implementazione di Debug Target

La tabella seguente illustra le differenze tra le tattiche di debug di at.js e Platform Web SDK:

| Funzione at.js | Equivalente dell’SDK per web di Platform |
| --- | --- |
| **Disattiva mbox** - disattivare il recupero e il rendering di Target per verificare se la pagina è interrotta senza le interazioni di Target<br><br>Carica la pagina con il parametro URL: `mboxDisable=true` | Nessun equivalente diretto. Puoi bloccare tutte le richieste Platform Web SDK con gli strumenti per sviluppatori del browser in uso. |
| **Debug mbox** - registra ogni azione at.js nella console del browser per aiutare a risolvere i problemi di rendering<br><br>Carica la pagina con il parametro URL: `mboxDebug=true` | **Debug lega** - registra azioni dettagliate dell’SDK, incluse, tra l’altro, le azioni di personalizzazione Target.<br><br>Carica la pagina con il parametro URL: `alloy_debug=true`  <br /><br />Oppure esegui `alloy("setDebug", { "enabled": true });` in Developer Console |
| **Traccia di destinazione** - con un token di traccia mbox generato nell’interfaccia utente di Target, è disponibile un oggetto trace con i dettagli che hanno partecipato al processo decisionale in `window.___target_trace` oggetto.<br><br>Carica la pagina con il parametro URL: `mboxTrace=window&authorization={TOKEN}` | Utilizza l’estensione Adobe Experience Platform Debugger o Platform Assurance. |

>[!NOTE]
>
>Tutte le funzioni di debug di at.js elencate qui sopra sono disponibili con funzionalità avanzate in Adobe Experience Platform Debugger.

### Disattiva la funzionalità di Target

L’SDK per web di Platform non dispone attualmente di una funzione per sopprimere selettivamente le risposte di Target. Tuttavia, è possibile eliminare le richieste SDK per web di Platform con gli strumenti per sviluppatori del browser, varie estensioni del browser o applicazioni di terze parti. Ad esempio, per bloccare Platform Web SDK con Google Chrome:

1. Fai clic con il pulsante destro del mouse in un punto qualsiasi della pagina e seleziona **Inspect**
1. Seleziona la **Rete** scheda
1. Filtrare per stringa `//ee//` per visualizzare solo le chiamate SDK per web Platform
1. Ricarica la pagina
1. Fai clic con il pulsante destro del mouse su una delle richieste di rete filtrate e seleziona **Dominio di richiesta blocco**
1. Ricarica la pagina e osserva che la richiesta di rete è bloccata
1. Al termine del debug, fai clic con il pulsante destro del mouse sulla richiesta di rete bloccata e seleziona **Sblocca** o chiudi il pannello Strumenti per sviluppatori

### Visualizza registrazione debug

Eseguire il debug della registrazione per at.js utilizzando `mboxDebug=true` Il parametro URL mostra informazioni dettagliate su ogni richiesta, risposta e tentativo di rendering del contenuto sulla pagina. Platform Web SDK ha una registrazione di debug simile utilizzando `alloy_debug=true` Parametro URL.

| Informazioni registrate | at.js (`mboxDebug=true`) | SDK Web per Platform (`alloy_debug=true`) |
| --- | --- | --- |
| Prefisso di registrazione per il filtro | `AT:` | `[alloy]` |
| Dettagli della richiesta di caricamento pagina | Sì | Sì |
| Dettagli richiesta mbox o ambito | Sì | Sì |
| Stato della richiesta | Sì | Sì |
| Dettagli di risposta | Sì | Sì |
| Stato del rendering | Riuscito ed errori | Solo errori |
| Dettagli di rendering | Sì | Sì |

>[!NOTE]
>
>I registri di debug per at.js e Platform Web SDK forniscono un livello di dettaglio simile, con l’eccezione notevole che Web SDK notifica solo gli errori di rendering dovuti a selettori non validi. La registrazione di debug attualmente non conferma che il rendering sia stato eseguito correttamente.

### Visualizzare le tracce di Target

Le tracce di Target forniscono informazioni dettagliate sulle qualifiche di attività e sul profilo di Target del visitatore. Poiché le tracce di Target contengono informazioni non disponibili al pubblico, la loro visualizzazione richiede un token di autorizzazione o l’autenticazione all’interno della finestra dell’estensione del browser Adobe Experience Platform Debugger.

| Metodo di traccia di Target | at.js | SDK Web per Platform |
| --- | --- | --- |
| `mboxTrace` Parametro URL | Sì | No |
| Estensione Adobe Experience Platform Debugger del browser | Sì | Sì |
| Adobe Experience Platform Assurance | No | Sì |


Per visualizzare le tracce di Target dell’SDK per web di Platform con Adobe Experience Platform Debugger, procedi come segue:

1. Passa a una pagina del sito in cui Target è stato implementato con Platform Web SDK
1. Apri l’estensione Adobe Experience Platform Debugger selezionando l’icona (![](assets/start-icon.jpg)) nella barra di navigazione del browser
1. Seleziona la **[!UICONTROL Accesso]** collegamento
1. Autenticazione tramite l’accesso a Adobe Experience Cloud
1. Seleziona la **[!UICONTROL Registri]** scheda a sinistra
1. Seleziona la **[!UICONTROL Bordo]** scheda in alto
1. Se necessario, dai un nome alla sessione di debug e fai clic sul pulsante **[!UICONTROL Connetti]** pulsante
1. Ricarica la pagina e il registro deve compilare con informazioni dettagliate sulle interazioni di rete edge
1. Attiva le voci di registro che iniziano con &quot;Tracce di destinazione&quot; nella descrizione e seleziona **[!UICONTROL Visualizza]** per visualizzare i dettagli di traccia di Target

![Come visualizzare le tracce di Target con Adobe Experience Platform Debugger](assets/target-trace-debugger.png)

Dopo aver selezionato **[!UICONTROL Visualizza]**, viene visualizzata una sovrapposizione che consente di visualizzare le seguenti informazioni relative alla richiesta:

- Attività corrispondenti
- Attività senza pari
- Dettagli richiesta
- Istantanea del profilo

Fai riferimento alla guida dedicata sulle [debugging della distribuzione dei contenuti Target](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html) per ulteriori informazioni sulle tracce di Target.

### Risolvere i problemi con Assurance

Le informazioni di traccia di Target sono visualizzabili sia nell’estensione del browser Adobe Experience Platform Debugger che nell’applicazione Assurance (precedentemente nota come Project Griffon). Per visualizzare le tracce di Target in Assurance, procedi come segue:

1. Apri l’estensione del browser Adobe Experience Platform Debugger e connetti una sessione di debug remoto come descritto sopra
1. Seleziona il collegamento con il nome della sessione sopra il registro di debug
1. Platform Assurance carica e mostra la registrazione dettagliata per tutte le applicazioni Adobe configurate nel flusso di dati per l’implementazione
1. Filtrare il registro per `adobe.target`
1. Selezionare una voce di registro con il tipo `com.adobe.target.trace`
1. Espandi i dettagli del payload e visualizza le informazioni in `context > targetTrace`

![Come visualizzare le tracce di Target con Assurance](assets/target-trace-assurance.png)

## Esamina richiesta e risposta di rete

Payload della richiesta e risposta dell’SDK per web di Platform `sendEvent` le chiamate sono diverse da at.js. La struttura seguente dovrebbe aiutarti a comprendere la struttura della richiesta e della risposta durante l’analisi delle chiamate di rete con gli strumenti per sviluppatori del tuo browser.

### Payload per la richiesta di contenuto

![Elementi specifici di Target del payload dell’SDK per web di Platform](assets/target-payload.png)

- Profilo, entità e altri parametri non mbox vengono passati nell’array eventi in `data.__adobe.target`
- Gli ambiti decisionali si trovano nella matrice eventi in `query.personalization.decisionScopes`
- I dati XDM mappati ai parametri mbox a valle si trovano nell’array eventi in `xdm`

### Corpo di risposta al contenuto

![Individuare elementi specifici del corpo di risposta dell’SDK web di Platform](assets/target-response.png)

- L’SDK per web di Platform restituisce azioni per tutte le applicazioni di Adobe nel `handle` oggetto
- La `personalization:decisions` indica una risposta da Target o offer decisioning
- Le proposizioni di destinazione sono presentate come array, ognuna con un ID di proposizione univoco con il prefisso `AT:`
- L’ambito delle decisioni e i dettagli dell’attività si trovano all’interno della matrice delle proposte
- I dettagli dell’offerta si trovano nella sezione `items` matrice sotto `data`
- I token di risposta si trovano nella `items` matrice sotto `meta`

### Payload evento proposta

![Esempio di evento della proposizione di destinazione](assets/target-proposition-event.png)

- Gli eventi SDK specifici di Target `decisioning.propositionDisplay` per un&#39;impressione o `decisioning.propositionInteract` per un’interazione, ad esempio un clic
- I dettagli dell&#39;evento di proposizione si trovano nell&#39;array di eventi in `xdm._experience.decisioning`
- L’ID della proposizione dell’evento di visualizzazione o di interazione deve corrispondere all’ID della proposizione del contenuto restituito da Target


Congratulazioni, hai raggiunto la fine del tutorial! Buona fortuna per la migrazione dell’implementazione Adobe Target all’SDK per web.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
