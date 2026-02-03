---
title: Adobe Analytics e Claude.ai con server MCP
description: Adobe Analytics e Claude.ai con server MCP
kt: 5342
doc-type: tutorial
source-git-commit: 44559d6278da4bed8a864d0faf092352b8370398
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 1.5.3 Adobe Analytics e Claude.ai con server MCP

[!BADGE Alpha]

+++Dettagli di Alpha
Utilizzando CJA &amp; Claude.ai con il server MCP Alpha, l&#39;utente riconosce che l&#39;Alpha viene fornito &quot;così com&#39;è&quot; senza alcuna garanzia di alcun tipo. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Alpha. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Alpha e/o dei materiali di accompagnamento. Alpha è considerata un&#39;informazione riservata di Adobe. Qualsiasi &quot;Feedback&quot; (informazioni relative ad Alpha inclusi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Alpha, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

+++

## Video

Questo video illustra e illustra tutti i passaggi di questo esercizio.

>[!VIDEO](https://video.tv.adobe.com/v/3479562?quality=12&learn=on)

## 1.5.3.1 Creare un&#39;app personalizzata in Claude.ai per Adobe Analytics

>[!NOTE]
>
>L’utilizzo di Adobe Analytics in Claude.ai richiede quanto segue:
>- una versione a pagamento di Claude.ai
>- utilizzo del client web Claude.ai

Vai a [https://claude.ai/](https://claude.ai/){target="_blank"} e accedi utilizzando i dettagli del tuo account. Una volta effettuato l’accesso, dovresti visualizzarlo. Fai clic sull&#39;icona **+**.

![Claude.ai](./images/claudeaa1.png)

Seleziona **Aggiungi connettori**.

![Claude.ai](./images/claudeaa2.png)

Fai clic su **aggiungi un elemento personalizzato**.

![Claude.ai](./images/claudeaa3.png)

Compila i campi in questo modo:

- **Nome**: `CJA`
- **URL server MCP**: verifica con il tuo rappresentante Adobe

Fai clic su **Aggiungi**.

![Claude.ai](./images/claudeaa4.png)

Dovresti vedere questo. Fai clic su **Connetti**.

![Claude.ai](./images/claudeaa5.png)

Una volta autenticato correttamente, dovresti visualizzarlo. Fai clic sull&#39;icona **+** per avviare una nuova chat.

![Claude.ai](./images/claudeaa6.png)

Vai a **+**, a **Connettori** e dovresti notare che il connettore **Adobe Analytics** è ora abilitato.

![Claude.ai](./images/claudeaa7.png)

Ora puoi iniziare l’analisi dei dati.

![Claude.ai](./images/claudeaa8.png)

## 1.5.3.2 Imposta contesto in Adobe Analytics

Prima di interagire ulteriormente con CJA tramite Claude.ai, è necessario impostare il contesto.

Per questo esercizio, il contesto deve essere impostato per utilizzare:

- **Suite di rapporti**: **CID - Dati dimostrativi**

L’impostazione Report Suite consente di identificare quali dati Claude.ai devono essere considerati quando si pongono domande.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
list report suites
```

![Claude.ai](./images/claudeaa9.png)

Seleziona **Consenti sempre**.

![Claude.ai](./images/claudeaa10.png)

Seleziona **Consenti sempre**.

![Claude.ai](./images/claudeaa11.png)

Dovresti vedere qualcosa del genere.

![Claude.ai](./images/claudeaa12.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
use report suite CID Demo Data
```

![Claude.ai](./images/claudeaa13.png)

Seleziona **Consenti sempre**.

![Claude.ai](./images/claudeaa14.png)

La suite di rapporti è stata selezionata.

![Claude.ai](./images/claudeaa15.png)

## 1.5.2.3 Esplora la suite di rapporti

Immetti il seguente **Prompt** e fai clic sul pulsante **invia** per scoprire quali metriche e dimensioni sono disponibili.

```javascript
list the available metrics and dimensions
```

![Claude.ai e CJA](./images/claudeaa101.png)

Seleziona **Consenti sempre**.

![Claude.ai e CJA](./images/claudeaa102.png)

Seleziona di nuovo **Consenti sempre**.

![Claude.ai e CJA](./images/claudeaa103.png)

Dovresti quindi visualizzare questa risposta, che include le metriche e le dimensioni configurate in questa suite di rapporti.

![Claude.ai e CJA](./images/claudeaa104.png)

## 1.5.2.4 report

Ora puoi iniziare a esplorare i dati. Inizia immettendo il seguente prompt e fai clic su **invia** per inviare la richiesta di report.

```javascript
show me pageviews for Feb 2?
```

![Claude.ai e CJA](./images/claudeaa105.png)

Dovresti vedere qualcosa del genere.

![Claude.ai e CJA](./images/claudeaa106.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
break down pageviews by page name
```

![Claude.ai e CJA](./images/claudeaa107.png)

Dovresti vedere questo.

![Claude.ai e CJA](./images/claudeaa108.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
give me an overview of page names, page views by marketing channel
```

![Claude.ai e CJA](./images/claudeaa109.png)

Dovresti vedere qualcosa del genere.

![Claude.ai e CJA](./images/claudeaa110.png)

Scorri verso il basso un po&#39; per vedere l&#39;analisi.

![Claude.ai e CJA](./images/claudeaa111.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Analyze different metrics by marketing channel
```

![Claude.ai e CJA](./images/claudeaa112.png)

Dovresti vedere qualcosa del genere.

![Claude.ai e CJA](./images/claudeaa113.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
which tracking codes drove the most visits and purchases?
```

![Claude.ai e CJA](./images/claudeaa114.png)

Dovresti quindi vedere qualcosa di simile, mostrando prima **i codici di tracciamento principali per visite**.

![Claude.ai e CJA](./images/claudeaa115.png)

Puoi quindi visualizzare i codici di tracciamento che hanno determinato il maggior numero di acquisti nel rapporto **Codici di tracciamento principali per ordini (acquisti)**.

![Claude.ai e CJA](./images/claudeaa116.png)

E poi trovi ulteriori informazioni fornite da Claude.ai in base ai dati provenienti da Adobe Analytics.

![Claude.ai e CJA](./images/claudeaa117.png)

Hai terminato questo esercizio.

Torna a [Analytics e agenti](./analyticsagents.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}