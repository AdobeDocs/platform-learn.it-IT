---
title: Guida introduttiva ad Agent Orchestrator
description: Guida introduttiva ad Agent Orchestrator
kt: 5342
doc-type: tutorial
source-git-commit: dee5b0855eeeb455bf22f511d11cd13f7e904889
workflow-type: tm+mt
source-wordcount: '1112'
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

## 1.1.1.2 Inizia con le tendenze generali di acquisto per ancorare il contesto e ingrandire la visualizzazione della fibra

**Intento**

Ottieni un impulso a livello di toplevel sulla domanda di categoria: mobile, rete fissa, Internet, TV, fibra ottica, in particolare per gli ultimi 60 giorni. Questo stabilisce le linee di base per la stagionalità, gli effetti promozionali e la varianza regionale dopo il rollout di New York.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/ao4.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/ao5.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

`Show me purchases by mainCategory = Fiber over the last 2 months per week`

![Agent Orchestrator](./images/ao6.png)

Dovresti vedere questo, che approfondisce le tendenze specifiche della fibra.

**Azione**: annota la curva di crescita e i picchi regionali.

![Agent Orchestrator](./images/ao7.png)

## 1.1.1.3 Correlazione degli ordini con le preferenze del contenuto

**Intento**

Testare l&#39;ipotesi che la preferenza dei contenuti (ad esempio, SciFi, Sport, Drammatico) preveda il comportamento di aggiornamento della banda larga, in particolare per le esigenze di larghezza di banda elevata.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me ordersYTD by preferredGenre for the last 2 months
```

![Agent Orchestrator](./images/ao8.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/ao9.png)

## 1.1.1.4 Identificare Percorsi Fibre Esistenti

**Intento**

Scopri quali percorsi attivi o conclusi di recente includono &quot;Fibre&quot; nel titolo, ad esempio &quot;Fibre Upgrade NYC - Sept&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/ao12.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/ao13.png)

Elenca i percorsi attivi o passati con la messaggistica Fibre Channel.

Azione: selezionare percorsi con prestazioni elevate per la clonazione.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/ao14.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/ao15.png)

## 1.1.1.5 Controllare il valore seed

**Intento**:

Comprendi la definizione di seed del percorso &quot;CitiSignal - Fibre Max Launch Promotion&quot;, ossia le caratteristiche che hanno guidato il targeting (ad esempio, &quot;Preferenza di genere SciFi&quot;, &quot;4+ dispositivi&quot;, &quot;streaming ≥ 300 GB/mese&quot;).

Immetti il seguente **Prompt**, quindi digita **+CitiSignal fib** per abilitare il completamento automatico. Seleziona il percorso **CitiSignal - Promozione lancio massimo Fibre Channel**.

```javascript
What was the initial audience in the journey named 
```

![Agent Orchestrator](./images/ao16.png)

Dovresti vedere questo. Fai clic sul pulsante **invia**.

![Agent Orchestrator](./images/ao17.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/ao18.png)

## 1.1.1.6 Convalidare le prestazioni del percorso tramite analisi dell&#39;abbandono

**Intento**

Creare un funnel graduale in Customer Journey Analytics

Consegnato → aperto → Clic → Landed → Product View → Aggiungi al carrello → Checkout → Ordine completato

Includi viste SKU relative a Fibre come ramo.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/ao19.png)

## 1.1.1.7 Crea un nuovo pubblico

**Intento**

Sulla base dei risultati di cui sopra, esiste una correlazione tra i clienti che consumano molti dati e che hanno un genere preferito di fantascienza o fantasy. Ora combinerai questi attributi in un pubblico.

Vai a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

>[!NOTE]
>
>Verifica che il contesto dell&#39;assistente punti alla sandbox **Accelerate** e alla visualizzazione dati **Accelerate 2026 B2C**

```javascript
Create an audience that combines people with an average download per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/ao32.png)

Rivedi il piano. Immetti `yes` e fai clic su **invia**.

![Agent Orchestrator](./images/ao33.png)

Rivedi l’espressione della query del segmento. Immetti `yes` e fai clic sul pulsante **invia**.

![Agent Orchestrator](./images/ao34.png)

Rivedi la stima della dimensione del segmento. Immetti `yes` e fai clic sul pulsante **invia**.

![Agent Orchestrator](./images/ao35.png)

Fai clic su **Rivedi**.

![Agent Orchestrator](./images/ao36.png)

Rivedi la definizione del segmento. Fai clic su **Crea**.

![Agent Orchestrator](./images/ao37.png)

Il pubblico è stato creato.

![Agent Orchestrator](./images/ao38.png)

>[!NOTE]
>
>Durante la creazione di un nuovo pubblico, sono necessarie 24 ore prima che il pubblico sia disponibile per l’assistente per un ulteriore utilizzo.

## 1.1.1.8 Trova i tipi di pubblico esistenti allineati all&#39;utilizzo elevato e verifica se sono in uso

**Intento**:

Individua qualsiasi pubblico denominato con &quot;download pesanti&quot;, definito dalle soglie di utilizzo dei dati mensili.

>[!NOTE]
>
>Nella versione precedente hai creato un nuovo pubblico, ricorda che ci vorranno 24 ore prima che il pubblico sia disponibile per un ulteriore utilizzo da parte dell’assistente. Ora dovresti utilizzare invece un altro pubblico già esistente.

Vai a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Dovresti vedere questo. Assicurati di essere nell&#39;organizzazione **Experience Platform International**.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

>[!NOTE]
>
>Verifica che il contesto dell&#39;assistente punti alla sandbox **Accelerate** e alla visualizzazione dati **Accelerate 2026 B2C**

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/ao31.png)

Ci sono già alcuni tipi di pubblico per i &quot;downloader pesanti&quot;. Vediamo se sono già in uso.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao50.png)

Dovresti vedere qualcosa di simile a questo.

![Agent Orchestrator](./images/ao51.png)

È ora necessario verificare se il percorso è attivo. Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which of the above are used in a journey? 
```

![Agent Orchestrator](./images/ao52.png)

Dovresti vedere qualcosa di simile a questo. Il percorso non è in esecuzione al momento.

![Agent Orchestrator](./images/ao53.png)

Per il prossimo lancio di Fibre Max, è ora necessario creare un nuovo percorso.

## 1.1.1.9 Crea nuovo Percorso per il lancio Fibre Max

**Intento**:

Crea un nuovo percorso destinato al pubblico composto:

Download pesanti ∩ preferenza SciFi (chiave pubblico kbaa_5207bf).

Vai a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Dovresti vedere questo. Assicurati di essere nell&#39;organizzazione **Experience Platform International**.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

>[!NOTE]
>
>Verifica che il contesto dell&#39;assistente punti alla sandbox **Accelerate** e alla visualizzazione dati **Accelerate 2026 B2C**

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Dovresti vedere questo. Immettere `yes` e fare clic su genera.

![Agent Orchestrator](./images/aocj2.png)

Dovresti vedere questo. Immettere `yes` e fare clic su genera.

![Agent Orchestrator](./images/aocj3.png)

Dovresti vedere questo. Immettere `The first one` e fare clic su genera.

![Agent Orchestrator](./images/aocj4.png)

Dovresti vedere questo. Immettere `yes` e fare clic su genera.

![Agent Orchestrator](./images/aocj5.png)

Rivedi la risposta. Immettere `yes` e fare clic su genera.

![Agent Orchestrator](./images/aocj6.png)

Fai clic su **Rivedi**.

![Agent Orchestrator](./images/aocj7.png)

Aggiorna il nome del percorso con il tuo LDAP per renderlo univoco. Fai clic su **Salva**.

![Agent Orchestrator](./images/aocj8.png)

Il percorso è stato creato in modalità bozza.

![Agent Orchestrator](./images/aocj9.png)

## Gestione dei conflitti di Percorso di 1.1.1.10

Vai a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Dovresti vedere questo. Assicurati di essere nell&#39;organizzazione **Experience Platform International**.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

>[!NOTE]
>
>Verifica che il contesto dell&#39;assistente punti all&#39;origine della documentazione **Journey Optimizer**, alla sandbox **Accelerate** e alla visualizzazione dati **Accelerate 2026 B2C**

```javascript
How can I manage journey conflicts?
```

![Agent Orchestrator](./images/aocj80.png)

Rivedi le informazioni.

![Agent Orchestrator](./images/aocj81.png)

Scorri verso il basso e seleziona **Origini** per verificare che le informazioni provengano da Experience League.

![Agent Orchestrator](./images/aocj82.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
List any conflicts for "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aocj70.png)

Esaminare le informazioni sul conflitto di percorso.

![Agent Orchestrator](./images/aocj71.png)

Scorri verso il basso per trovare ulteriori dettagli sui conflitti di percorso.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.1.11 esperimenti

Vai a [https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat](https://experience.adobe.com/#/@experienceplatform/ai-assistant/chat).

Dovresti vedere questo. Assicurati di essere nell&#39;organizzazione **Experience Platform International**.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

>[!NOTE]
>
>Verifica che il contesto dell&#39;assistente punti alla sandbox **Accelerate** e alla visualizzazione dati **Accelerate 2026 B2C**

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/aoea1.png)

Fare clic sul suggerimento per confrontare i tassi di conversione di ogni trattamento e quindi fare clic su **invia**.

![Agent Orchestrator](./images/aoea2.png)

Dovresti quindi vedere un confronto dettagliato come questo:

![Agent Orchestrator](./images/aoea4.png)

Torna a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}