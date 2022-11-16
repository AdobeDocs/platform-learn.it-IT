---
title: Bootcamp - Customer Journey Analytics - Visualizzazione con Customer Journey Analytics
description: Bootcamp - Customer Journey Analytics - Visualizzazione con Customer Journey Analytics
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 051b5b91-56c4-414e-a4c4-74aa67219551
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 1%

---

# 4.5 Visualizzazione con Customer Journey Analytics

## Obiettivi

- Interfaccia utente di Analysis Workspace
- Scopri alcune funzioni che rendono Analysis Workspace così diverso.
- Scopri come analizzare in CJA utilizzando Analysis Workspace

## Contesto

In questo esercizio utilizzerai Analysis Workspace all’interno di CJA per analizzare le visualizzazioni dei prodotti, i funnel dei prodotti, l’abbandono ecc.

Usiamo il progetto creato in [4.4 Preparazione dei dati in Analysis Workspace](./ex4.md)quindi vai a [https://analytics.adobe.com](https://analytics.adobe.com).

![demo](./images/prohome.png)

Apri il progetto `yourLastName - Omnichannel Analysis`.

Con il progetto aperto e la visualizzazione dati `yourLastName - Omnichannel Analysis` seleziona puoi iniziare a creare le tue prime visualizzazioni.

![demo](./images/prodataView1.png)

## Quante visualizzazioni di prodotto abbiamo quotidianamente?

Prima di tutto, dobbiamo selezionare le date giuste per analizzare i dati. Vai al menu a discesa Calendario sul lato destro dell’area di lavoro. Fai clic su di esso e seleziona l’intervallo di date applicabile.

>[!IMPORTANT]
>
>Seleziona un intervallo di date come **Questa settimana** o **Questo mese**. I dati più recenti disponibili sono stati acquisiti il 19 settembre 2022.

![demo](./images/pro1.png)

Nel menu a sinistra (area componenti), trova la metrica calcolata **Visualizzazioni prodotto**. Selezionala e trascinala nell’area di lavoro, in alto a destra all’interno della tabella a forma libera.

![demo](./images/pro2.png)

Automaticamente la dimensione **Giorno** verrà aggiunto per creare la prima tabella. Ora potete vedere la risposta immediata alla vostra domanda.

![demo](./images/pro3.png)

Fai clic con il pulsante destro del mouse sul riepilogo della metrica.

![demo](./images/pro4.png)

Fai clic su **Visualizza** quindi seleziona **Linea** come visualizzazione.

![demo](./images/pro5.png)

Visualizzerai le visualizzazioni dei tuoi prodotti per giorno.

![demo](./images/pro6.png)

Puoi cambiare l’ambito dell’ora in giorno facendo clic su **Impostazioni** all’interno della visualizzazione.

![demo](./images/pro7.png)

Fai clic sul punto accanto a **Linea** a **Gestione dell&#39;origine dati**.

![demo](./images/pro7a.png)

Quindi, fai clic su **Blocca selezione** e seleziona **Elementi selezionati** per bloccare questa visualizzazione in modo che visualizzi sempre una timeline di Visualizzazioni prodotto .

![demo](./images/pro7b.png)

## Primi 5 prodotti visualizzati

Quali sono i primi 5 prodotti visualizzati?

Ricorda di salvare il progetto ogni tanto.

| Sistema operativo | Taglio corto |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Comando+S |

Cominciamo a trovare i primi 5 prodotti visualizzati. Nel menu a sinistra, trova la **Nome del prodotto** - Dimension.

![demo](./images/pro8.png)

Ora trascina e rilascia **Nome del prodotto** per sostituire **Giorno** dimensione:

Questo sarà il risultato

![demo](./images/pro10a.png)

Quindi, prova a suddividere uno dei prodotti in base al nome del marchio. Cerca **brandName** e trascinarlo sotto il nome del prodotto.

![demo](./images/pro13.png)

Quindi, eseguire un raggruppamento utilizzando l&#39;agente utente. Cerca **Agente utente** e trascinarlo sotto il nome del marchio.

![demo](./images/pro15.png)

Vedrai questo:

![demo](./images/pro15a.png)

Infine puoi aggiungere altre visualizzazioni. Sul lato sinistro, in visualizzazioni, cerca `Donut`. Prendi `Donut`, trascinalo sull’area di lavoro sotto la **Linea** visualizzazione.

![demo](./images/pro18.png)

Quindi, nella tabella, selezionare il primo 5 **Agente utente**  righe dal raggruppamento che abbiamo fatto in **Smartphone nero Google Pixel XL da 32 GB** > **Segnale Citi**. Quando selezioni le 5 righe, tieni premuto il pulsante **CTRL** su Windows o **Comando** (su Mac).

![demo](./images/pro20.png)

Il grafico ad anello è stato modificato:

![demo](./images/pro21.png)

È anche possibile adattare il design per essere più leggibile, rendendo entrambi **Linea** grafico e **Anello** grafico un po&#39; più piccolo in modo che possano adattarsi l&#39;uno accanto all&#39;altro:

![demo](./images/pro22.png)

Fai clic sul punto accanto a **Anello** a **Gestione dell&#39;origine dati**.
Quindi, fai clic su **Blocca selezione** per bloccare questa visualizzazione in modo che visualizzi sempre una timeline di Visualizzazioni prodotto .

![demo](./images/pro22b.png)

Puoi trovare ulteriori informazioni sulle visualizzazioni con Analysis Workspace qui:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=it](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=it)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funnel di interazione del prodotto, dalla visualizzazione all&#39;acquisto

Ci sono molti modi per risolvere questa domanda. Uno di questi è quello di utilizzare il tipo di interazione prodotto e utilizzarlo su una tabella a forma libera. Un altro modo è quello di utilizzare un **Visualizzazione Abbandono**. Usiamo l&#39;ultima come vogliamo visualizzare e analizzare contemporaneamente.

Per chiudere il pannello corrente, fai clic qui:

![demo](./images/pro23.png)

Ora aggiungi un nuovo pannello vuoto facendo clic su **+ Aggiungi pannello vuoto**.

![demo](./images/pro24.png)

Fai clic sulla visualizzazione **Abbandono**.

![demo](./images/pro25.png)

Seleziona lo stesso intervallo di date dell’esercizio precedente.

![demo](./images/prodatef.png)

Vedrete questo.

![demo](./images/prodatefa.png)

Trova la dimensione **Tipo evento** sotto i componenti sul lato sinistro:

![demo](./images/pro26.png)

Fai clic sulla freccia per aprire la dimensione:

![demo](./images/pro27.png)

Verranno visualizzati tutti i tipi di evento disponibili.

![demo](./images/pro28.png)

Seleziona l’elemento **commerce.productViews** e trascinarlo nella **Aggiungi punto di contatto** all&#39;interno del campo **Visualizzazione Abbandono**.

![demo](./images/pro29.png)

Fai lo stesso con **commerce.productListAdd** e **commerce.purchase** e rilasciarli sul **Aggiungi punto di contatto** all&#39;interno del campo **Visualizzazione Abbandono**. La visualizzazione si presenterà così:

![demo](./images/props1.png)

Puoi fare molte cose qui. Alcuni esempi: confronta nel tempo, confronta ogni passaggio per dispositivo o confronta per fedeltà. Tuttavia, se vogliamo analizzare cose interessanti come il motivo per cui i clienti non acquistano dopo aver aggiunto un articolo al carrello, possiamo utilizzare lo strumento migliore in CJA: fare clic con il pulsante destro del mouse.

Fai clic con il pulsante destro del mouse sul punto di contatto **commerce.productListAdd**. Quindi fai clic su **Abbandono suddiviso in questo punto di contatto**.

![demo](./images/pro32.png)

Verrà creata una nuova tabella a forma libera per analizzare ciò che le persone hanno fatto se non hanno acquistato.

![demo](./images/pro33.png)

Modificare la **Tipo evento** da **Nome pagina**, nella nuova tabella a forma libera, per vedere quali pagine stanno andando invece della pagina di conferma di acquisto .

![demo](./images/pro34.png)

## Cosa fanno le persone sul sito prima di raggiungere la pagina Annulla servizio?

Anche in questo caso, esistono molti modi per eseguire questa analisi. Usiamo l&#39;analisi di flusso per avviare la parte di individuazione.

Per chiudere il pannello corrente, fai clic qui:

![demo](./images/pro0.png)

Ora aggiungi un nuovo pannello vuoto facendo clic su **+ Aggiungi pannello vuoto**.

![demo](./images/pro0a.png)

Fai clic sulla visualizzazione **Flusso**.

![demo](./images/pro35.png)

Vedrai questo:

![demo](./images/pro351.png)

Seleziona lo stesso intervallo di date dell’esercizio precedente.

![demo](./images/pro0b.png)

Trova la dimensione **Nome pagina** sotto i componenti sul lato sinistro:

![demo](./images/pro36.png)

Fai clic sulla freccia per aprire la dimensione:

![demo](./images/pro37.png)

Troverete tutte le pagine visualizzate. Trova il nome della pagina: **Annulla servizio**.
Trascinamento della selezione **Annulla servizio** nella Visualizzazione Flusso nel campo centrale:

![demo](./images/pro38.png)

Vedrai questo:

![demo](./images/pro40.png)

Ora esaminiamo se i clienti che hanno visitato il **Annulla servizio** sul sito web ha anche chiamato il call center, e qual è stato il risultato.

Sotto le dimensioni, torna indietro e trova **Tipo di interazione chiamata**.
Trascinamento della selezione **Tipo di interazione chiamata** per sostituire la prima interazione a destra all’interno della **Visualizzazione Flusso**.

![demo](./images/pro43.png)

Ora visualizzi il ticket di supporto dei clienti che hanno chiamato il call center dopo aver visitato il **Annulla servizio** pagina.

![demo](./images/pro44.png)

Quindi, sotto le dimensioni, cerca **Sensazione di chiamata**.  Trascinala per sostituire la prima interazione a destra all’interno della **Visualizzazione Flusso**.

![demo](./images/pro46.png)

Vedrai questo:

![demo](./images/flow.png)

Come puoi vedere, abbiamo eseguito un’analisi omnicanale utilizzando la visualizzazione Flusso. Grazie a questo abbiamo scoperto che alcuni clienti che stavano pensando di annullare il loro servizio, hanno avuto un sentimento positivo dopo aver chiamato il call center. Forse abbiamo cambiato idea con una promozione?


## Come si comportano i clienti con un contatto Callcenter positivo rispetto ai KPI principali?

Segmentiamo prima i dati per ottenere solo gli utenti con **positivo** chiamate. In CJA, i segmenti sono denominati Filtri. Vai ai filtri all’interno dell’area del componente (sul lato sinistro) e fai clic su **+**.

![demo](./images/pro58.png)

Nel Generatore di filtri, assegna un nome al filtro

| Nome | Descrizione |
| ----------------- |-------------| 
| Sensazione di chiamata - Positivo | Sensazione di chiamata - Positivo |

![demo](./images/pro47.png)

Sotto i componenti (nel Generatore di filtri), trova **Sensazione di chiamata** e trascinarlo nella definizione del Generatore di filtri.

![demo](./images/pro48.png)

Ora seleziona **positivo** come valore per il filtro.

![demo](./images/pro49.png)

Modificare l&#39;ambito da **Persona** livello.

![demo](./images/pro50.png)

Per terminare, fai clic su **Salva**.

![demo](./images/pro51.png)

Allora tornerai qui. Se non è ancora stato eseguito, chiudi il pannello precedente.

![demo](./images/pro0c.png)

Ora aggiungi un nuovo pannello vuoto facendo clic su **+ Aggiungi pannello vuoto**.

![demo](./images/pro24c.png)

Seleziona lo stesso intervallo di date dell’esercizio precedente.

![demo](./images/pro24d.png)

Fai clic su **Tabella a forma libera**.

![demo](./images/pro52.png)

Ora trascina e rilascia il filtro appena creato.

![demo](./images/pro53.png)

È ora di aggiungere alcune metriche. Inizia con **Visualizzazioni prodotto**. Trascina nella tabella a forma libera. È inoltre possibile eliminare **Eventi** metrica.

![demo](./images/pro54.png)

Fai lo stesso con **Persone**,  **Aggiungi al carrello** e **Acquisti**. Finirete con un tavolo come questo.

![demo](./images/pro55.png)

Grazie alla prima analisi di flusso, mi è venuta in mente una nuova domanda. Così abbiamo deciso di creare questa tabella e controllare alcuni KPI rispetto a un segmento per rispondere a quella domanda. Come si può vedere, il tempo di analisi è molto più veloce rispetto all&#39;utilizzo di SQL o di altre soluzioni BI.

## Customer Journey Analytics e Analysis Workspace recap

Come hai imparato in questo laboratorio, Analysis Workspace unisce i dati di tutti i canali per analizzare l’intero percorso dei clienti. Inoltre, ricorda che è possibile inserire dati nella stessa area di lavoro che non è unita al percorso.
Può essere utile inserire dati disconnessi nell’analisi per fornire contesto al percorso. Alcuni esempi includono dati Server dei criteri di rete, sondaggi, eventi Facebook Ads o interazioni offline (non identificate).

Passaggio successivo: [4.6 Da informazioni all&#39;azione](./ex6.md)

[Torna al flusso utente 4](./uc4.md)

[Torna a tutti i moduli](./../../overview.md)
