---
title: Cablaggio preassemblato IA
description: Cablaggio preassemblato IA
kt: 5342
doc-type: tutorial
exl-id: ce845231-17d1-40ab-96f7-bd386753e625
source-git-commit: 11ce179c0a94113dba391790ee6a86d70a7e9241
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---

# 1.1.6 Sfruttamento dell&#39;intelligenza artificiale

## Prerequisiti

Per seguire i passaggi descritti in questa esercitazione, come documentato di seguito, è necessario disporre dei seguenti diritti di accesso:

- Accesso a Real-Time CDP, Journey Optimizer e Customer Journey Analytics
- Accesso all’Assistente all’intelligenza artificiale in Adobe Experience Cloud
- Accesso ad AEP Agent Orchestrator
- È necessario installare Node.js 18+ nel sistema

## 1.1.6.1 Accedi ad Agent Orchestrator

Vai a [https://ao.adobe.io/](https://ao.adobe.io/). Accedi con il tuo account Adobe. Dopo aver effettuato l’accesso, assicurati di aver selezionato l’istanza e la sandbox corrette, modificandole come indicato di seguito.

![AO](./images/aov2lab1.png)

## 1.1.6.2 Imposta il contesto

Immetti il comando seguente e fai clic su **Invia**.

```
list dataviews
```

![AO](./images/aov2lab18.png)

Puoi ricevere questa richiesta. Fornisci le autorizzazioni necessarie.

![AO](./images/aov2lab19.png)

Puoi ricevere questa richiesta. Fornisci le autorizzazioni necessarie.

![AO](./images/aov2lab19a.png)

Dovresti vedere questo. Immetti il comando seguente e fai clic su **Invia**.

```
switch to dataview AdobeOne - Unified Customer Data View
```

![AO](./images/aov2lab20.png)

Dovresti vedere questo.

![AO](./images/aov2lab21.png)

## 1.1.6.3 Inizia con le tendenze generali di acquisto per ancorare il contesto e ingrandire la visualizzazione della fibra

**Intento**

Ottieni un impulso a livello di toplevel sulla domanda di categoria: mobile, rete fissa, Internet, TV, fibra ottica, in particolare per gli ultimi 60 giorni. Questo stabilisce le linee di base per la stagionalità, gli effetti promozionali e la varianza regionale dopo il rollout di New York.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by mainCategory over the last 2 months.
```

![Agent Orchestrator](./images/aotechlab4.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/aotechlab5.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by mainCategory = Fiber over the last 2 months per week
```

![Agent Orchestrator](./images/aotechlab6.png)

Dovresti vedere questo, che approfondisce le tendenze specifiche della fibra.

![Agent Orchestrator](./images/aotechlab7.png)

## 1.1.6.4 Correlazione degli ordini con le preferenze del contenuto

**Intento**

Testare l&#39;ipotesi che una preferenza per un genere specifico (ad esempio, SciFi, Sport, Drammatico) preveda il comportamento di aggiornamento della banda larga, in particolare per le esigenze di larghezza di banda elevata.

Innanzitutto, devi scoprire quale campo viene utilizzato per memorizzare la preferenza di genere.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which field is used to store the favourite genre?
```

![Agent Orchestrator](./images/aotechlab7a.png)

Dovresti visualizzarlo, il che mostra che il campo utilizzato per il genere è **`--aepTenantId--.individualCharacteristics.telco.mediaPreferences.favouriteGenre`**.

![Agent Orchestrator](./images/aotechlab7b.png)

Con tali informazioni, puoi iniziare a espandere i dati di acquisto.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Show me purchases by favourite genre for the last 2 months
```

![Agent Orchestrator](./images/aotechlab8.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/aotechlab9.png)

## 1.1.6.5 Identificare Percorsi Fibre Esistenti

**Intento**

Scopri quali percorsi attivi o conclusi di recente includono &quot;Fibre&quot; nel titolo, ad esempio &quot;Fibre Upgrade NYC - Sept&quot;, &quot;Fibre Trial - Streaming Bundle&quot;.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
What journeys exist? 
```

![Agent Orchestrator](./images/aotechlab12.png)

Dovresti vedere qualcosa del genere.

![Agent Orchestrator](./images/aotechlab13.png)

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Which of these journeys has 'Fiber' in its name?
```

![Agent Orchestrator](./images/aotechlab14.png)

Dovresti vedere questo. Fai clic sul collegamento a uno dei percorsi.

![Agent Orchestrator](./images/aotechlab15.png)

Verrà aperta una nuova finestra e verrà visualizzata immediatamente la panoramica dei dettagli del percorso.

![Agent Orchestrator](./images/aotechlab15a.png)

## 1.1.6.6 Controllare il pubblico utilizzato

**Intento**:

Comprendi la definizione di seed del percorso &quot;CitiSignal - Fibre Max Launch Promotion&quot;, ossia le caratteristiche che hanno guidato il targeting (ad esempio, &quot;Preferenza di genere SciFi&quot;, &quot;4+ dispositivi&quot;, &quot;streaming ≥ 300 GB/mese&quot;).

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
What was the initial audience in the journey named CitiSignal - Fiber Max Launch Promotion?
```

![Agent Orchestrator](./images/aotechlab16.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/aotechlab18.png)

## 1.1.6.7 Convalidare le prestazioni del percorso tramite analisi dell&#39;abbandono

**Intento**

Desideri comprendere l’abbandono delle prestazioni del percorso per sapere se nel percorso sono presenti nodi o condizioni che riscontrano una grande percentuale di profili eliminati. Questo è utile per capire se sono necessari ulteriori aggiustamenti nel percorso.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Create a fall-out report on the "CitiSignal - Fiber Max Launch Promotion" journey
```

![Agent Orchestrator](./images/aotechlab19.png)

Dovresti vedere questo.

![Agent Orchestrator](./images/aotechlab20.png)

## 1.1.6.8 Crea un nuovo pubblico

**Intento**

Sulla base dei risultati e delle ricerche di cui sopra, esiste una correlazione tra i clienti che consumano molti dati e che hanno un genere preferito di fantascienza o fantasy. Ora combinerai questi attributi in un pubblico.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Create an audience that combines people with an average download usage per month of over 2000 GB and a preferred genre of sci-fi or fantasy.
```

![Agent Orchestrator](./images/aotechlab32.png)

Se simili, i tipi di pubblico già esistenti sono già disponibili, dovresti visualizzare un messaggio simile.

![Agent Orchestrator](./images/aotechlab32a.png)

Rivedi il piano. Fare clic su **Approva piano**.

![Agent Orchestrator](./images/aotechlab33.png)

Il pubblico è stato creato.

![Agent Orchestrator](./images/aotechlab38.png)

>[!NOTE]
>
>Durante la creazione di un nuovo pubblico, sono necessarie 24 ore prima che il pubblico sia disponibile per l’Assistente AI per un ulteriore utilizzo.

## 1.1.6.9 Trova i tipi di pubblico esistenti allineati all&#39;utilizzo elevato e verifica se sono in uso

**Intento**:

Individua qualsiasi pubblico denominato con &quot;download pesanti&quot;, definito dalle soglie di utilizzo dei dati mensili.

>[!NOTE]
>
>Nel passaggio precedente, hai creato un nuovo pubblico. Tieni presente che saranno necessarie 24 ore prima che il pubblico sia disponibile per un ulteriore utilizzo per l’Assistente AI. Ora dovresti utilizzare invece un altro pubblico già esistente.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Is there an audience that has "heavy downloaders" in the title?
```

![Agent Orchestrator](./images/ao30.png)

Dovresti vedere questo. Ora vuoi vedere tutti i tuoi tipi di pubblico e quanto sono cambiati negli ultimi giorni.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
List how much these audiences changed over the last few days.
```

![Agent Orchestrator](./images/ao31.png)

Dovresti vedere questo. Fai clic su **Mostra altro**.

![Agent Orchestrator](./images/ao31a.png)

Dovresti vedere questo. Fare clic per chiudere il riquadro destro.

![Agent Orchestrator](./images/ao31b.png)

Scorri verso il basso un po&#39; per rivedere i passaggi eseguiti dall&#39;Assistente all&#39;intelligenza artificiale.

![Agent Orchestrator](./images/ao31c.png)

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
Are these journeys active? 
```

![Agent Orchestrator](./images/ao52.png)

Dovresti vedere qualcosa di simile a questo. Nessuno di questi percorsi è attualmente in esecuzione.

![Agent Orchestrator](./images/ao53.png)

Per il prossimo lancio di Fibre Max, è ora necessario creare un nuovo percorso.

## 1.1.6.10 Crea nuovo Percorso per il lancio Fibre Max

**Intento**:

Crea un nuovo percorso destinato al pubblico composto:

Download pesanti ∩ preferenza SciFi.

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
Create a  journey towards the audience Heavy Downloaders - Sci-Fi Preference_kbaa_5207bf. The journey is for the rollout of fiber broadband. There will 2 versions of an email  based on  a split of the audience based on who is in the "Eligble for Fiber upgrade" audience.  After 3 days, profiles from both email treatments who have not purchased fibre max will be sent a follow up email. 
```

![Agent Orchestrator](./images/aocj1.png)

Dovresti vedere questo. Immettere `yes` e fare clic su genera.

![Agent Orchestrator](./images/aocj2.png)

Dovresti vedere questo. Immettere `yes` e fare clic su genera.

![Agent Orchestrator](./images/aocj3.png)

Dovresti vedere questo. Immettere `The first one` e fare clic su Invia.

![Agent Orchestrator](./images/aocj4.png)

Dovresti vedere questo. Immettere `yes` e fare clic su Invia.

![Agent Orchestrator](./images/aocj5.png)

Rivedi la risposta. Immettere `yes` e fare clic su Invia.

![Agent Orchestrator](./images/aocj6.png)

Fai clic su **Rivedi**.

![Agent Orchestrator](./images/aocj7.png)

Aggiorna il nome del percorso con il tuo LDAP per renderlo univoco. Fai clic su **Salva**.

![Agent Orchestrator](./images/aocj8.png)

Il percorso è stato creato in modalità bozza.

![Agent Orchestrator](./images/aocj9.png)

## Gestione dei conflitti di Percorso di 1.1.6.11

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

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
List any conflicts for the journey +CitiSignal Fiber Max
```

Quindi seleziona manualmente il percorso **CitiSignal - Fibre Max Launch Promotion** dall&#39;elenco.

![Agent Orchestrator](./images/aocj70.png)

Dovresti vedere questo. Fai clic su **invia**.

![Agent Orchestrator](./images/aocj70a.png)

Esaminare le informazioni sul conflitto di percorso.

![Agent Orchestrator](./images/aocj71.png)

Scorri verso il basso per trovare ulteriori dettagli sui conflitti di percorso.

![Agent Orchestrator](./images/aocj72.png)

## 1.1.6.12 esperimenti

Immetti il seguente **Prompt** e fai clic sul pulsante **invia**.

```javascript
How are the experiments performing for the journey named 'CitiSignal - Fiber Max Launch Promotion'?
```

![Agent Orchestrator](./images/aoea0.png)

Dovresti quindi vedere quanto segue:

![Agent Orchestrator](./images/aoea1.png)

Scorri verso il basso e fai clic su uno dei suggerimenti. Fai clic su **invia**.

>[!NOTE]
>
>I suggerimenti sono dinamici, pertanto è necessario aspettarsi di visualizzare suggerimenti diversi ogni volta che viene generata una risposta. I suggerimenti saranno probabilmente diversi da quelli mostrati in questa schermata.

![Agent Orchestrator](./images/aoea2.png)

Dovresti quindi vedere una risposta dettagliata relativa al suggerimento scelto.

![Agent Orchestrator](./images/aoea4.png)

Ora hai completato il laboratorio.

## Passaggi successivi

Torna a [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}

