---
title: Guida introduttiva a Brand Concierge
description: Guida introduttiva a Brand Concierge
kt: 5342
doc-type: tutorial
exl-id: e05b60b1-62d7-4b70-834d-ef91782ac388
source-git-commit: fcf99e48868fd0b189291a7215a2871387ea7532
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 1%

---

# 1.4.1 Guida introduttiva a Brand Concierge

## Panoramica di 1.4.1.1 Brand Concierge

Durante la configurazione di Brand Concierge, i due elementi principali che utilizzerai sono:

- **Compositore agente (livello di configurazione)**

  Finalità: la piattaforma dell’interfaccia utente principale utilizzata per creare e configurare esperienze di IA per la conversazione.

  Responsabilità principali:

   - Definizione e gestione di origini dati e knowledge base
   - Imposta l’espressione del brand (tono, stile, guardrail)
   - Imposta l&#39;agente di prenotazione riunioni

- **Agent Orchestrator (motore di esecuzione)**

  Finalità: motore di ragionamento e orchestrazione che interpreta le richieste degli utenti ed esegue le azioni agente appropriate.

  Responsabilità principali:

   - Interpretare gli intenti dell&#39;utente in linguaggio naturale
   - Generare ed eseguire piani di ragionamento in più passaggi
   - Seleziona e richiama gli operatori/strumenti appropriati
   - Imporre contesto, conformità e guardrail del marchio
   - Coordinare flussi di lavoro con più agenti
   - Aggregare e comporre risposte da più origini dati

- **Runtime conversazione Brand Concierge (livello servizio)**

  Finalità: il livello di servizio di conversazione rivolto al cliente che gestisce le sessioni di chat, il contesto e le interazioni con i clienti.

  Componenti chiave:

   - Agente web (client): interfaccia utente browser o chat mobile integrata tramite Web SDK
   - Servizio di conversazione (back-end): gestisce lo stato della sessione e funge da gateway di orchestrazione

  Responsabilità principali:

   - Gestire le sessioni utente e le trascrizioni delle conversazioni
   - Gestire l’autenticazione e i profili degli utenti
   - Instradare i messaggi tra il client e Agent Orchestrator
   - Mantenere il contesto della conversazione
   - Registra gli eventi comportamentali e operativi in AEP per Analytics
   - Applicare configurazioni specifiche della superficie

## Configurazione istanza di Brand Concierge 1.4.1.2

Per iniziare a creare una tua istanza di Brand Concierge, segui i passaggi seguenti.

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Apri **Brand Concierge**.

![Brand Concierge](./images/bc1.png)

Dovresti vedere questo. Fai clic sul menu **selezione sandbox**. Scegli la sandbox che ti è stata assegnata. La sandbox deve essere denominata `techinsidersX` (sostituisci X con il numero assegnato).

![Brand Concierge](./images/bc2.png)

Quindi, compila le seguenti variabili:

- **Nome società**: CitiSignal

- **nome concierge**: `CitiSignal Sales Assistant`.

Immetti il testo seguente in **Come desideri che faccia il portinaio?**.

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

- **Collegamento sito Web**: fornisci il collegamento al sito Web in uso

Fai clic su **Continua**.

![Brand Concierge](./images/bc5.png)

Dovresti vedere questo. Queste informazioni sono state generate utilizzando l’intelligenza artificiale in base all’input fornito nella pagina precedente. Rivedi le informazioni e, quando ne sei soddisfatto, fai clic su **Genera concierge**.

![Brand Concierge](./images/bc6.png)

Dovresti vedere questo. Fai clic su **+ Add** accanto a **product advisory per gli utenti consumer**.

![Brand Concierge](./images/bc6a.png)

Dovresti vedere questo. Compila i campi seguenti utilizzando il testo seguente.

**Cosa deve sapere il consulente sul prodotto o sul pubblico prima di formulare consigli?**

```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

**Esistono regole o limitazioni aziendali che il portinaio deve seguire quando formula i consigli?**

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

**Esistono parole chiave o frasi specifiche che il portinaio deve seguire o evitare?**

```
Competitor pricing, competitor products
```

Fai clic su **Salva**.

![Brand Concierge](./images/bc13.png)

Fai clic sulla **freccia** per tornare alla schermata precedente.

![Brand Concierge](./images/bc13a.png)

Vai a **Knowledge Source** e fai clic su **Crea la tua origine della conoscenza**.

![Brand Concierge](./images/bc7.png)

Seleziona **Collegamenti al sito Web** e fai clic su **Continua**.

![Brand Concierge](./images/bc7a.png)

Dovresti vedere questo. Immetti `CitiSignal website` come nome per l&#39;origine della conoscenza.

Ora devi caricare un file csv contenente i collegamenti del tuo sito web. Scarica [Il file CSV dei collegamenti del sito Web CitiSignal](./assets/citisignal-website-links.csv) sul desktop.

Fare clic su **Sfoglia file**.

![Brand Concierge](./images/bc8.png)

Apri il file **citisignal-website-links.csv** e aggiorna i collegamenti in modo che puntino al tuo sito Web CitiSignal.

![Brand Concierge](./images/bc8a.png)

Seleziona il file **citisignal-website-links.csv** che hai appena scaricato e modificato. Fai clic su **Apri**.

![Brand Concierge](./images/bc9.png)

Il file viene ora aggiunto a questa origine di conoscenza. Fai clic su **Aggiungi**.

![Brand Concierge](./images/bc10.png)

Dovresti vedere questo. Fai clic su **Genera l&#39;origine della conoscenza**.

![Brand Concierge](./images/bc11.png)

Seleziona **Catalogo prodotti** e fai clic su **Continua**.

![Brand Concierge](./images/bc20.png)

Dovresti vedere questo. Immetti `CitiSignal Products` come nome per l&#39;origine della conoscenza. Fare clic su **Sfoglia file** e selezionare **Sfoglia dal dispositivo**.

![Brand Concierge](./images/bc21.png)

Ora devi caricare un file csv contenente i collegamenti del tuo sito web. Scarica il catalogo di prodotti [CitiSignal](./assets/CitiSignal-catalog.json.zip) sul desktop e decomprimi.

![Brand Concierge](./images/bc26.png)

Seleziona il file **CitiSignal-catalog.json** e fai clic su **Apri**.

![Brand Concierge](./images/bc23.png)

Dovresti vedere questo. Fai clic su **Aggiungi**.

![Brand Concierge](./images/bc24.png)

Allora tornerai qui. L’elaborazione richiederà 10-20 minuti, quindi dovrai tornare qui in un secondo momento per verificare se l’elaborazione è andata a buon fine.

![Brand Concierge](./images/bc25.png)

## 1.4.1.3 passaggi per l&#39;onboarding di AEP

Brand Concierge utilizza Adobe Experience Platform per memorizzare i dati di interazione provenienti dalle conversazioni. La connessione tra Brand Concierge e Experience Platform richiede che Brand Concierge configuri e utilizzi un flusso di dati.

### Stream di dati

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Apri **Experience Platform**.

![Brand Concierge](./images/aep1.png)

Verifica di aver selezionato la sandbox corretta, che deve essere denominata `techinsidersX`. Nel menu a sinistra, scorri verso il basso e seleziona **Flussi di dati**.

![Brand Concierge](./images/aep2.png)

Fare clic su **Nuovo flusso di dati**.

![Brand Concierge](./images/aep3.png)

Immettere il nome **Datastream** `--aepUserLdap-- - Brand Concierge`, quindi selezionare lo **Schema di mappatura** `cja-brand-concierge-sb-XXX`.

Fai clic su **Salva**.

![Brand Concierge](./images/aep4.png)

Lo stream di dati è ora configurato. Copia il nome e l’ID dello stream di dati e scrivili in un file di testo sul computer.

![Brand Concierge](./images/aep5.png)

### Gestione configurazione stream di dati

Il passaggio successivo consiste nell’abilitare l’API di gestione della configurazione di Brand Concierge per configurare lo stream di dati appena creato. Questa operazione è necessaria per risolvere elementi come l’ID organizzazione IMS e i dettagli della sandbox durante l’elaborazione della richiesta.

Vai alla **Home** e seleziona **Controlli di amministrazione**.

![Brand Concierge](./images/admincontrols1.png)

Vai a **Gestione configurazione Datastream**, quindi fai clic su **Aggiungi configurazione**.

![Brand Concierge](./images/admincontrols2.png)

Incolla l&#39;**ID dello stream di dati** creato in precedenza. Fai clic su **Salva**.

![Brand Concierge](./images/admincontrols3.png)

Dovresti vedere qualcosa del genere.

![Brand Concierge](./images/admincontrols4.png)

## Gestione configurazione stili 1.4.1.4

Vai a **Gestione configurazione stili**. Fare clic su **Inizializza configurazione stile**.

![Brand Concierge](./images/admincontrols7.png)

Immetti **Brand Name** `CitiSignal` e fai clic su **Initialize style config**.

![Brand Concierge](./images/admincontrols8.png)

Dovresti vedere questo.

![Brand Concierge](./images/admincontrols9.png)

## Manifesto Agent Orchestrator 1.4.1.5

Vai a **Aggiorna manifesto**. Dovresti vedere questo. Esamina le informazioni in ciascun campo e apporta le modifiche necessarie. Dopo aver apportato le modifiche, fai clic su **Aggiorna manifesto.

![Brand Concierge](./images/admincontrols5.png)

## 1.4.1.6 Completare l&#39;installazione dell&#39;origine delle informazioni

Vai a **Origini informazioni**. Dopo 10-20 minuti, lo **Stato** di entrambe le origini di conoscenza deve essere **Completato**. Quando lo stato è **Operazione completata** per entrambe le origini di conoscenza, fare clic su **Home**.

![Brand Concierge](./images/admincontrols10.png)

Dovresti vedere questo. Fai clic su **+ Connect** nella scheda **Collegamenti al sito Web**.

![Brand Concierge](./images/bc28.png)

Seleziona l&#39;origine della conoscenza **Sito Web CitiSignal** e fai clic su **Salva**.

![Brand Concierge](./images/bc29.png)

Dovresti vedere questo. Fai clic su **+ Connect** nella scheda **Catalogo prodotti**.

![Brand Concierge](./images/bc30.png)

Selezionare l&#39;origine della Knowledge Base **Prodotti CitiSignal** e fare clic su **Salva**.

![Brand Concierge](./images/bc31.png)

Dovresti vedere questo. Fai clic su **Anteprima** per iniziare a interagire con il tuo Brand Concierge.

![Brand Concierge](./images/bc32.png)

Ora puoi iniziare a porre domande relative alle fonti di conoscenza fornite.

![Brand Concierge](./images/bc33.png)

Immetti la domanda `what products do you sell?` e fai clic su **invia**.

![Brand Concierge](./images/bc102.png)

Dovresti ricevere una risposta simile.

![Brand Concierge](./images/bc103.png)

L’istanza di Brand Concierge è ora pronta per essere implementata sul sito web.

## Passaggi successivi

Vai a [Implementa Brand Concierge sul tuo sito Web](./ex2.md){target="_blank"}

Torna a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
