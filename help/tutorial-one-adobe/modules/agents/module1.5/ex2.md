---
title: CJA e Claude.ai con server MCP
description: CJA e Claude.ai con server MCP
kt: 5342
doc-type: tutorial
source-git-commit: b8906d1995dcb470789be2a1297eb48cb7690a9c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# 1.5.2 CJA e Claude.ai con server MCP

[!BADGE Alpha]

+++Dettagli di Alpha
Utilizzando CJA &amp; Claude.ai con il server MCP Alpha, l&#39;utente riconosce che l&#39;Alpha viene fornito &quot;così com&#39;è&quot; senza alcuna garanzia di alcun tipo. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Alpha. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Alpha e/o dei materiali di accompagnamento. Alpha è considerata un&#39;informazione riservata di Adobe. Qualsiasi &quot;Feedback&quot; (informazioni relative ad Alpha inclusi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Alpha, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

+++


>[!NOTE]
>
>Questo esercizio sulla configurazione e l&#39;utilizzo di un server MCP con Claude.ai per la connessione a CJA è correlato a questo esercizio [1.1 Customer Journey Analytics: Creare un dashboard utilizzando Analysis Workspace su Adobe Experience Platform](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md). La visualizzazione dati e la connessione di CJA utilizzate nell&#39;esercizio seguente sono la visualizzazione dati e la connessione configurate in tale esercizio. Se desideri replicare i risultati seguenti, segui prima queste istruzioni.

## Video

Questo video illustra e illustra tutti i passaggi di questo esercizio.

>[!VIDEO](https://video.tv.adobe.com/v/3479159?quality=12&learn=on)

## 1.5.1.1 Creazione di un&#39;app personalizzata in Claude.ai per CJA

>[!NOTE]
>
>L’utilizzo di CJA in Claude.ai richiede quanto segue:
>- una versione a pagamento di Claude.ai
>- utilizzo del client web Claude.ai

Vai a [https://claude.ai/](https://claude.ai/){target="_blank"} e accedi utilizzando i dettagli del tuo account. Una volta effettuato l’accesso, dovresti visualizzarlo. Fai clic sull&#39;icona **+**.

![Claude.ai](./images/claude1.png)

Seleziona **Aggiungi connettori**.

![Claude.ai](./images/claude2.png)

Fai clic su **aggiungi un elemento personalizzato**.

![Claude.ai](./images/claude3.png)

Compila i campi in questo modo:

- **Nome**: `CJA`
- **URL server MCP**: verifica con il tuo rappresentante Adobe

Fai clic su **Aggiungi**.

![Claude.ai](./images/claude4.png)

Dovresti vedere questo. Fai clic su **Aggiungi**.

![Claude.ai](./images/claude5.png)

Una volta autenticato correttamente, dovresti visualizzarlo. Fai clic sull&#39;icona **+** per avviare una nuova chat.

![Claude.ai](./images/claude6.png)

Vai a **+**, a **Connettori** e dovresti notare che il connettore **CJA** è ora abilitato.

![Claude.ai](./images/claude8.png)

Ora puoi iniziare l’analisi dei dati.

![Claude.ai](./images/claude7.png)


## 1.5.1.2 Imposta contesto in CJA

Prima di interagire ulteriormente con CJA tramite Claude.ai, è necessario impostare il contesto.

Per questo esercizio, il contesto deve essere impostato per utilizzare:

- **Visualizzazione dati**: **—aepUserLdap— - Visualizzazione dati omni-channel**

L’impostazione Visualizzazione dati consente di identificare quale visualizzazione dati deve essere considerata da Claude.ai quando si pongono domande.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
list dataviews
```

![Claude.ai e CJA](./images/claude9.png)

Seleziona **Consenti sempre**.

![Claude.ai e CJA](./images/claude10.png)

Dovresti quindi visualizzare un elenco simile delle visualizzazioni dati disponibili.

![Claude.ai e CJA](./images/claude11.png)

Per modificare la visualizzazione dati da utilizzare, immetti il seguente **Prompt** e fai clic sul pulsante **send**.

```javascript
switch to dataview --aepUserLdap-- - Omnichannel Data View
```

![Claude.ai e CJA](./images/claude11a.png)

Seleziona **Consenti sempre**.

![Claude.ai e CJA](./images/claude12.png)

Dovresti vedere questo.

![Claude.ai e CJA](./images/claude16.png)

Il contesto è ora impostato correttamente, quindi puoi iniziare a inviare successivamente richieste specifiche.

## 1.5.1.3 Esplora la visualizzazione dati

>[!NOTE]
>
>La visualizzazione dati utilizzata è stata impostata nell&#39;ambito dell&#39;esercizio [Creare una visualizzazione dati](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

Immetti il seguente **Prompt** e fai clic sul pulsante **invia** per scoprire quali metriche e dimensioni sono disponibili.

```javascript
list the available metrics and dimensions
```

![Claude.ai e CJA](./images/claude101.png)

Seleziona **Consenti sempre** due volte, una volta per recuperare **metriche** e una seconda volta per recuperare **dimensioni**.

![Claude.ai e CJA](./images/claude101a.png)

Dovresti quindi visualizzare questa risposta, che include le metriche e le dimensioni configurate come parte dell&#39;esercizio [Crea una visualizzazione dati](./../../../modules/reporting-insights/cja-b2c/cjab2c-1/ex3.md).

![Claude.ai e CJA](./images/claude102.png)

## Tabella a forma libera 1.5.1.4 - Visualizzazioni prodotto

Ora puoi iniziare a esplorare i dati. Inizia immettendo il seguente prompt e fai clic su **invia** per inviare la richiesta di report.

```javascript
how many product views happened on January 21, 2026?
```

![Claude.ai e CJA](./images/claude103.png)

Seleziona **Consenti sempre**.

![Claude.ai e CJA](./images/claude104.png)

Dovresti vedere una risposta come questa.

![Claude.ai e CJA](./images/claude105.png)

Ora puoi suddividere la risposta aggiungendo una dimensione. Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
break down product views by product name
```

![Claude.ai e CJA](./images/claude106.png)

Dovresti vedere una risposta come questa.

![Claude.ai e CJA](./images/claude107.png)

Ora puoi anche creare una visualizzazione. Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
create a line visualization by hour for product views on January 21
```

![Claude.ai e CJA](./images/claude108.png)

Dovresti vedere questo.

![Claude.ai e CJA](./images/claude109.png)

Ora puoi anche scaricare questo grafico a linee. Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
export this chart to PNG
```

![Claude.ai e CJA](./images/claude113.png)

Dovresti vedere questo. Fai clic su **Scarica**.

![Claude.ai e CJA](./images/claude114.png)

È quindi possibile aprire il file PNG scaricato e utilizzarlo in altri documenti.

![Claude.ai e CJA](./images/claude114a.png)

Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
can you breakdown product views by user agent?
```

![Claude.ai e CJA](./images/claude115.png)

Dovresti vedere questo.

![Claude.ai e CJA](./images/claude117.png)

## Visualizzazione Abbandono 1.5.1.5

Immetti il seguente **prompt** e fai clic sul pulsante **invia**.

```javascript
can you create a fallout visualization for the product interaction funnel, starting with all traffic and then in the next steps add Product Views, Add to Cart and purchases?
```

![Claude.ai e CJA](./images/claude118.png)

Dovresti quindi vedere qualcosa di simile, che include una visualizzazione generata da Claude.ai basata sui dati forniti da Customer Journey Analytics.

![Claude.ai e CJA](./images/claude119.png)

Torna a [Analytics e agenti](./analyticsagents.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}