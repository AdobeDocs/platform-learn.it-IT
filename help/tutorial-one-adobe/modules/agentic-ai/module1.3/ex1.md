---
title: Guida introduttiva ad Agent Orchestrator
description: Guida introduttiva ad Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: e90dee164dfe098c9fc56a04c481a733c0843858
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# 1.1.1 Guida introduttiva ad Agent Orchestrator

## 1.3.1 Impostare il contesto in Agent Orchestrator

Passa all’assistente AI e attiva la visualizzazione Grande.

Conferma di essere nel contesto CJA per le attività di analisi.

>[!NOTE]
>
>Utilizza il cambio di contesto quando si passa da un’analisi (CJA) a un’orchestrazione (JO).

## 1.3.2 Inizia con le tendenze generali di acquisto per ancorare il contesto e ingrandire la fibra

**Prompt**:

```javascript
Show me purchases by mainCategory over the last 2 month
```

**Intento**: ottieni un impulso a livello toplevel sulla domanda di categoria, mobile, rete fissa, Internet, TV, fibra ottica, in particolare per gli ultimi 60 giorni. Questo stabilisce le linee di base per la stagionalità, gli effetti promozionali e la varianza regionale dopo il rollout NY.

Pensiero:

&quot;Fibre sta guadagnando azioni postNY? Stiamo assistendo alla cannibalizzazione di Internet in rame/DSL? Qual è il mix shift rispetto ai bundle TV?&quot;

&quot;Questo mi aiuterà a dimensionare il pubblico a cui rivolgersi a Vienna e a fissare obiettivi realistici&quot;.

Letture utilizzabili che l’addetto al marketing si aspetta:

Grafico a barre/linee in pila degli acquisti per categoria principale (granulosità giornaliera/settimanale).

Percentuale di acquisti per categoria rispetto al periodo precedente.

Picchi significativi correlati alle date promozionali.

>[!NOTE]
>
>Tieni d’occhio l’attribuzione in ritardo: gli ordini in fibra ottica possono essere acquisiti in &quot;Internet&quot; in alcuni schemi legacy. In tal caso, riconciliare la tassonomia prima delle decisioni.

 

**Prompt**:

```javascript
Show me purchases by mainCategory over the last 2 monthzoom into fiber performance
```

**Prompt successivo**

`Show me purchases by mainCategory = Fiber over the last 2 months`

Approfondisci le tendenze specifiche per le fibre.

**Azione** Nota la curva di crescita e i picchi regionali.

## 1.3.3 Correlazione tra ordini e preferenze di contenuto

**Prompt**:

```javascript
Show me ordersYTD by preferred genre for the last 2 months
```

**Intento** Verificare l&#39;ipotesi che la preferenza del contenuto (ad esempio, SciFi, Sport, Drammatico) preveda il comportamento di aggiornamento della banda larga, in particolare per le esigenze di larghezza di banda elevata.

**Pensiero**

&quot;I fan di SciFi spesso guardano il 4K e lo streaming da più dispositivi; probabilmente a basso valore di latenza.&quot;

&quot;Quantifichiamo se SciFi (e forse Sport) è correlato agli ordini recenti.&quot;

**Output previsti**

Un pivot di Ordini (applicato filtro YTD) suddiviso per genere preferito, limitato agli ultimi 2 mesi.

Classifica i generi in base al tasso di conversione dell’ordine e al valore medio dell’ordine.

Decisione: se SciFi mostra un segnale forte, questo diventa un pilastro creativo primario per il lancio di Vienna di Fibre Max (ad esempio, messaggi &quot;mai più buffer&quot;, bundle premium).

**Chiedi conferma**

`Show me ordersYTD by preferred genre for the last 2 months`

**Intenzione**

Analizza la conversione per genere (ad esempio, Sci-Fi, Sport).

**Obiettivo** Verificare se le ventole Sci-Fi sono sovraindicizzate per gli aggiornamenti Fibre Channel.

## 1.3.4 Identificare I Percorsi In Fibra Esistenti

**Prompt**:

```javascript
What journey was running and had Fiber in the name
```

**Intento** Scopri quali percorsi attivi o conclusi di recente includono &quot;Fibre&quot; nel titolo, ad esempio &quot;Fibre Upgrade NYC - Sept&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

**Pensiero**

&quot;Quale di questi percorsi ha funzionato bene, e quali sono stati i loro fattori scatenanti?&quot;

&quot;Posso riutilizzare la logica di orchestrazione vincente per Vienna?&quot;

**Output previsti**

Elenco di percorsi con stato (attivo, in pausa, terminato), intervalli di date, segmenti di destinazione, KPI (tasso di apertura, CTR, conversione).

Prossima mossa: selezionare uno o due percorsi in fibra di successo per la clonazione/adattamento.

**Chiedi conferma**

`What journey was running and had Fiber in the name?`

Elenca i percorsi attivi o passati con la messaggistica Fibre Channel.

Azione: selezionare percorsi con prestazioni elevate per la clonazione.

## 1.3.5 Controllare il pubblico seed per una promozione storica rilevante

**Prompt**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey
```

**Intento** Comprendere la definizione di seed del percorso &quot;SciFi Promo 2024 - jl&quot;. Quali caratteristiche hanno guidato il targeting (ad esempio, &quot;Preferenza di genere SciFi&quot;, &quot;4+ dispositivi&quot;, &quot;streaming ≥ 300 GB/mese&quot;).

**Pensiero**

&quot;Voglio combinare la creatività di SciFi con la messaggistica a elevate prestazioni Fibre Max&quot;.

&quot;Se il pubblico si sovrappone con molti downloader, possiamo impilare la propensione.&quot;

**Output previsti**

Criteri di pubblico (inclusione/esclusione), dimensioni del pubblico, filtri per area geografica, attualità, soglie di frequenza.

>[!NOTE]
>
>Cambia contesto in CJA

Da questo punto, l’addetto al marketing passa alla modalità di analisi per garantire la generazione rapporti corretta.

**Prompt**:

```javascript
What was the initial audience in that SCi-Fi promo 2024 - jl journey?
```

Rivedi i criteri di pubblico (abitudini di streaming, conteggio dei dispositivi).

Obiettivo: comprendere le caratteristiche per le esigenze di larghezza di banda elevata.

## 1.3.6 Convalidare le prestazioni del percorso mediante l&#39;analisi dell&#39;abbandono

**Prompt**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey
```

>[!NOTE]
>
>Cambia contesto in CJA)

**Intento** Creare un funnel graduale in Customer Journey Analytics

Consegnato → aperto → Clic → Landed → Product View → Aggiungi al carrello → Checkout → Ordine completato

Includi viste SKU relative a Fibre come ramo.

Pensiero:

&quot;Dove stiamo perdendo le persone: e-mail aperte, caricamento della pagina di destinazione, PDP, attrito per il checkout?&quot;

&quot;Gli utenti di SciFi non raggiungono più o meno la media su Fibre PDP?&quot;

Output previsti:

Una visualizzazione dell’abbandono con tassi di abbandono a ogni passaggio.

Sovrapposizioni dei segmenti (SciFi vs Sport vs Altro).

Guasto del dispositivo/browser per attrito tecnico.

Decisioni

Se l’abbandono del pagamento è elevato, effettua una coordinazione con product/UX per correggere il flusso di pagamento.

Se l&#39;uscita da PDP è elevata, rielaborare la richiesta di rimborso (velocità, tempi di installazione, valore del bundle).

>[!NOTE]
>
>Cambia contesto in JO

Ora l’addetto al marketing si sposta in Adobe Journey Optimizer per l’orchestrazione e le operazioni del pubblico.

**Prompt**:

```javascript
Create a fall-out report on the "Sci-Fi Promo 2024 - jl" journey 
```

Creare una visualizzazione funnel: consegnato → aperto → selezionato → ordine di estrazione →.

Azione: identifica i punti di riconsegna e ottimizza la messaggistica o l’esperienza utente.


## 1.3.7 Trovare il pubblico esistente allineato all&#39;utilizzo elevato

**Prompt**:

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Cambia contesto in Adobe Journey Optimizer

Intento: individua qualsiasi pubblico JO denominato con &quot;download pesanti&quot;, probabilmente definito da soglie di utilizzo dei dati mensili, ore di streaming o concorrenza tra dispositivi.

Pensiero:

&quot;Se esiste un pubblico come Heavy Downloaders, è perfetto per il posizionamento di Fibre Max: velocità, affidabilità, livelli illimitati&quot;.

Output previsti:

Metadati del pubblico: criteri di definizione, dimensioni, ultimo aggiornamento, tag di governance, disponibilità area geografica.

**Prompt**:

```javascript
Is there an audience that has " heavy downloaders" in the title 
```

Individua tipi di pubblico con utilizzo elevato dei dati.

Obiettivo: combina con la preferenza Sci-Fi per il targeting Fibre Max.

## 1.3.8 Determinare se tali tipi di pubblico sono già utilizzati

**Prompt**:

```javascript
Which of the above are used in a journey? 
```

Intento: controlla il collegamento pubblico-percorso: assicurati di non raddoppiare il messaggio o entrare in conflitto con i programmi correnti.

Pensiero:

&quot;Se i Download pesanti si trovano già in un percorso di conservazione, abbiamo bisogno di una logica di soppressione o di un limite di frequenza per evitare affaticamenti.&quot;

Output previsti:

Mappature: pubblico → nome del percorso, stato, criteri di contatto, ultimo invio, prestazioni.

Decisione:

Se in uso, crea esclusioni o soppressione condivisa per il lancio di Vienna.

Se non in uso, luce verde per il nuovo percorso.

Prompt:

quale dei suddetti metodi è utilizzato in un percorso?

Assicurati di non sovrapporsi alle campagne attive.

Azione: se necessario, applica l’eliminazione.

## 1.3.9 Creazione di un nuovo Percorso per il lancio di Fibre Max

**Prompt**:

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

Intento: Creare un nuovo percorso JO destinato al pubblico composto:

Download pesanti ∩ preferenza SciFi (chiave pubblico kbaa_5207bf).

Pensiero:

&quot;Questo è il punto ideale per Fibre Max: alta propensione + rilevanza creativa.&quot;

&quot;Orchestreremo un’esperienza con più elementi in base alla disponibilità di Vienna.&quot;

Progettazione percorso (JO):

Criteri di ingresso:

Pubblico: Download pesanti - Preferenza Sci-Fi_kbaa_5207bf

Geografia: metropolitana di Vienna (ZIP/CAP o geo polygon)

Idoneità: non fa parte della campagna &quot;Fiber Upgrade NYC - Sept&quot; attiva; non è un abbonato Fibre Channel corrente.

Attivazione e tempistica:

T14 giorni prima del lancio di Vienna (gennaio 2026): e-mail di anteprima—&quot;Fibre Max è in arrivo&quot;.

Settimana di lancio: e-mail principale + banner in-app + sincronizzazione di contenuti multimediali a pagamento (tramite destinazione CDP).

T+3 giorni: suddivisione del comportamento, se non si fa clic, SMS nudge; se si fa clic su ma non si ordina, effettua il retargeting con un CTA di disponibilità del programma di installazione.

T+10 giorni: test di offerta: installazione gratuita e sconto del 1° mese (A/B).

Personalization:

Copia dinamica per gli amanti di SciFi (latenza/hook di streaming 4K).

Dichiarazioni di velocità/latenza personalizzate in base al mix di dispositivi (console di gioco, caselle di streaming).

Consigli per il bundle: pacchetto di contenuti scifi Fibre Max + Premium TV.

Governance:

Limite di frequenza: massimo 3 contatti per 10 giorni.

Elimina se è presente l&#39;abbonato Fibre Channel corrente o un ticket per l&#39;installazione.

Rispetta le preferenze di rinuncia.

Piano di misurazione (CJA):

Tracciamento: consegna, apertura, clic, visualizzazione PDP, inizio pagamento, completamento ordine.

KPI: tasso di conversione a Fibre Max, uplift vs control, timetoinstall.

Diagnostica: rapporto di fallout per segmento dispositivo/genere.

Forma

Come tutto questo si inserisce (il modello mentale dell’addetto marketing)

Diagnosticare la domanda (categorie generali → Fibra in particolare).

Dimostrare il segnale di conversione del contenuto (ordini per genere).

I miei percorsi di successo (trova percorsi con nome Fiberon e il pubblico promozionale SciFi).

Convalida dei punti di attrito (fallout CJA sul percorso SciFi).

Attiva contro i segmenti ad alta propensione (Download pesanti ∩ SciFi).


Torna a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}