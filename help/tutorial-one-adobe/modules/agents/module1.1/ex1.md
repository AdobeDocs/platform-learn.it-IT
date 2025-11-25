---
title: Guida introduttiva ad Agent Orchestrator
description: Guida introduttiva ad Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: 9011c4093b5fd6612426baf7003cd7b99523b6e8
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# 1.1.1 Guida introduttiva ad Agent Orchestrator

## 1.1.1.1 Imposta contesto in Agent Orchestrator

Vai a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Dovresti vedere questo. Assicurati di essere nell&#39;organizzazione **Experience Platform International**.

![Agent Orchestrator](./images/ao1.png)

Fare clic sulla finestra **contesto**.

![Agent Orchestrator](./images/ao2.png)

Imposta il contesto su:

- **Documentazione di Source**: **Customer Journey Analytics**
- **Sandbox**: **Accelera**
- **Visualizzazione dati**: **Accelerare il B2C del 2026**

Fare clic su **Imposta contesto**.

![Agent Orchestrator](./images/ao3.png)

>[!NOTE]
>
>In questa esercitazione, cambierete contesto quando passerete dall&#39;analisi all&#39;orchestrazione.

## 1.1.1.2 Inizia con le tendenze generali di acquisto per ancorare il contesto e ingrandire la visualizzazione della fibra

**Intento**: ottieni un impulso a livello toplevel sulla domanda di categoria, mobile, rete fissa, Internet, TV, fibra ottica, in particolare per gli ultimi 60 giorni. Questo stabilisce le linee di base per la stagionalità, gli effetti promozionali e la varianza regionale dopo il rollout NY.

**Pensiero**:

&quot;Fibre sta guadagnando azioni postNY? Stiamo assistendo alla cannibalizzazione di Internet in rame/DSL? Qual è il mix shift rispetto ai bundle TV?&quot;

&quot;Questo mi aiuterà a dimensionare il pubblico a cui rivolgersi a Vienna e a fissare obiettivi realistici&quot;.

**Letture utilizzabili previste dall&#39;addetto marketing**:

Grafico a barre/linee in pila degli acquisti per categoria principale (granulosità giornaliera/settimanale).

Percentuale di acquisti per categoria rispetto al periodo precedente.

Picchi significativi correlati alle date promozionali.

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Dovresti quindi vedere quanto segue:

>[!NOTE]
>
>Tieni d’occhio l’attribuzione in ritardo: gli ordini in fibra ottica possono essere acquisiti in &quot;Internet&quot; in alcuni schemi legacy. In tal caso, riconciliare la tassonomia prima delle decisioni.

![Agent Orchestrator](./images/ao5.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Dovresti vedere questo, che approfondisce le tendenze specifiche della fibra.

**Azione**: annota la curva di crescita e i picchi regionali.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Correlazione degli ordini con le preferenze del contenuto

**Intento**: verifica l&#39;ipotesi che la preferenza per i contenuti (ad esempio, SciFi, Sport, Drammatico) preveda il comportamento di aggiornamento della banda larga, in particolare per le esigenze di larghezza di banda elevata.

**Pensiero**

&quot;I fan di SciFi spesso guardano il 4K e lo streaming da più dispositivi; probabilmente a basso valore di latenza.&quot;

&quot;Quantifichiamo se SciFi (e forse Sport) è correlato agli ordini recenti.&quot;

**Output previsti**

Un pivot di Ordini (applicato filtro YTD) suddiviso per genere preferito, limitato agli ultimi 2 mesi.

Classifica i generi in base al tasso di conversione dell’ordine e al valore medio dell’ordine.

Decisione: se SciFi mostra un segnale forte, questo diventa un pilastro creativo primario per il lancio di Vienna di Fibre Max (ad esempio, messaggi &quot;mai più buffer&quot;, bundle premium).

**Intenzione**

Analizza la conversione per genere (ad esempio, Sci-Fi, Sport).

**Obiettivo** Verificare se le ventole Sci-Fi sono sovraindicizzate per gli aggiornamenti Fibre Channel.

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 Identificare Percorsi Fibre Esistenti

Fare clic sulla finestra **contesto**.

![Agent Orchestrator](./images/ao10.png)

Imposta il contesto su:

- **Documentazione di Source**: **Adobe Journey Optimizer**
- **Sandbox**: **Accelera**
- **Visualizzazione dati**: **Accelerare il B2C del 2026**

![Agent Orchestrator](./images/ao11.png)

**Intento** Scopri quali percorsi attivi o conclusi di recente includono &quot;Fibre&quot; nel titolo, ad esempio &quot;Fibre Upgrade NYC - Sept&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

**Pensiero**

&quot;Quale di questi percorsi ha funzionato bene, e quali sono stati i loro fattori scatenanti?&quot;

&quot;Posso riutilizzare la logica di orchestrazione vincente per Vienna?&quot;

**Output previsti**

Elenco di percorsi con stato (attivo, in pausa, terminato), intervalli di date, segmenti di destinazione, KPI (tasso di apertura, CTR, conversione).

Prossima mossa: selezionare uno o due percorsi in fibra di successo per la clonazione/adattamento.

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/ao13.png)

Elenca i percorsi attivi o passati con la messaggistica Fibre Channel.

Azione: selezionare percorsi con prestazioni elevate per la clonazione.

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Controllare il valore seed

**Intento**:

Comprendi la definizione di seed del percorso &quot;CitiSignal - Fibre Max Launch Promotion&quot;, ossia le caratteristiche che hanno guidato il targeting (ad esempio, &quot;Preferenza di genere SciFi&quot;, &quot;4+ dispositivi&quot;, &quot;streaming ≥ 300 GB/mese&quot;).

**Pensiero**

&quot;Voglio combinare la creatività di SciFi con la messaggistica a elevate prestazioni Fibre Max&quot;.

&quot;Se il pubblico si sovrappone con molti downloader, possiamo impilare la propensione.&quot;

**Output previsti**

Criteri di pubblico (inclusione/esclusione), dimensioni del pubblico, filtri per area geografica, attualità, soglie di frequenza.

>[!NOTE]
>
>Cambia contesto in CJA

Da questo punto, l’addetto al marketing passa alla modalità di analisi per garantire la generazione rapporti corretta.

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
What was the initial audience in the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/ao16.png)
Rivedi i criteri di pubblico (abitudini di streaming, conteggio dei dispositivi).

**Obiettivo**: comprendere le caratteristiche per le esigenze di larghezza di banda elevata.

## 1.1.1.6 Convalidare le prestazioni del percorso tramite analisi dell&#39;abbandono

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

>[!NOTE]
>
>Cambia contesto in CJA)

**Intento**:

Creare un funnel graduale in Customer Journey Analytics

Consegnato → aperto → Clic → Landed → Product View → Aggiungi al carrello → Checkout → Ordine completato

Includi viste SKU relative a Fibre come ramo.

**Pensiero**:

&quot;Dove stiamo perdendo le persone: e-mail aperte, caricamento della pagina di destinazione, PDP, attrito per il checkout?&quot;

&quot;Gli utenti di SciFi non raggiungono più o meno la media su Fibre PDP?&quot;

**Output previsti**:

Una visualizzazione dell’abbandono con tassi di abbandono a ogni passaggio.

Sovrapposizioni dei segmenti (SciFi vs Sport vs Altro).

Guasto del dispositivo/browser per attrito tecnico.

**Decisione**:

Se l’abbandono del pagamento è elevato, effettua una coordinazione con product/UX per correggere il flusso di pagamento.

Se l&#39;uscita da PDP è elevata, rielaborare la richiesta di rimborso (velocità, tempi di installazione, valore del bundle).

>[!NOTE]
>
>Cambia contesto in JO

Ora l’addetto al marketing si sposta in Adobe Journey Optimizer per l’orchestrazione e le operazioni del pubblico.

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey 
```

Creare una visualizzazione funnel: consegnato → aperto → selezionato → ordine di estrazione →.

**Azione**: identifica i punti di riconsegna e ottimizza la messaggistica o l&#39;interfaccia utente.

## 1.1.1.7 Trova i tipi di pubblico esistenti allineati all&#39;utilizzo elevato

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

>[!NOTE]
>
>Cambia contesto in Adobe Journey Optimizer

**Intento**:

Individua qualsiasi pubblico JO denominato con &quot;download pesanti&quot;, probabilmente definito da soglie di utilizzo dei dati mensili, ore di streaming o concorrenza tra dispositivi.

**Pensiero**:

&quot;Se esiste un pubblico come Heavy Downloaders, è perfetto per il posizionamento di Fibre Max: velocità, affidabilità, livelli illimitati&quot;.

**Output previsti**:

Metadati del pubblico: criteri di definizione, dimensioni, ultimo aggiornamento, tag di governance, disponibilità area geografica.

Individua tipi di pubblico con utilizzo elevato dei dati.

**Obiettivo**: combinare con la preferenza Sci-Fi per il targeting Fibre Max.

## 1.1.1.8 Determinare se tali tipi di pubblico sono già in uso

**Intento**:

Verifica il collegamento tra pubblico e percorso: assicurati di non duplicare i messaggi o entrare in conflitto con i programmi correnti.

**Pensiero**:

&quot;Se i Download pesanti si trovano già in un percorso di conservazione, abbiamo bisogno di una logica di soppressione o di un limite di frequenza per evitare affaticamenti.&quot;

**Output previsti**:

Mappature: pubblico → nome del percorso, stato, criteri di contatto, ultimo invio, prestazioni.

**Decisione**:

Se in uso, crea esclusioni o soppressione condivisa per il lancio di Vienna.

Se non in uso, luce verde per il nuovo percorso.

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Which of the above are used in a journey? 
```

Assicurati di non sovrapporsi alle campagne attive.

**Azione**: applica l&#39;eliminazione se necessario.

## 1.1.1.9 Crea nuovo Percorso per il lancio Fibre Max

**Intento**:

Crea un nuovo percorso destinato al pubblico composto:

Download pesanti ∩ preferenza SciFi (chiave pubblico kbaa_5207bf).

**Pensiero**:

&quot;Questo è il punto ideale per Fibre Max: alta propensione + rilevanza creativa.&quot;

&quot;Orchestreremo un’esperienza con più elementi in base alla disponibilità di Vienna.&quot;

**Progettazione Percorso (JO)**:

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

Dimostrare il contenuto al segnale di conversione (ordini per genere).

I miei percorsi di successo (trova percorsi con nome Fiberon e il pubblico promozionale SciFi).

Convalida dei punti di attrito (fallout CJA sul percorso SciFi).

Attiva contro i segmenti ad alta propensione (Download pesanti ∩ SciFi).

Immetti il seguente **Prompt** e fai clic sul pulsante **generate**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

Torna a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}