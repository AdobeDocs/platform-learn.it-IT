---
title: Guida introduttiva a Brand Concierge
description: Guida introduttiva a Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 1%

---

# 1.4.1 Guida introduttiva a Brand Concierge

## Video

Questo video illustra e illustra tutti i passaggi di questo esercizio.

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

Dovresti vedere questo. Fai clic sul menu **selezione sandbox**.

![Brand Concierge](./images/bc2.png)

Scegli la sandbox che ti è stata assegnata. La sandbox deve essere denominata `--aepUserLdap-- - bc`.

![Brand Concierge](./images/bc3.png)

Fai clic su **Inizia**.

![Brand Concierge](./images/bc4.png)

Per il nome dell&#39;istanza di Brand Concierge, utilizzare: `--aepUserLdap-- - CitiSignal Brand Concierge`.

Immetti il testo seguente in **Come desideri che faccia il portinaio?**.

```javascript
Brand Concierge should help customers find their best device, plan or entertainment deal. Brand Concierge should help users discover internet plans, entertainment deals,  and help find the best available packages. Brand Concierge should also answer questions about devices such as phones and watches.
```

Fai clic su **Crea**.

![Brand Concierge](./images/bc5.png)

Dovresti vedere questo. Fare clic su **Inizia** per aggiungere un&#39;origine della conoscenza.

![Brand Concierge](./images/bc6.png)

Seleziona **Collegamenti al sito Web** e fai clic su **Continua**.

![Brand Concierge](./images/bc7.png)

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

Dovresti vedere questo. Fai clic su **Portami a casa**.

![Brand Concierge](./images/bc11.png)

Dovresti vedere questo. Fai clic su **Inizia** nella scheda **Product Advisory per i consumatori**.

![Brand Concierge](./images/bc12.png)

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

Gli aggiornamenti vengono salvati automaticamente. Fai clic sulla **freccia** per tornare alla schermata precedente.

![Brand Concierge](./images/bc13.png)

Dovresti vedere questo. Fai clic su **Inizia** per personalizzare l&#39;espressione del brand.

![Brand Concierge](./images/bc14.png)

Puoi effettuare le tue scelte nella pagina **Espressione marchio**, assicurati che sia selezionata un&#39;opzione per ogni domanda.

![Brand Concierge](./images/bc15.png)

Scorri verso il basso e seleziona un&#39;impostazione per il campo **Lunghezza risposta**.

Gli aggiornamenti vengono salvati automaticamente.

![Brand Concierge](./images/bc16.png)

Scorri verso l&#39;alto e fai clic sulla **freccia** per tornare alla schermata precedente.

![Brand Concierge](./images/bc17.png)

Allora tornerai qui. Fare clic su **Origini informazioni**.

![Brand Concierge](./images/bc18.png)

Fai clic su **Genera le tue origini di conoscenza**.

![Brand Concierge](./images/bc19.png)

Seleziona **Catalogo prodotti** e fai clic su **Continua**.

![Brand Concierge](./images/bc20.png)

Dovresti vedere questo. Immetti `CitiSignal Products` come nome per l&#39;origine della conoscenza.

![Brand Concierge](./images/bc21.png)

Ora devi caricare un file csv contenente i collegamenti del tuo sito web. Scarica il catalogo di prodotti [CitiSignal](./assets/CitiSignal-catalog.json.zip) sul desktop e decomprimi.

![Brand Concierge](./images/bc26.png)

Fare clic su **Sfoglia file** e selezionare **Sfoglia dal dispositivo**.

![Brand Concierge](./images/bc22.png)

Seleziona il file **CitiSignal-catalog.json** e fai clic su **Apri**.

![Brand Concierge](./images/bc23.png)

Dovresti vedere questo. Fai clic su **Aggiungi**.

![Brand Concierge](./images/bc24.png)

Allora tornerai qui.

![Brand Concierge](./images/bc25.png)

Dopo 10-20 minuti, lo **Stato** di entrambe le origini di conoscenza deve essere **Completato**. Fare clic su **Home**.

![Brand Concierge](./images/bc27.png)

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

## 1.4.1.3 passaggi per l&#39;onboarding di AEP

Brand Concierge utilizza Adobe Experience Platform per memorizzare i dati di interazione provenienti dalle conversazioni. La connessione tra Brand Concierge e Experience Platform richiede che Brand Concierge configuri e utilizzi un flusso di dati.

### Stream di dati

Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Apri **Experience Platform**.

![Brand Concierge](./images/aep1.png)

Verifica di aver selezionato la sandbox corretta, che deve essere denominata `--aepUserLdap-- - bc`. Nel menu a sinistra, scorri verso il basso e seleziona **Flussi di dati**.

![Brand Concierge](./images/aep2.png)

Fare clic su **Nuovo flusso di dati**.

![Brand Concierge](./images/aep3.png)

Immettere il nome **Datastream** `--aepUserLdap-- - Brand Concierge`, quindi selezionare lo **Schema di mappatura** `cja-brand-concierge-sb-XXX`.

Fai clic su **Salva**.

![Brand Concierge](./images/aep4.png)

Lo stream di dati è ora configurato. Copia il nome e l’ID dello stream di dati e scrivili in un file di testo sul computer.

![Brand Concierge](./images/aep5.png)

### API di gestione della configurazione di Brand Concierge

Il passaggio successivo consiste nell’abilitare l’API di gestione della configurazione di Brand Concierge per configurare lo stream di dati appena creato. Questa operazione è necessaria per risolvere elementi come l’ID organizzazione IMS e i dettagli della sandbox durante l’elaborazione della richiesta.

Questo è attualmente un passaggio interno di Adobe che deve essere eseguito. Questo passaggio è necessario, altrimenti la configurazione dello stream di dati non è corretta per l’utilizzo da parte di Brand Concierge.

Passaggio successivo: [Implementare Brand Concierge nel sito Web](./ex2.md){target="_blank"}

Torna a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}