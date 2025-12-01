---
title: Guida introduttiva a Brand Concierge
description: Guida introduttiva a Brand Concierge
kt: 5342
doc-type: tutorial
source-git-commit: 6642acb3fdce2c9d3a9b919d5c9457191e4780a6
workflow-type: tm+mt
source-wordcount: '536'
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

Scegli la sandbox che ti è stata assegnata. La sandbox deve essere denominata `--aepUserLdap--`.

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



```
CitiSignal is a telecommunications company that sells devices such as phones and watches and that sells internet services such as their lead product CitiSignal Fiber Max. On top of that, CitiSignal sells entertainment services that offer premium streaming services at a discounted price. CitiSignal is targeting these 3 personas primarily: Smart Home Families, Online Gamers and Remote Professionals.
```

```
Prioritize positioning the CitiSignal Fiber Max offering.
```

```
Competitor pricing, competitor products
```

Gli aggiornamenti vengono salvati automaticamente. Fai clic sulla **freccia** per tornare alla schermata precedente.

![Brand Concierge](./images/bc13.png)

Dovresti vedere questo. Fai clic su **Inizia** per personalizzare l&#39;espressione del brand.

![Brand Concierge](./images/bc14.png)

Puoi effettuare le tue scelte nella pagina **Espressione marchio**.

![Brand Concierge](./images/bc15.png)

Scorri verso il basso e seleziona un&#39;impostazione per il campo **Lunghezza risposta**.

Gli aggiornamenti vengono salvati automaticamente.

![Brand Concierge](./images/bc16.png)

Scorri verso l&#39;alto e fai clic sulla **freccia** per tornare alla schermata precedente.

![Brand Concierge](./images/bc17.png)


Torna a [Brand Concierge](./brandconcierge.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}