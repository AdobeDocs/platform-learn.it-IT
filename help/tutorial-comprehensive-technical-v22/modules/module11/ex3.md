---
title: Customer Journey Analytics - Creare una visualizzazione dati
description: Customer Journey Analytics - Creare una visualizzazione dati
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 4d78dccd-0544-469e-a91b-eb2e7771b3bd
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 2%

---

# 11.3 Creare una visualizzazione dati

## Obiettivi

- Comprendere l’interfaccia utente della visualizzazione dati
- Comprendere le impostazioni di base della definizione della visita
- Comprendere l’attribuzione e la persistenza all’interno di una visualizzazione dati

## Visualizzazione dati 11.3.1

Al termine della connessione, puoi ora passare all’influenza della visualizzazione. Una differenza tra Adobe Analytics e CJA è che CJA ha bisogno di una visualizzazione dati per pulire e preparare i dati prima della visualizzazione.

Una visualizzazione dati è simile al concetto di suite di rapporti virtuali in Adobe Analytics, dove puoi definire definizioni di visite basate sul contesto, filtri e anche come vengono chiamati i componenti.

È necessaria almeno una visualizzazione dati per connessione. Tuttavia, per alcuni casi d’uso, è grandioso disporre di più visualizzazioni dati per la stessa connessione, con l’obiettivo di fornire informazioni diverse a diversi team.
Se desideri che la tua azienda sia basata sui dati, devi adattare il modo in cui i dati vengono visualizzati in ciascun team. Alcuni esempi:

- Metriche UX solo per il team di progettazione UX
- Utilizza gli stessi nomi per KPI e Metriche per Google Analytics e Customer Journey Analytics in modo che il team di analisi digitale possa parlare solo 1 lingua.
- Visualizzazione dati filtrata per mostrare, ad esempio, i dati per un solo mercato, un solo marchio o solo per dispositivi mobili.

Sulla **Connessioni** seleziona la casella di controllo di fronte alla connessione appena creata. Fai clic su **Crea visualizzazione dati**.

![demo](./images/exta.png)

Verrai reindirizzato al **Crea visualizzazione dati** workflow.

![demo](./images/0-v2.png)

## 11.3.2 Definizione della visualizzazione dati

Ora puoi configurare le definizioni di base per la visualizzazione dati.

![demo](./images/0-v2.png)

La **Connessione** creato nell’esercizio precedente è già selezionato. La connessione è denominata `--demoProfileLdap-- – Omnichannel Data Connection`.

![demo](./images/ext5.png)

Successivamente, assegna alla visualizzazione dati un nome seguendo questa convenzione di denominazione: `--demoProfileLdap-- – Omnichannel Data View`.

Inserisci lo stesso valore per la descrizione: `--demoProfileLdap-- – Omnichannel Data View`.

| Nome | Descrizione |
| ----------------- |-------------| 
| `--demoProfileLdap-- – Omnichannel Data View` | `--demoProfileLdap-- – Omnichannel Data View` |

![demo](./images/1-v2.png)

Per **Fuso orario**, seleziona il fuso orario **Ora media di Greenwich; Monrovia, Casablanca [GMT]**. Si tratta di un ambiente molto interessante in quanto alcune aziende operano in diversi paesi e aree geografiche. Allocare il fuso orario giusto per ogni paese eviterà errori di dati tipici come credere che, per esempio, in Perù, la maggior parte delle persone compra T-shirt alle 4:00 del mattino.

![demo](./images/ext7.png)

Puoi anche modificare la denominazione delle metriche principali (Persona, Sessione ed Evento). Questo non è necessario, ma ad alcuni clienti piace utilizzare Persone, Visite e Hit al posto di Persona, Sessione ed Eventi (convenzione di denominazione predefinita dal Customer Journey Analytics).

A questo punto è necessario configurare le seguenti impostazioni:

![demo](./images/1-v2.png)

Fai clic su **Salva e continua**.

![demo](./images/12-v2.png)

## 11.3.3 Componenti di visualizzazione dati

In questo esercizio, configurerai i componenti necessari per analizzare i dati e visualizzarli utilizzando Analysis Workspace. In questa interfaccia utente sono disponibili tre aree principali:

- Lato sinistro: Componenti disponibili dai set di dati selezionati
- Medio: Componenti aggiunti alla visualizzazione dati
- Lato destro: Impostazioni dei componenti

![demo](./images/2-v2.png)

>[!IMPORTANT]
>
>Se non riesci a trovare una metrica o una dimensione specifica, controlla se il campo `Contains data` viene rimosso dalla visualizzazione dati. In caso contrario, cancella quel campo.
>
>![demo](./images/2-v2a.png)

Ora devi trascinare i componenti necessari per l’analisi nella sezione **Componenti aggiunti**. A questo scopo, devi selezionare i componenti nel menu a sinistra, trascinarli e rilasciarli nell’area di lavoro al centro.

Cominciamo con il primo componente: **Nome (web.webPageDetails.name)**. Cerca questo componente, quindi trascinalo sull’area di lavoro.

![demo](./images/3-v2.png)

Questo componente è il nome della pagina, come è possibile derivare dalla lettura del campo schema `(web.webPageDetails.name)`.

Tuttavia, utilizzando **Nome** poiché il nome non è la convenzione di denominazione migliore per consentire a un utente aziendale di comprendere rapidamente questa dimensione.

Cambiamo il nome in modo che sia **Nome pagina**. Fai clic sul componente e rinominalo nel **Impostazioni dei componenti** area.

![demo](./images/3-0-v2.png)

Qualcosa di veramente importante è la **Impostazioni di persistenza**. Il concetto di evar e prop non esiste in CJA, ma le impostazioni di persistenza rendono possibile un comportamento simile.

![demo](./images/3-0-v21.png)

Se non modifichi queste impostazioni, CJA interpreterà la dimensione come una **Prop** (livello hit). Inoltre, possiamo cambiare la Persistenza per rendere la dimensione una **eVar** (persiste il valore in tutto il percorso).

Se non conosci eVar e proprietà, puoi [ulteriori informazioni nella documentazione](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html).

Lasciamo il Nome pagina come proprietà. In quanto tale, non è necessario modificare alcuna **Impostazioni di persistenza**.

| Nome componente da cercare | Nuovo nome | Impostazioni di persistenza |
| ----------------- |-------------| --------------------| 
| Nome (web.webPageDetails.name) | Nome pagina |  |

Quindi, scegli la dimensione **phoneNumber** e rilasciarlo sull&#39;area di lavoro. Il nuovo nome deve essere **Numero di telefono**.

![demo](./images/3-1-v2.png)

Infine, modifichiamo le impostazioni di persistenza, in quanto il numero mobile deve persistere a livello di utente.

Per modificare la persistenza, scorri verso il basso nel menu di destra e apri la **Persistenza** scheda:

![demo](./images/5-v2.png)

Seleziona la casella di controllo per modificare le impostazioni di persistenza. Seleziona **Più recente** e **Persona (intervallo di reporting)** scopo, in quanto ci importa solo dell&#39;ultimo numero di cellulare di quella persona. Se il cliente non compila il dispositivo mobile nelle visite future, visualizzerai comunque questo valore popolato.

![demo](./images/6-v2.png)

| Nome componente da cercare | Nuovo nome | Impostazioni di persistenza |
| ----------------- |-------------| --------------------| 
| phoneNumber | Numero di telefono | Più recente, Persona (intervallo di reporting) |

Il componente successivo è `web.webPageDetails.pageViews.value`.

Nel menu a sinistra, cerca `web.webPageDetails.pageViews.value`. Trascina e rilascia la metrica nell’area di lavoro.

Modificare il nome in modo che sia **Visualizzazioni pagina** in **Impostazioni dei componenti**.

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |  |

![demo](./images/7-v2.png)

Per le impostazioni di attribuzione, lasceremo vuoto questo campo.

Nota: Le impostazioni di persistenza sulle metriche possono essere modificate anche in Analysis Workspace. In alcuni casi puoi scegliere di impostarlo qui per evitare che gli utenti aziendali debbano pensare quale sia il modello di persistenza migliore.

Successivamente, dovrai configurare molti Dimension e metriche, come indicato nella tabella seguente.

### Dimension


| Nome componente da cercare | Nuovo nome | Impostazioni di persistenza |
| ----------------- |-------------| --------------------| 
| brandName | Nome del marchio | Sessione più recente |
| sentimento | Sensazione di chiamata |  |
| ID chiamata | Tipo di interazione chiamata |  |
| callTopic | Argomento della chiamata | Sessione più recente |
| ecid | ECID | Più recente, Persona (intervallo di reporting) |
| e-mail | ID e-mail | Più recente, Persona (intervallo di reporting) |
| Tipo di pagamento | Tipo di pagamento |  |
| Metodo di aggiunta dei prodotti | Metodo di aggiunta dei prodotti | Sessione più recente |
| Tipo evento | Tipo evento |  |
| Nome (productListItems.name) | Nome del prodotto |  |
| SKU | SKU (sessione) | Sessione più recente |
| ID transazione | ID transazione |  |
| URL (web.webPageDetails.URL) | URL |  |
| Agente utente | Agente utente | Sessione più recente |

### METRICHE

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| Quantità | Quantità |  |
| commerce.order.priceTotal | Ricavi |  |

La configurazione dovrebbe quindi essere simile alla seguente:

![demo](./images/11-v2.png)

Non dimenticarti di **Salva** visualizzazione dati. Fai clic su **Salva** ora.

![demo](./images/12-v2s.png)

## 11.3.4 Metriche calcolate


Anche se abbiamo organizzato tutti i componenti nella visualizzazione dati, è comunque necessario adattarli, in modo che gli utenti aziendali siano pronti per iniziare la loro analisi.

Se ricordi, non abbiamo introdotto specificatamente Metriche come Aggiungi al carrello, Visualizzazione prodotto o Acquisti nella Visualizzazione dati.
Tuttavia, abbiamo una dimensione chiamata: **Tipo evento**. Quindi, deriviamo questi tipi di interazione creando 3 Metriche calcolate.

Cominciamo con la prima metrica: **Visualizzazioni prodotto**.

Sul lato sinistro, cerca **Tipo evento** e seleziona la quota. Quindi trascinalo nella **Componenti inclusi** tela.

![demo](./images/calcmetr1.png)

Fai clic per selezionare la nuova metrica **Tipo evento**.

![demo](./images/calcmetr2.png)

Ora modifica il nome e la descrizione del componente con i seguenti valori:

| Nome componente | Descrizione del componente |
| ----------------- |-------------| 
| Visualizzazioni prodotto | Visualizzazioni prodotto |

![demo](./images/calcmetr3.png)

Ora possiamo contare solo **Visualizzazioni prodotto** eventi. Per farlo, scorri verso il basso nella sezione **Impostazioni dei componenti** fino a quando non vedi **Includi valori di esclusione**. Assicurati di abilitare l’opzione **Imposta valori di inclusione/esclusione**.

![demo](./images/calcmetr4.png)

Come vogliamo solo contare **Visualizzazioni prodotto**, specificare **commerce.productViews** secondo i criteri.

![demo](./images/calcmetr5.png)

La metrica calcolata è ora pronta.

Quindi, ripeti lo stesso processo per **Aggiungi al carrello** e **Acquisto** eventi.

### Aggiungi al carrello

Trascina e rilascia la stessa dimensione **Tipo evento**.

![demo](./images/calcmetr1.png)

Visualizzerai un avviso pop-up di un campo duplicato mentre utilizziamo la stessa variabile. Fai clic su **Aggiungi comunque**:

![demo](./images/calcmetr6.png)

Ora segui lo stesso processo utilizzato per la metrica Visualizzazioni prodotto :
- Modificare innanzitutto il nome e la descrizione.
- Aggiungi infine **commerce.productListAdd** come criteri per contare solo Aggiungi al carrello

| Nome | Discrepione | Criteri |
| ----------------- |-------------| -------------|
| Aggiungi al carrello | Aggiungi al carrello | commerce.productListAdds |

![demo](./images/calcmetr6a.png)

### Acquisti

Trascina e rilascia la stessa dimensione **Tipo evento** come abbiamo fatto per entrambe le metriche precedenti.

![demo](./images/calcmetr1.png)

Visualizzerai un avviso pop-up di un campo duplicato mentre utilizziamo la stessa variabile. Fai clic su **Aggiungi comunque**:

![demo](./images/calcmetr7.png)

Ora, segui lo stesso processo delle metriche Visualizzazioni prodotto e Aggiungi al carrello:
- Modificare innanzitutto il nome e la descrizione.
- Aggiungi infine **commerce.purchase** come criteri per contare solo Aggiungi ai carrelli

| Nome | Discrepione | Criteri |
| ----------------- |-------------| -------------|
| Acquisti | Acquisti | commerce.purchases |

![demo](./images/calcmetr7a.png)

La configurazione finale dovrebbe quindi essere simile a questa. Fai clic su **Salva e continua**.

![demo](./images/calcmetr8.png)

## 11.3.5 Impostazioni visualizzazione dati

Dovresti essere reindirizzato a questa schermata:

![demo](./images/8-v2.png)

In questa scheda, puoi modificare alcune impostazioni importanti per modificare la modalità di elaborazione dei dati. Cominciamo impostando il **Timeout sessione** a 30 min. Grazie alla marca temporale di ogni evento di esperienza puoi estendere il concetto di sessione su tutti i canali. Ad esempio, cosa succede se un cliente chiama il call-center dopo aver visitato il sito web? Utilizzando i timeout di sessione personalizzati hai molta flessibilità nel decidere cosa sia una sessione e come tale sessione unirà i dati.

![demo](./images/ext8.png)

In questa scheda puoi modificare altri elementi, come filtrare i dati utilizzando un segmento/filtro. Non dovrete farlo in questo esercizio.

![demo](./images/10-v2.png)

Al termine, fai clic su **Salva e completa**.

![demo](./images/13-v2.png)

>[!NOTE]
>
>Successivamente potrai tornare a questa visualizzazione dati e modificare le impostazioni e i componenti in qualsiasi momento. Le modifiche avranno effetto sulla visualizzazione dei dati storici.

Ora puoi continuare con la parte relativa alla visualizzazione e all’analisi.

Passaggio successivo: [11.4 Preparazione dei dati in Customer Journey Analytics](./ex4.md)

[Torna al modulo 11](./customer-journey-analytics-build-a-dashboard.md)

[Torna a tutti i moduli](./../../overview.md)
