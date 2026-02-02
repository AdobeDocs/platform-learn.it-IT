---
title: CJA e ChatGPT con server MCP
description: CJA e ChatGPT con server MCP
kt: 5342
doc-type: tutorial
source-git-commit: b8906d1995dcb470789be2a1297eb48cb7690a9c
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# 1.5.1 CJA e ChatGPT con server MCP

[!BADGE Alpha]

+++Dettagli di Alpha
Utilizzando CJA &amp; Claude.ai con il server MCP Alpha, l&#39;utente riconosce che l&#39;Alpha viene fornito &quot;così com&#39;è&quot; senza alcuna garanzia di alcun tipo. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Alpha. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Alpha e/o dei materiali di accompagnamento. Alpha è considerata un&#39;informazione riservata di Adobe. Qualsiasi &quot;Feedback&quot; (informazioni relative ad Alpha inclusi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Alpha, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

+++

>[!NOTE]
>
>Questo esercizio sulla configurazione e l&#39;utilizzo di un server MCP con ChatGPT per la connessione a CJA è correlato a questo esercizio [1.1 Customer Journey Analytics: Creare una dashboard utilizzando Analysis Workspace sopra Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). La visualizzazione dati e la connessione di CJA utilizzate nell&#39;esercizio seguente sono la visualizzazione dati e la connessione configurate in tale esercizio. Se desideri replicare i risultati seguenti, segui prima queste istruzioni.

## Video

Questo video illustra e illustra tutti i passaggi di questo esercizio.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 Creazione di un&#39;app personalizzata in ChatGPT per CJA

>[!NOTE]
>
>L’utilizzo di CJA in ChatGPT richiede quanto segue:
>- una versione a pagamento di OpenAI&#39;s ChatGPT
>- utilizzo del client web ChatGPT

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

- **Nome**: `CJA`
- **URL server MCP**: verifica con il tuo rappresentante Adobe
- **Autenticazione**: `OAuth`

Seleziona la casella di controllo per **Ho capito e voglio continuare**.

Fai clic su **Crea**.

![ChatGPT](./images/chatgpt6.png)

Dopo aver effettuato l’accesso, dovresti notare che l’app CJA è ora connessa correttamente.

![ChatGPT](./images/chatgpt8.png)

## 1.5.1.2 Imposta contesto in CJA

Chiudi questa finestra.

![ChatGPT e CJA](./images/chatgpt9.png)

Dovresti vedere questo. Fai clic sull&#39;icona **+**, passa a **Altro** e seleziona **CJA**.

![ChatGPT e CJA](./images/chatgpt10.png)

Prima di interagire ulteriormente con CJA tramite ChatGPT, è necessario impostare il contesto.

Per questo esercizio, il contesto deve essere impostato per utilizzare:

- **Visualizzazione dati**: **—aepUserLdap— - Visualizzazione dati omni-channel**

L’impostazione Visualizzazione dati consente di identificare la visualizzazione dati che ChatGPT deve esaminare quando pone domande.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
list dataviews
```

![ChatGPT e CJA](./images/chatgpt11.png)

Dovresti quindi visualizzare un elenco simile delle visualizzazioni dati disponibili.

![ChatGPT e CJA](./images/chatgpt11a.png)

Per modificare la visualizzazione dati da utilizzare, immetti il seguente **Prompt** e fai clic sul pulsante **send**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![ChatGPT e CJA](./images/chatgpt12.png)

Dovresti vedere questo.

![ChatGPT e CJA](./images/chatgpt16.png)

Il contesto è ora impostato correttamente, quindi puoi iniziare a inviare successivamente richieste specifiche.

## 1.5.1.3 Esplora la visualizzazione dati

>[!NOTE]
>
>La visualizzazione dati utilizzata è stata impostata nell&#39;ambito dell&#39;esercizio [Creare una visualizzazione dati](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Immetti il seguente **Prompt** e fai clic sul pulsante **invia** per scoprire quali metriche e dimensioni sono disponibili.

```javascript
list the available metrics and dimensions
```

![ChatGPT e CJA](./images/chatgpt101.png)

Dovresti quindi visualizzare questa risposta, che include le metriche e le dimensioni configurate come parte dell&#39;esercizio [Crea una visualizzazione dati](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![ChatGPT e CJA](./images/chatgpt102.png)

## Tabella a forma libera 1.5.1.4 - Visualizzazioni prodotto

Ora puoi iniziare a esplorare i dati. Inizia immettendo il seguente prompt e fai clic su **invia** per inviare la richiesta di report.

```javascript
how many product views happened on January 21?
```

![ChatGPT e CJA](./images/chatgpt103.png)

Selezionare **RunReport**.

![ChatGPT e CJA](./images/chatgpt104.png)

Dovresti vedere una risposta come questa.

![ChatGPT e CJA](./images/chatgpt105.png)

Ora puoi suddividere la risposta aggiungendo una dimensione. Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
break down product views by product name
```

![ChatGPT e CJA](./images/chatgpt106.png)

Dovresti vedere una risposta come questa.

![ChatGPT e CJA](./images/chatgpt107.png)

Ora puoi anche creare una visualizzazione. Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
create a line visualization by hour for product views on January 21
```

![ChatGPT e CJA](./images/chatgpt108.png)

Selezionare **UpsertProject**.

![ChatGPT e CJA](./images/chatgpt109.png)

Selezionare **RunReport**.

![ChatGPT e CJA](./images/chatgpt110.png)

Dovresti vedere questo.

![ChatGPT e CJA](./images/chatgpt111.png)

Scorri verso il basso.

![ChatGPT e CJA](./images/chatgpt112.png)

Ora puoi anche scaricare questo grafico a linee. Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
export this chart to PNG
```

![ChatGPT e CJA](./images/chatgpt113.png)

Dovresti vedere questo. Fai clic su **Scarica PNG**.

![ChatGPT e CJA](./images/chatgpt114.png)

Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
can you breakdown product views by user agent?
```

![ChatGPT e CJA](./images/chatgpt115.png)

Selezionare **RunReport**.

![ChatGPT e CJA](./images/chatgpt116.png)

Dovresti vedere questo.

![ChatGPT e CJA](./images/chatgpt117.png)

## Visualizzazione Abbandono 1.5.1.5

Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![ChatGPT e CJA](./images/chatgpt118.png)

Selezionare **UpsertProject**.

![ChatGPT e CJA](./images/chatgpt119.png)

Selezionare **RunReport**.

![ChatGPT e CJA](./images/chatgpt120.png)

Dovresti vedere qualcosa del genere. Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
can you show me a visualization of the above fallout analysis?
```

![ChatGPT e CJA](./images/chatgpt120a.png)

Fai clic su **Scarica PNG**.

![ChatGPT e CJA](./images/chatgpt121.png)

Ora puoi vedere la visualizzazione dell’analisi dell’abbandono.

![ChatGPT e CJA](./images/chatgpt122.png)

Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
break down the fallout analysis at the touchpoint of the add to carts
```

![ChatGPT e CJA](./images/chatgpt123.png)

Selezionare **RunReport**.

![ChatGPT e CJA](./images/chatgpt124.png)

Torna a [Analytics e agenti](./analyticsagents.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}