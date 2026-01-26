---
title: Adobe Marketing Agent per ChatGPT Enterprise
description: Adobe Marketing Agent per ChatGPT Enterprise
kt: 5342
doc-type: tutorial
source-git-commit: 44d0e98ae4c7568411cb0e01ed8eff38b4a34137
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# 1.1.2 Adobe Marketing Agent per ChatGPT Enterprise

>[!IMPORTANT]
>
>Questa esercitazione utilizza una funzione che non è ancora stata rilasciata. La funzione è ancora in fase di sviluppo e quindi non è ancora disponibile a livello generale.

[!BADGE In Sviluppo]

+++Nei dettagli di sviluppo
Utilizzando Adobe Marketing Agent per ChatGPT Enterprise Beta, l&#39;utente riconosce che il Beta viene fornito &quot;così com&#39;è&quot; senza alcuna garanzia di alcun tipo. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Beta. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Beta e/o dei materiali di accompagnamento. Beta è considerata un&#39;informazione riservata di Adobe.  Qualsiasi &quot;Feedback&quot; (informazioni relative a Beta, compresi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

+++

## Video

Questo video illustra e illustra tutti i passaggi di questo esercizio.

>[!VIDEO](https://video.tv.adobe.com/v/3478410?quality=12&learn=on)

## 1.1.2.1 Creazione di un&#39;app personalizzata in ChatGPT Enterprise per Adobe Marketing Agent

>[!NOTE]
>
>L’utilizzo di Adobe Marketing Agent in ChatGPT richiede quanto segue:
>- una versione a pagamento di OpenAI ChatGPT Enterprise
>- utilizzo del client Web ChatGPT Enterprise

Vai a [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} e accedi utilizzando i dettagli del tuo account. Una volta effettuato l’accesso, dovresti visualizzarlo. Fai clic sul nome utente.

![ChatGPT](./images/chatgpt1.png)

Seleziona **Impostazioni**.

![ChatGPT](./images/chatgpt2.png)

Vai a **App** e seleziona **Impostazioni avanzate**.

![ChatGPT](./images/chatgpt3.png)

Attiva **Modalità sviluppatore**, quindi fai clic su **Indietro**.

![ChatGPT](./images/chatgpt4.png)

Fai clic su **Crea app**.

![ChatGPT](./images/chatgpt5.png)

Compila i campi in questo modo:

- **Nome**: `Adobe Marketing Agent`
- **URL server MCP**: verifica con il tuo rappresentante Adobe
- **Autenticazione**: `OAuth`

Seleziona la casella di controllo per **Ho capito e voglio continuare**.

Fai clic su **Crea**.

![ChatGPT](./images/chatgpt6.png)

ChatGPT tenterà ora di connettersi al tuo account Adobe. Seleziona **Consenti accesso**, quindi dovrai accedere con il tuo account Adobe.

![ChatGPT](./images/chatgpt7.png)

Dopo aver effettuato l’accesso, dovresti notare che il tuo Adobe Marketing Agent è ora connesso correttamente.

![ChatGPT](./images/chatgpt8.png)

## 1.1.2.2 Imposta contesto in Adobe Marketing Agent

Chiudi questa finestra.

![Agent Orchestrator](./images/chatgpt9.png)

Dovresti vedere questo. Fai clic sull&#39;icona **+**, passa a **Altro** e seleziona **Adobe Marketing Agent**.

![Agent Orchestrator](./images/chatgpt10.png)

Prima di interagire ulteriormente con Adobe Marketing Agent tramite ChatGPT, è necessario impostare il contesto.

Per questo esercizio, il contesto deve essere impostato per utilizzare:

- **Sandbox**: **Prod - Accelerate (VA7)**

L’impostazione Sandbox consente di identificare quale sandbox ChatGPT deve esaminare quando si pongono domande.

- **Visualizzazione dati**: **Accelerare il B2C del 2026**

L’impostazione Visualizzazione dati consente di identificare la visualizzazione dati che ChatGPT deve esaminare quando pone domande.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
list sandboxes
```

![Agent Orchestrator](./images/chatgpt11.png)

Dovresti quindi visualizzare un elenco simile delle sandbox disponibili. La sandbox corrente in questo esempio è impostata su **prod**.

Per modificare la sandbox da utilizzare, immetti il seguente **Prompt** e fai clic sul pulsante **send**.

```javascript
switch to sandbox accelerate
```

![Agent Orchestrator](./images/chatgpt12.png)

Dovresti vedere questo. Fare clic su **Imposta contesto**.

![Agent Orchestrator](./images/chatgpt13.png)

Dovresti vedere questo. Immetti il seguente **Prompt** e fai clic sul pulsante **invia** per impostare la visualizzazione dati da utilizzare.

```javascript
list dataviews
```

![Agent Orchestrator](./images/chatgpt14.png)

Dovresti quindi visualizzare un elenco simile delle visualizzazioni dati disponibili.

Per impostare la visualizzazione dati da utilizzare, immetti il seguente **Prompt** e fai clic sul pulsante **send**.

```javascript
switch to Accelerate 2026 B2C
```

![Agent Orchestrator](./images/chatgpt15.png)

Dovresti vedere questo. Fare clic su **Imposta contesto**.

![Agent Orchestrator](./images/chatgpt16.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/chatgpt17.png)

Il contesto è ora impostato correttamente, quindi puoi iniziare a inviare richieste specifiche successivamente.

## 1.1.2.3 Inizia con le tendenze generali di acquisto per ancorare il contesto e ingrandire la visualizzazione della fibra

**Intento**

Ottieni un impulso a livello di toplevel sulla domanda di categoria: mobile, rete fissa, Internet, TV, fibra ottica, in particolare per gli ultimi 60 giorni. Questo stabilisce le linee di base per la stagionalità, gli effetti promozionali e la varianza regionale dopo il rollout di New York.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/chatgpt18.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/chatgpt19.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/chatgpt20.png)

Dovresti vedere questo, che approfondisce le tendenze specifiche della fibra.

![Agent Orchestrator](./images/chatgpt21.png)

## 1.1.2.4 Correlazione degli ordini con le preferenze del contenuto

**Intento**

Testare l&#39;ipotesi che una preferenza per un genere specifico (ad esempio, SciFi, Sport, Drammatico) preveda il comportamento di aggiornamento della banda larga, in particolare per le esigenze di larghezza di banda elevata.

Innanzitutto, devi scoprire quale campo viene utilizzato per memorizzare la preferenza di genere.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which field is used to store the preferred genre in the sandbox accelerate?
```

![Agent Orchestrator](./images/chatgpt22.png)

Dovresti visualizzarlo, il che mostra che il campo utilizzato per il genere è **_experienceplatform.individualCharacteristics.preferences.preferredGenre**.

![Agent Orchestrator](./images/chatgpt23.png)

Con tali informazioni, puoi iniziare a espandere i dati di acquisto.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/chatgpt24.png)

Dovresti vedere questo. Fai clic su **Ricerche**.

![Agent Orchestrator](./images/chatgpt25.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/chatgpt26.png)

Scorri verso il basso per visualizzare ulteriori informazioni.

![Agent Orchestrator](./images/chatgpt27.png)

## 1.1.2.5 Identificare Percorsi Fibre Esistenti

**Intento**

Scopri quali percorsi attivi o conclusi di recente includono &quot;Fibre&quot; nel titolo, ad esempio &quot;Fibre Upgrade NYC - Sept&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/chatgpt28.png)

Dovresti vedere questo. Fai clic su **Ricerche**.

![Agent Orchestrator](./images/chatgpt29.png)

Dovresti quindi visualizzare un elenco di percorsi.

![Agent Orchestrator](./images/chatgpt30.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/chatgpt31.png)

Dovresti vedere questo. Fai clic su **Ricerche**.

![Agent Orchestrator](./images/chatgpt32.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/chatgpt33.png)

Scorri verso il basso per visualizzare ulteriori dettagli.

![Agent Orchestrator](./images/chatgpt34.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
show me the details of the journey 'CitiSignal - Fiber Max Launch Promotion'
```

![Agent Orchestrator](./images/chatgpt35.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/chatgpt36.png)

## 1.1.2.6 Convalidare le prestazioni del percorso tramite analisi dell&#39;abbandono

**Intento**

Desideri comprendere l’abbandono delle prestazioni del percorso per sapere se nel percorso sono presenti nodi o condizioni che riscontrano una grande percentuale di profili eliminati. Questo è utile per capire se sono necessari ulteriori aggiustamenti nel percorso.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/chatgpt37.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/chatgpt38.png)

Scorri verso il basso un po&#39;. È ora possibile rivedere la tabella esaminando ogni nodo e i rispettivi numeri di immissione, numeri di abbandono e tasso di abbandono.

![Agent Orchestrator](./images/chatgpt39.png)

Scorri verso il basso ancora un po’ per vedere le osservazioni e i consigli.

![Agent Orchestrator](./images/chatgpt40.png)

Ora hai completato il laboratorio.

Torna a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}