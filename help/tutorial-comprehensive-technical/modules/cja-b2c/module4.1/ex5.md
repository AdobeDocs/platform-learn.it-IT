---
title: 'Customer Journey Analytics: visualizzazione tramite Customer Journey Analytics'
description: 'Customer Journey Analytics: visualizzazione tramite Customer Journey Analytics'
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# 4.1.5 Visualizzazione tramite Customer Journey Analytics

## Obiettivi

- Interfaccia utente di Analysis Workspace
- Scopri alcune funzioni che rendono Analysis Workspace così diverso.
- Scopri come analizzare in CJA utilizzando Analysis Workspace

## Contesto

In questi esercizi utilizzerai Analysis Workspace all’interno di CJA per analizzare le visualizzazioni dei prodotti, i funnel di prodotto, l’abbandono, ecc.

Copriremo alcune delle query eseguite nel Modulo 7 - Query Service in modo da vedere quanto è facile eseguire le stesse query e altro ancora, ma senza utilizzare SQL e affidandosi solo alla filosofia di trascinamento della selezione di Analysis Workspace.

Utilizziamo il progetto creato in [11.4 Data Preparation in Analysis Workspace](./ex4.md), quindi passa a [https://analytics.adobe.com](https://analytics.adobe.com).

![demo](./images/prohome.png)

Apri il progetto `--demoProfileLdap-- - Omnichannel Analysis`.

Con il progetto aperto e la visualizzazione dati `--demoProfileLdap-- - Omnichannel Analysis` selezionata, puoi iniziare a creare le prime visualizzazioni.

![demo](./images/prodataView1.png)

## Quante visualizzazioni di prodotto abbiamo su base giornaliera

Prima di tutto, dobbiamo selezionare le date giuste per analizzare i dati. Vai al menu a discesa del calendario sul lato destro dell’area di lavoro. Fai clic su di esso e seleziona l’intervallo di date applicabile.

![demo](./images/pro1.png)

Nel menu a sinistra (area componenti), individua la metrica calcolata **Visualizzazioni prodotto**. Selezionala e trascinala nell’area di lavoro, in alto a destra all’interno della tabella a forma libera.

![demo](./images/pro2.png)

Automaticamente la dimensione **Day** verrà aggiunta per creare la prima tabella. Ora puoi vedere la tua domanda rispondere al volo.

![demo](./images/pro3.png)

Quindi, fai clic con il pulsante destro del mouse sul riepilogo delle metriche.

![demo](./images/pro4.png)

Fai clic su **Visualizza**, quindi seleziona **Riga** come visualizzazione.

![demo](./images/pro5.png)

Visualizzerai le visualizzazioni dei prodotti per giorno.

![demo](./images/pro6.png)

Puoi cambiare l&#39;ambito orario in giorno facendo clic su **Impostazioni** all&#39;interno della visualizzazione.

![demo](./images/pro7.png)

Fai clic sul punto accanto a **Riga** per **Gestire Data Source**.

![demo](./images/pro7a.png)

Quindi, fai clic su **Blocca selezione** e seleziona **Elementi selezionati** per bloccare questa visualizzazione in modo che visualizzi sempre una timeline di Visualizzazioni prodotto.

![demo](./images/pro7b.png)

## Primi 5 prodotti visualizzati

Quali sono i primi 5 prodotti visualizzati?

Ricorda di salvare il progetto di tanto in tanto.

| Sistema operativo | Scelta rapida |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Comando+S |

Iniziamo a trovare i primi 5 prodotti visualizzati. Nel menu a sinistra, individua il **Nome prodotto** - Dimension.

![demo](./images/pro8.png)

Trascina e rilascia **Nome prodotto** per sostituire la dimensione **Giorno**:

Questo sarà il risultato

![demo](./images/pro10a.png)

Quindi, prova a suddividere uno dei prodotti per Marchio. Cerca **brandName** e trascinalo sotto il nome del primo prodotto.

![demo](./images/pro13.png)

Quindi, effettua un raggruppamento utilizzando l’agente utente. Cerca **Agente utente** e trascinalo con il nome del brand.

![demo](./images/pro15.png)

A questo punto viene visualizzato quanto segue:

![demo](./images/pro15a.png)

Infine, puoi aggiungere altre visualizzazioni. Sul lato sinistro, in Visualizzazioni, cerca `Donut`. Prendi `Donut` e trascinalo sull&#39;area di lavoro sotto la visualizzazione **Line**.

![demo](./images/pro18.png)

Quindi, nella tabella, seleziona le prime 5 **righe Agente utente** dal raggruppamento eseguito in **Smartphone nero Google Pixel XL da 32 GB** > **Segnale Citi**. Durante la selezione delle 3 righe, tenere premuto il pulsante **CTRL** (in Windows) o il pulsante **Comando** (in Mac).

![demo](./images/pro20.png)

Il grafico ad anello verrà modificato:

![demo](./images/pro21.png)

Puoi anche adattare la progettazione in modo da renderla più leggibile, riducendo leggermente sia il grafico **Line** che il grafico **Donut** in modo che possano adattarsi l&#39;uno accanto all&#39;altro:

![demo](./images/pro22.png)

Fai clic sul punto accanto a **Anello** per **Gestire Data Source**.
Quindi, fai clic su **Blocca selezione** per bloccare questa visualizzazione in modo che visualizzi sempre una timeline di Visualizzazioni prodotto.

![demo](./images/pro22b.png)

Ulteriori informazioni sulle visualizzazioni con Analysis Workspace disponibili qui:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funnel di interazione del prodotto, dalla visualizzazione all’acquisto

Ci sono molti modi per risolvere questa domanda. Una di queste consiste nell’utilizzare il tipo di interazione prodotto e utilizzarlo in una tabella a forma libera. Un altro modo consiste nell&#39;utilizzare una **Visualizzazione di fallout**. Usiamo l’ultimo dato che vogliamo visualizzare e analizzare allo stesso tempo.

Per chiudere il pannello corrente, fai clic qui:

![demo](./images/pro23.png)

Aggiungere ora un nuovo pannello vuoto facendo clic su **+ Aggiungi pannello vuoto**.

![demo](./images/pro24.png)

Fai clic sulla visualizzazione **Abbandono**.

![demo](./images/pro25.png)

Selezionare lo stesso intervallo di date dell&#39;esercizio precedente.

![demo](./images/prodatef.png)

Poi vedrai questo.

![demo](./images/prodatefa.png)

Trova la dimensione **Tipo evento** sotto i componenti sul lato sinistro:

![demo](./images/pro26.png)

Fare clic sulla freccia per aprire la dimensione:

![demo](./images/pro27.png)

Verranno visualizzati tutti i tipi di evento disponibili.

![demo](./images/pro28.png)

Seleziona l&#39;elemento **commerce.productViews** e trascinalo sul campo **Aggiungi punto di contatto** all&#39;interno della **Visualizzazione di abbandono**.

![demo](./images/pro29.png)

Fai lo stesso con **commerce.productListAdds** e **commerce.purchases** e rilasciali nel campo **Aggiungi punto di contatto** all&#39;interno della **Visualizzazione di fallout**. La visualizzazione sarà ora simile alla seguente:

![demo](./images/props1.png)

Puoi fare molte cose qui. Alcuni esempi: confronta nel tempo, confronta ogni passaggio per dispositivo o confronta per fedeltà. Tuttavia, se vogliamo analizzare aspetti interessanti come il motivo per cui i clienti non acquistano dopo aver aggiunto un articolo al carrello, possiamo utilizzare il migliore strumento in CJA: fai clic con il pulsante destro del mouse.

Fai clic con il pulsante destro del mouse sul punto di contatto **commerce.productListAdds**. Quindi fai clic su **Abbandono raggruppamento in questo punto di contatto**.

![demo](./images/pro32.png)

Verrà creata una nuova tabella a forma libera per analizzare le azioni intraprese dalle persone in caso di mancato acquisto.

![demo](./images/pro33.png)

Modificare **Tipo evento** in **Nome pagina** nella nuova tabella a forma libera per vedere quali pagine vanno invece della pagina di conferma dell&#39;acquisto.

![demo](./images/pro34.png)

## Cosa fanno le persone sul sito prima di raggiungere la pagina Annulla servizio?

Anche in questo caso, esistono diversi modi per eseguire questa analisi. Utilizziamo l&#39;analisi di flusso per avviare la parte di individuazione.

Per chiudere il pannello corrente, fai clic qui:

![demo](./images/pro0.png)

Aggiungere ora un nuovo pannello vuoto facendo clic su **+ Aggiungi pannello vuoto**.

![demo](./images/pro0a.png)

Fai clic sulla visualizzazione **Flusso**.

![demo](./images/pro35.png)

A questo punto viene visualizzato quanto segue:

![demo](./images/pro351.png)

Selezionare lo stesso intervallo di date dell&#39;esercizio precedente.

![demo](./images/pro0b.png)

Trova la dimensione **Nome pagina** sotto i componenti sul lato sinistro:

![demo](./images/pro36.png)

Fare clic sulla freccia per aprire la dimensione:

![demo](./images/pro37.png)

Troverai tutte le pagine visualizzate. Trovare il nome della pagina: **Annulla servizio**.
Trascina e rilascia **Annulla servizio** nella visualizzazione Flusso nel campo centrale:

![demo](./images/pro38.png)

A questo punto viene visualizzato quanto segue:

![demo](./images/pro40.png)

Analizziamo ora se i clienti che hanno visitato la pagina **Annulla servizio** del sito Web hanno chiamato anche il callcenter e qual è stato il risultato.

Nelle dimensioni, torna indietro e trova **Tipo di interazione chiamata**.
Trascina e rilascia **Tipo di interazione chiamata** per sostituire la prima interazione a destra nella **Visualizzazione flusso**.

![demo](./images/pro43.png)

Stai visualizzando il ticket di supporto dei clienti che hanno chiamato il call center dopo aver visitato la pagina **Annulla servizio**.

![demo](./images/pro44.png)

Quindi, nelle dimensioni, cerca **Sentimento chiamata**.  Trascinarlo e rilasciarlo per sostituire la prima interazione a destra nella **Visualizzazione flusso**.

![demo](./images/pro46.png)

A questo punto viene visualizzato quanto segue:

![demo](./images/flow.png)

Come puoi vedere, abbiamo eseguito un’analisi omnicanale utilizzando la Visualizzazione del flusso. Grazie a questo abbiamo trovato che sembra che alcuni clienti che stavano pensando di annullare il loro servizio, ha avuto un sentimento positivo dopo aver chiamato il call center. Forse abbiamo cambiato idea con una promozione?

## Quali sono le prestazioni dei clienti con un contatto del centro chiamate positivo rispetto ai KPI principali?

Segmentiamo innanzitutto i dati per ottenere solo gli utenti con **chiamate positive**. In CJA, i segmenti sono denominati Filtri. Vai ai filtri all&#39;interno dell&#39;area dei componenti (a sinistra) e fai clic su **+**.

![demo](./images/pro58.png)

All’interno del Generatore di filtri, assegna un nome al filtro

| Nome | Descrizione |
| ----------------- |-------------| 
| Sentimento di chiamata - Positivo | Sentimento di chiamata - Positivo |

![demo](./images/pro47.png)

Sotto i componenti (nel Generatore di filtri), trova **Sentimento chiamata** e trascinalo nella definizione del Generatore di filtri.

![demo](./images/pro48.png)

Ora seleziona **positivo** come valore per il filtro.

![demo](./images/pro49.png)

Modifica l&#39;ambito impostandolo al livello **Persona**.

![demo](./images/pro50.png)

Per terminare, fai clic su **Salva**.

![demo](./images/pro51.png)

Allora tornerai qui. Se non l’hai ancora fatto, chiudi il pannello precedente.

![demo](./images/pro0c.png)

Aggiungere ora un nuovo pannello vuoto facendo clic su **+ Aggiungi pannello vuoto**.

![demo](./images/pro24c.png)

Selezionare lo stesso intervallo di date dell&#39;esercizio precedente.

![demo](./images/pro24d.png)

Fai clic su **Tabella a forma libera**.

![demo](./images/pro52.png)

Trascina il filtro appena creato.

![demo](./images/pro53.png)

È ora di aggiungere alcune metriche. Inizia con **Visualizzazioni prodotto**. Trascina nella tabella a forma libera. Puoi anche eliminare la metrica **Eventi**.

![demo](./images/pro54.png)

Fai lo stesso con **Persone**, **Aggiungi al carrello** e **Acquisti**. Finirai con un tavolo come questo.

![demo](./images/pro55.png)

Grazie alla prima analisi di flusso, mi è venuta in mente una nuova domanda. Quindi abbiamo deciso di creare questa tabella e confrontare alcuni KPI con un segmento per rispondere a quella domanda. Come è possibile notare, il tempo necessario per ottenere informazioni approfondite è molto più veloce rispetto all&#39;utilizzo di SQL o di altre soluzioni BI.

## Riepilogo Customer Journey Analytics e Analysis Workspace

Come hai imparato in questo laboratorio, Analysis Workspace unisce i dati di tutti i canali per analizzare l’intero percorso di clienti. Inoltre, ricorda che puoi inserire dati nella stessa area di lavoro che non è unita al percorso.
Può essere molto utile inserire nell’analisi dati disconnessi per dare contesto al percorso. Alcuni esempi includono dati NPS, sondaggi, eventi Facebook Ads o interazioni offline (non identificate).

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 4.1](./customer-journey-analytics-build-a-dashboard.md)

[Torna a tutti i moduli](./../../../overview.md)
