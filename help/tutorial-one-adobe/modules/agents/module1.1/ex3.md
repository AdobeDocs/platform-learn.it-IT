---
title: Adobe Marketing Agent for Microsoft 365 Copilot
description: Adobe Marketing Agent per Microsoft 365 CopilotCopilot
kt: 5342
doc-type: tutorial
source-git-commit: 44d0e98ae4c7568411cb0e01ed8eff38b4a34137
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# 1.1.3 Adobe Marketing Agent for Microsoft 365 Copilot

>[!IMPORTANT]
>
>Questa esercitazione utilizza una funzione che non è ancora stata rilasciata. La funzione è ancora in fase di sviluppo e quindi non è ancora disponibile a livello generale.

[!BADGE Beta]

+++Dettagli Beta
Utilizzando il Adobe Marketing Agent con Microsoft 365 Copilot Beta, l&#39;Utente riconosce che il Beta viene fornito &quot;così com&#39;è&quot; senza alcuna garanzia di alcun tipo. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Beta. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Beta e/o dei materiali di accompagnamento. Beta è considerata un&#39;informazione riservata di Adobe.  Qualsiasi &quot;Feedback&quot; (informazioni relative a Beta, compresi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

+++

## Prerequisiti

Per seguire i passaggi descritti in questa esercitazione, come documentato di seguito, è necessario disporre dei seguenti diritti di accesso:

- Accesso a Real-Time CDP, Journey Optimizer e Customer Journey Analytics
- Accesso all’Assistente all’intelligenza artificiale in Adobe Experience Cloud
- Accesso ad AEP Agent Orchestrator
- Accesso a Microsoft 365 Copilot

## Video

Questo video illustra e illustra tutti i passaggi di questo esercizio.

>[!VIDEO](https://video.tv.adobe.com/v/3479158?quality=12&learn=on)

## 1.1.3.1 Aggiungi Adobe Marketing Agent a Microsoft 365 Teams e Copilot

Apri Microsoft Teams e accedi utilizzando i dettagli del tuo account. Una volta effettuato l’accesso, dovresti visualizzarlo.

Fare clic su **App**.

![ChatGPT](./images/copilot1.png)

Seleziona **Gestione app**.

![ChatGPT](./images/copilot2.png)

Seleziona **Carica un&#39;app**.

![ChatGPT](./images/copilot3.png)

Seleziona **Carica un&#39;app personalizzata**.

![ChatGPT](./images/copilot4.png)

Selezionare il file manifesto fornito dall&#39;istruttore e fare clic su **Apri**.

![ChatGPT](./images/copilot5.png)

Fai clic su **Aggiungi**.

![ChatGPT](./images/copilot6.png)

Fare clic su **Apri con Copilot**.

![ChatGPT](./images/copilot7.png)

Adobe Marketing Agent ora è caricato correttamente.

![ChatGPT](./images/copilot8.png)

Immettere il prompt `login` e fare clic sul pulsante **invia**.

![ChatGPT](./images/copilotlogin1.png)

Fai clic su **Accedi a Adobe Marketing Agent**.

![ChatGPT](./images/copilotlogin2.png)

Viene visualizzata una nuova finestra in cui viene richiesto di accedere con le credenziali dell’account Adobe.

![ChatGPT](./images/copilotlogin3.png)

Dopo aver eseguito correttamente l’autenticazione, potrebbe essere necessario selezionare l’istanza specifica da utilizzare. Se visualizzi questa schermata, seleziona l’istanza —aepImsOrgName—.

![ChatGPT](./images/copilotlogin4.png)

Verrà quindi generato un codice simile. Fai clic su **Copia** per copiare il codice.

![ChatGPT](./images/copilotlogin5.png)

Incollare il codice nella finestra di Adobe Marketing Agent in Copilot e fare clic sul pulsante **invia**.

![ChatGPT](./images/copilotlogin6.png)

Dovresti vedere qualcosa di simile a questo. Hai effettuato correttamente l’accesso a Adobe Marketing Agent in Microsoft 365 Copilot.

![ChatGPT](./images/copilotlogin7.png)

## 1.1.3.2 Imposta contesto in Adobe Marketing Agent

Prima di interagire ulteriormente con Adobe Marketing Agent tramite Copilot, è necessario impostare il contesto.

Per questo esercizio, il contesto deve essere impostato per utilizzare:

- **Sandbox**: **Prod - Accelerate (VA7)**

  L’impostazione sandbox consente di identificare quale sandbox AI Assistant deve esaminare quando si pongono domande.

- **Visualizzazione dati**: **Accelerare il B2C del 2026**

  L’impostazione della visualizzazione dati consente di identificare quale visualizzazione dati deve essere esaminata dall’Assistente IA per l’analisi dei dati quando si pongono domande.

![Agent Orchestrator](./images/copilotlogin7.png)

Per modificare la sandbox, immetti il comando seguente e fai clic sul pulsante **invia**.

```javascript
change sandbox
```

![Agent Orchestrator](./images/copilot9.png)

Dovresti vedere qualcosa di simile a questo. Seleziona la sandbox da utilizzare e fai clic su **seleziona**.

![Agent Orchestrator](./images/copilot10.png)

Dovresti vedere questo. Per modificare la visualizzazione dati, immettere il comando seguente e fare clic sul pulsante **invia**.

```javascript
change dataview
```

![Agent Orchestrator](./images/copilot11.png)

Dovresti vedere qualcosa di simile a questo. Seleziona la visualizzazione dati da utilizzare e fai clic su **seleziona**.

![Agent Orchestrator](./images/copilot12.png)

Dovresti vedere questo. Il contesto ora è impostato correttamente, quindi puoi iniziare a inviare successivamente richieste specifiche.

![Agent Orchestrator](./images/copilot13.png)

## 1.1.3.3 Inizia con le tendenze generali di acquisto per ancorare il contesto e ingrandire la visualizzazione della fibra

**Intento**

Ottieni un impulso a livello di toplevel sulla domanda di categoria: mobile, rete fissa, Internet, TV, fibra ottica, in particolare per gli ultimi 60 giorni. Questo stabilisce le linee di base per la stagionalità, gli effetti promozionali e la varianza regionale dopo il rollout di New York.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by mainCategory over the last 4 months.
```

![Agent Orchestrator](./images/copilot18.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/copilot19.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by mainCategory = Fiber over the last 4 months broken down by week
```

![Agent Orchestrator](./images/copilot20.png)

Dovresti vedere questo, che approfondisce le tendenze specifiche della fibra.

![Agent Orchestrator](./images/copilot21.png)

## 1.1.3.4 Correlazione degli ordini con le preferenze del contenuto

**Intento**

Testare l&#39;ipotesi che una preferenza per un genere specifico (ad esempio, SciFi, Sport, Drammatico) preveda il comportamento di aggiornamento della banda larga, in particolare per le esigenze di larghezza di banda elevata.

Innanzitutto, devi scoprire quale campo viene utilizzato per memorizzare la preferenza di genere.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which field is used to store the preferred genre
```

![Agent Orchestrator](./images/copilot22.png)

Dovresti visualizzarlo, il che mostra che il campo utilizzato per il genere è **_experienceplatform.individualCharacteristics.preferences.preferredGenre**.

![Agent Orchestrator](./images/copilot23.png)

Con tali informazioni, puoi iniziare a espandere i dati di acquisto.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me ordersYTD by preferredGenre for the last 4 months
```

![Agent Orchestrator](./images/copilot24.png)

Dovresti vedere questo. Fare clic su **Visualizza dati**.

![Agent Orchestrator](./images/copilot25.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/copilot26.png)

## 1.1.3.5 Identificare Percorsi Fibre Esistenti

**Intento**

Scopri quali percorsi attivi o conclusi di recente includono &quot;Fibre&quot; nel titolo, ad esempio &quot;Fibre Upgrade NYC - Sept&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/copilot28.png)

Dovresti quindi visualizzare un elenco di percorsi.

![Agent Orchestrator](./images/copilot29.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/copilot31.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/copilot33.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/copilot35.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/copilot36.png)

## 1.1.3.6 Convalidare le prestazioni del percorso tramite analisi dell&#39;abbandono

**Intento**

Desideri comprendere l’abbandono delle prestazioni del percorso per sapere se nel percorso sono presenti nodi o condizioni che riscontrano una grande percentuale di profili eliminati. Questo è utile per capire se sono necessari ulteriori aggiustamenti nel percorso.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/copilot37.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/copilot38.png)

Scorri verso il basso ancora un po’ per vedere le osservazioni e i consigli. Fai clic sui tre punti **...**, quindi seleziona **Dettagli Percorso** per aprire il percorso specifico in Adobe Journey Optimizer.

![Agent Orchestrator](./images/copilot40.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/copilot41.png)

Ora hai completato il laboratorio.

Torna a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}