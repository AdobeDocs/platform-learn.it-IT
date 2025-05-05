---
title: Customer Journey Analytics - Creare una visualizzazione dati
description: Customer Journey Analytics - Creare una visualizzazione dati
kt: 5342
doc-type: tutorial
exl-id: 048e4f0f-4713-4249-a118-88906b3ba5c0
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 3%

---

# 1.1.3 Creare una visualizzazione dati

## Obiettivi

- Comprendere l’interfaccia utente della visualizzazione dati
- Comprendere le impostazioni di base della definizione della visita
- Comprendere l’attribuzione e la persistenza all’interno di una visualizzazione dati

## 1.1.3.1 Visualizzazione dati

Una volta stabilita la connessione, ora puoi passare a influenzare la visualizzazione. Una differenza tra Adobe Analytics e CJA è che CJA necessita di una visualizzazione dati per pulire e preparare i dati prima della visualizzazione.

Una visualizzazione dati è simile al concetto di suite di rapporti virtuali in Adobe Analytics, in cui si definiscono le definizioni di visita in base al contesto, i filtri e anche il modo in cui vengono chiamati i componenti.

È necessaria almeno una visualizzazione dati per connessione. Tuttavia, per alcuni casi d’uso, è utile disporre di più visualizzazioni dati per la stessa connessione, con l’obiettivo di fornire informazioni diverse a team diversi.
Se desideri che la tua azienda diventi basata sui dati, devi adattare il modo in cui i dati vengono visualizzati in ogni team. Alcuni esempi:

- Metriche UX solo per il team di progettazione UX
- Per KPI e metriche per Google Analytics utilizza gli stessi nomi utilizzati per Customer Journey Analytics, in modo che il team di analisi digitale possa parlare una sola lingua.
- Visualizzazione dati filtrata per mostrare, ad esempio, i dati per un solo mercato, un marchio o solo per dispositivi mobili.

Nella schermata **Connessioni**, seleziona la casella di controllo davanti alla connessione appena creata. Fare clic su **Crea visualizzazione dati**.

![demo](./images/exta.png)

Verrai reindirizzato al flusso di lavoro **Crea visualizzazione dati**.

![demo](./images/0v2.png)

## 1.1.3.2 Definizione della visualizzazione dati

Ora puoi configurare le definizioni di base per la visualizzazione dati.

![demo](./images/0v2.png)

La **connessione** creata nell&#39;esercizio precedente è già selezionata. La connessione si chiama `--aepUserLdap-- – Omnichannel Data Connection`.

![demo](./images/ext5.png)

Assegnare quindi un nome alla visualizzazione dati seguendo questa convenzione di denominazione: `--aepUserLdap-- – Omnichannel Data View`.

Immettere lo stesso valore per la descrizione: `--aepUserLdap-- – Omnichannel Data View`.

| Nome | Descrizione | ID esterno |
| ----------------- |-------------|-------------| 
| `--aepUserLdap-- – Omnichannel Data View` | `--aepUserLdap-- – Omnichannel Data View` | `--aepUserLdap--123` |

![demo](./images/1v2.png)

Per il **fuso orario**, selezionare il fuso orario **Ora di Greenwich; Monrovia, Casablanca [GMT]**. Si tratta di un contesto molto interessante in quanto alcune aziende operano in paesi e aree geografiche diversi. Assegnare il fuso orario giusto a ciascun paese eviterebbe di commettere errori tipici nei dati, come credere, ad esempio, che in Perù la maggior parte della gente compri magliette alle 4 del mattino.

![demo](./images/ext7.png)

Puoi anche modificare la denominazione delle metriche principali (persona, sessione ed evento). Non è necessario, ma ad alcuni clienti piace utilizzare Persone, Visite e Hit invece di Persona, Sessione ed Eventi (la convenzione di denominazione predefinita è Customer Journey Analytics).

Ora dovresti aver configurato le seguenti impostazioni:

![demo](./images/1v2.png)

Fai clic su **Salva e continua**.

![demo](./images/12v2.png)

Fai clic su **Salva**.

![demo](./images/12v2a.png)

## 1.1.3.3 Componenti della visualizzazione dati

In questo esercizio configurerai i componenti necessari per analizzare i dati e visualizzarli utilizzando Analysis Workspace. In questa interfaccia utente sono disponibili tre aree principali:

- Lato sinistro: componenti disponibili dai set di dati selezionati
- In mezzo: componenti aggiunti alla visualizzazione dati
- Lato destro: Impostazioni dei componenti

![demo](./images/2v2.png)

Ora devi trascinare e rilasciare i componenti necessari per l&#39;analisi sui **Componenti aggiunti**. A questo scopo, devi selezionare i componenti nel menu a sinistra e trascinarli nell’area di lavoro al centro.

Iniziamo con il primo componente: **Nome (web.webPageDetails.name)**. Cerca questo componente, quindi trascinalo sull’area di lavoro.

![demo](./images/3v2.png)

Questo componente è il nome della pagina, come si può derivare dalla lettura del campo schema `(web.webPageDetails.name)`.

Tuttavia, l&#39;utilizzo di **Nome** come nome non è la migliore convenzione di denominazione per consentire a un utente aziendale di comprendere rapidamente questa dimensione.

Cambiiamo il nome in **Nome pagina**. Fare clic sul componente e rinominarlo nell&#39;area **Impostazioni componente**.

![demo](./images/30v2.png)

Un elemento molto importante è **Impostazioni di persistenza**. Il concetto di evar e prop non esiste in CJA, ma le impostazioni di persistenza consentono un comportamento simile.

![demo](./images/30v21.png)

Se non modifichi queste impostazioni, CJA interpreterà la dimensione come **Prop** (livello hit). Inoltre, possiamo cambiare la persistenza per rendere la dimensione un **eVar** (mantenere il valore in tutto il percorso).

Se non conosci eVar e proprietà, puoi [ulteriori informazioni su di esse nella documentazione](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html?lang=it).

Lasciamo Nome pagina come proprietà. Non è quindi necessario modificare le **impostazioni di persistenza**.

| Nome componente da cercare | Nuovo nome | Impostazioni persistenza |
| ----------------- |-------------| --------------------| 
| Nome (web.webPageDetails.name) | Nome pagina |          |

Quindi, scegli la dimensione **phoneNumber** e rilasciala nell&#39;area di lavoro. Il nuovo nome deve essere **Numero di telefono**.

![demo](./images/31v2.png)

Infine, cambiamo le impostazioni di Persistenza, in quanto il numero mobile deve persistere a livello di utente.

Per modificare la persistenza, scorri verso il basso nel menu a destra e apri la scheda **Persistenza**:

![demo](./images/5v2.png)

Seleziona la casella di controllo per modificare le impostazioni di persistenza. Seleziona **Most Recent** (Più recente) e l&#39;ambito **Person (Finestra di reporting)** (Persona), in quanto ci interessa solo l&#39;ultimo numero di cellulare di quella persona. Se il cliente non compila il dispositivo mobile nelle visite future, vedrai comunque questo valore popolato.

| Nome componente da cercare | Nuovo nome | Impostazioni persistenza |
| ----------------- |-------------| --------------------| 
| phoneNumber | Numero di telefono | Più recente, finestra di reporting per persona |

![demo](./images/6v2.png)

Il componente successivo è `web.webPageDetails.pageViews.value`.

Nel menu a sinistra, cercare `web.webPageDetails.pageViews.value`. Trascina e rilascia questa metrica nell’area di lavoro.

Cambia il nome in **Visualizzazioni pagina** nelle **Impostazioni componente**.

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |         |

![demo](./images/7v2.png)

Per le impostazioni di attribuzione, non è necessario modificare nulla.

Nota: le impostazioni di persistenza sulle metriche possono essere modificate anche in Analysis Workspace. In alcuni casi puoi scegliere di impostarlo qui per evitare che gli utenti aziendali debbano pensare qual è il modello di persistenza migliore.

Successivamente, dovrai configurare molte dimensioni e metriche, come indicato nella tabella seguente.

### DIMENSIONI


| Nome componente da cercare | Nuovo nome | Impostazioni persistenza |
| ----------------- |-------------| --------------------| 
| brandName | Marchio | Più recente, sessione |
| sentimento di chiamata | Sentimento di chiamata |          |
| ID chiamata | Tipo di interazione chiamata |          |
| callTopic | Richiama argomento | Più recente, sessione |
| ecid | ECID | Più recente, finestra di reporting per persona |
| e-mail | ID e-mail | Più recente, finestra di reporting per persona |
| Tipo di pagamento | Tipo di pagamento |          |
| Metodo di aggiunta del prodotto | Metodo di aggiunta del prodotto | Più recente, sessione |
| Tipo evento | Tipo evento |         |
| Nome (productListItems.name) | nome del prodotto |         |
| SKU (Stock Keeping Unit) | SKU (sessione) | Più recente, sessione |
| ID transazione | ID transazione |         |
| URL (web.webPageDetails.URL) | URL |         |
| Agente utente | Agente utente | Più recente, sessione |

### METRICHE

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| Quantità | Quantità |          |
| commerce.order.priceTotal | Ricavi |         |

La configurazione dovrebbe quindi essere simile alla seguente. Non dimenticare di **salvare** la visualizzazione dati. Quindi fai clic su **Salva** adesso.

![demo](./images/11v2.png)

## 1.1.3.4 Metriche calcolate


Anche se hai organizzato tutti i componenti nella visualizzazione dati, devi comunque adattarne alcuni, in modo che gli utenti aziendali siano pronti per iniziare la loro analisi.

Se ricordi, non hai inserito specificamente nella visualizzazione dati metriche quali Aggiungi al carrello, Visualizzazione prodotto o Acquisti.
Tuttavia, esiste una dimensione denominata: **Tipo evento**. Quindi, puoi derivare questi tipi di interazione creando 3 metriche calcolate.

Iniziamo con la prima metrica: **Visualizzazioni prodotto**.

Sul lato sinistro, cercare **Tipo evento** e selezionare la dimensione. Trascinalo nell&#39;area di lavoro **Componenti inclusi**.
Fare clic per selezionare la nuova metrica **Tipo evento**.

![demo](./images/calcmetr1.png)

Ora modifica il nome e la descrizione del componente con i seguenti valori:

| Nome componente | Descrizione componente |
| ----------------- |-------------| 
| Visualizzazioni prodotto | Visualizzazioni prodotto |

![demo](./images/calcmetr3.png)

Ora consente di contare solo **Visualizzazioni prodotto** eventi. A tale scopo, scorri verso il basso in **Impostazioni componente** fino a visualizzare **Includi valori di esclusione**. Assicurarsi di abilitare l&#39;opzione **Impostare i valori di inclusione/esclusione**.

![demo](./images/calcmetr4.png)

Poiché desideri contare solo **Visualizzazioni prodotto**, specifica **commerce.productViews** in base ai criteri.

![demo](./images/calcmetr5.png)

La metrica calcolata è ora pronta.

Ripeti quindi lo stesso processo per **Aggiungi al carrello** e **Acquista** eventi.

### Aggiungi al carrello

Trascinare la stessa dimensione **Tipo evento**.

![demo](./images/calcmetr1.png)

Verrà visualizzato un avviso popup di un campo duplicato poiché si sta utilizzando la stessa variabile. Fai clic su **Aggiungi comunque**:

![demo](./images/calcmetr6.png)

Ora, segui lo stesso processo che abbiamo fatto per la metrica Visualizzazioni prodotto:
- Modificare innanzitutto il nome e la descrizione.
- Infine, aggiungi **commerce.productListAdds** come criterio per contare solo Aggiungi al carrello

| Nome | Descrizione | Criteri |
| ----------------- |-------------| -------------|
| Aggiungi al carrello | Aggiungi al carrello | commerce.productListAdds |

![demo](./images/calcmetr6a.png)

### Acquisti

Trascina e rilascia la stessa dimensione **Tipo evento** come per entrambe le metriche precedenti.

![demo](./images/calcmetr1.png)

Verrà visualizzato un avviso popup di un campo duplicato poiché si sta utilizzando la stessa variabile. Fai clic su **Aggiungi comunque**:

![demo](./images/calcmetr6.png)

Ora, segui lo stesso processo che abbiamo fatto per le metriche Visualizzazioni prodotto e Aggiungi al carrello:
- Modificare innanzitutto il nome e la descrizione.
- Infine, aggiungi **commerce.purchases** come criterio per contare solo Aggiungi ai carrello

| Nome | Descrizione | Criteri |
| ----------------- |-------------| -------------|
| Acquisti | Acquisti | commerce.purchases |

![demo](./images/calcmetr7a.png)

La configurazione finale dovrebbe quindi essere simile a questa. Fai clic su **Salva e continua**.

![demo](./images/calcmetr8.png)

## 1.1.3.5 Impostazioni della visualizzazione dati

Dovresti essere reindirizzato a questa schermata:

![demo](./images/8v2.png)

In questa scheda puoi modificare alcune impostazioni importanti per modificare la modalità di elaborazione dei dati. Iniziamo impostando il **timeout sessione** su 30 minuti. Grazie alla marca temporale di ogni evento esperienza è possibile estendere il concetto di sessione su tutti i canali. Ad esempio, cosa succede se un cliente chiama il call center dopo aver visitato il sito web? Utilizzando i timeout di sessione personalizzati si dispone di molta flessibilità nel decidere cosa sia una sessione e come unirà i dati.

![demo](./images/ext8.png)

In questa scheda puoi modificare altri elementi, ad esempio filtrare i dati utilizzando un segmento o un filtro. Non è necessario eseguire questa operazione in questo esercizio.

![demo](./images/10v2.png)

Al termine, fai clic su **Salva e termina**.

![demo](./images/13v2.png)

>[!NOTE]
>
>Puoi tornare a questa visualizzazione dati in seguito e modificare le impostazioni e i componenti in qualsiasi momento. Le modifiche influiranno sulla visualizzazione dei dati storici.

Ora puoi continuare con la parte di visualizzazione e analisi.

## Passaggi successivi

Vai a [1.1.4 Preparazione dati in Customer Journey Analytics](./ex4.md)(./ex2.md){target="_blank"}

Torna a [Customer Journey Analytics](./customer-journey-analytics-build-a-dashboard.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
