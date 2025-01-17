---
title: Automazione dei processi con Workfront Fusion
description: Automazione dei processi con Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: f1f70a0e4ea3f59b5b121275e7db633caf953df9
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# 1.2.3 Automazione dei processi con Workfront Fusion

Il tuo scenario ora si presenta così.

![WF Fusion](./images/wffusion200.png)

## 1.2.3.1 Iterazione su più valori

Finora hai modificato il testo in un file Photoshop di un valore statico. Per ridimensionare e automatizzare i flussi di lavoro di creazione dei contenuti, è necessario scorrere un elenco di valori e inserirli in modo dinamico nel file Photoshop. Nei passaggi successivi, aggiungerai un messaggio per eseguire iterazioni sui valori nello scenario esistente.

Tra il nodo **Router** e il nodo **Testo modifica Photoshop**, fare clic sull&#39;icona **chiave inglese** e selezionare **Aggiungi modulo**.

![WF Fusion](./images/wffusion201.png)

Cercare `flow` e selezionare **Controllo flusso**.

![WF Fusion](./images/wffusion202.png)

Selezionare **Iteratore**.

![WF Fusion](./images/wffusion203.png)

Dovresti avere questo.

![WF Fusion](./images/wffusion204.png)

Anche se è possibile leggere file di input come i file CSV, per il momento devi utilizzare una versione di base di un file CSV definendo una stringa di testo e dividendo il file di testo.

Per trovare la funzione **split**, fai clic sull&#39;icona **T**, in cui sono visualizzate tutte le funzioni disponibili per manipolare i valori di testo. Fai clic sulla funzione **split** per visualizzarla.

![WF Fusion](./images/wffusion206.png)

La funzione split prevede una matrice di valori prima del punto e virgola e specifica il separatore dopo il punto e virgola. Per questo test, è necessario utilizzare un array semplice con 2 campi, **Acquista ora** e **Fai clic qui** e il separatore da utilizzare è **,**.

Immetti questo valore nel campo **Array** sostituendo la funzione **split** attualmente vuota: `{{split("Buy now, Click here "; ",")}}`. Fai clic su **OK**.

![WF Fusion](./images/wffusion205.png)

L’iteratore è ora configurato e, se esegui ora lo scenario, lo eseguirebbe due volte. Si è verificato comunque un problema, poiché si stanno utilizzando valori statici nel nodo **Testo di modifica Photoshop**. Fare clic su **Testo modifica Photoshop** per aggiungere alcune variabili anziché valori statici per i campi di input e output.

![WF Fusion](./images/wffusion207.png)

Nel **Contenuto richiesta**, verrà visualizzato il testo **Fare clic qui**. Questo testo deve essere sostituito dai valori provenienti dall’array.

![WF Fusion](./images/wffusion208.png)

Eliminare il testo **Fare clic qui** e sostituirlo selezionando la variabile **Value** dal nodo **Iterator**. In questo modo il testo sul pulsante nel documento Photoshop verrà aggiornato in modo dinamico.

![WF Fusion](./images/wffusion209.png)

È inoltre necessario aggiornare il nome del file utilizzato per scrivere il file nell’account di archiviazione Azure. Se il nome del file è statico, ogni nuova iterazione sovrascriverà semplicemente il file precedente e come tale, perderai i file personalizzati. Il nome del file statico corrente è **citisignal-fiber-changed-text.psd** ed è ora necessario aggiornarlo. Posizionare il cursore dietro la parola `text`.

![WF Fusion](./images/wffusion210.png)

Aggiungere un trattino `-`, quindi selezionare il valore **Posizione ordine bundle**. In questo modo, per la prima iterazione, Workfront Fusion aggiungerà `-1` al nome del file, per la seconda iterazione `-2` e così via. Fai clic su **OK**.

![WF Fusion](./images/wffusion211.png)

Salva lo scenario e fai clic su **Esegui una volta**.

![WF Fusion](./images/wffusion212.png)

Una volta eseguito lo scenario, torna ad Azure Storage Explorer e aggiorna la cartella. Dovresti quindi visualizzare i 2 file appena creati.

![WF Fusion](./images/wffusion213.png)

Scarica e apri ciascun file. Dovresti quindi vedere i vari testi sui pulsanti. Questo è il file `citisignal-fiber-changed-text-1.psd`.

![WF Fusion](./images/wffusion214.png)

Questo è il file `citisignal-fiber-changed-text-2.psd`.

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2 Attiva lo scenario utilizzando un webhook

Finora lo scenario è stato eseguito manualmente per essere testato. Aggiorniamo ora lo scenario con un webhook, in modo che possa essere attivato da un ambiente esterno.

Fai clic sull&#39;icona **+**, cerca **webhook**, quindi seleziona **Webhook**.

![WF Fusion](./images/wffusion216.png)

Seleziona **WebHook personalizzato**.

Trascinare e connettere il nodo **Webhook personalizzato** in modo che si connetta al primo nodo dell&#39;area di lavoro, denominato **Inizializza costanti**.

![WF Fusion](./images/wffusion217.png)

Fai clic sul nodo **Webhook personalizzato**. Quindi fare clic su **Aggiungi**.

![WF Fusion](./images/wffusion218.png)

Imposta **Nome webhook** su `--aepUserLdap-- - Tutorial 1.2`.

![WF Fusion](./images/wffusion219.png)

Seleziona la casella di controllo per **Ottieni intestazioni richiesta**. Fai clic su **Salva**.

![WF Fusion](./images/wffusion220.png)

L’URL del webhook è ora disponibile. Copia l’URL.

![WF Fusion](./images/wffusion221.png)

Apri Postman e aggiungi una nuova cartella nella raccolta **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Denomina la cartella `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

Nella cartella appena creata, fai clic sui tre punti **...** e seleziona **Aggiungi richiesta**.

![WF Fusion](./images/wffusion224.png)

Imposta **Tipo di metodo** su **POST** e incolla l&#39;URL del webhook nella barra degli indirizzi.

![WF Fusion](./images/wffusion225.png)

È necessario inviare un corpo personalizzato, in modo che gli elementi della variabile possano essere forniti da un’origine esterna allo scenario Workfront Fusion. Vai a **Body** e seleziona **raw**.

![WF Fusion](./images/wffusion226.png)

Incolla il testo seguente nel corpo della richiesta. Fai clic su **Invia**.

```json
{
    "psdTemplate": "placeholder",
    "xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

Tornare a Workfront Fusion. Nel webhook personalizzato verrà visualizzato un messaggio con il seguente messaggio: **Determinato correttamente**.

![WF Fusion](./images/wffusion227.png)

Fare clic su **Salva** e quindi su **Esegui una volta**. Il tuo scenario sarà ora attivo ma non verrà eseguito finché non farai di nuovo clic su **Invia** in Postman.

![WF Fusion](./images/wffusion230.png)

Vai a Postman e fai di nuovo clic su **Invia**.

![WF Fusion](./images/wffusion228.png)

Lo scenario verrà quindi eseguito di nuovo e creerà i 2 file come in precedenza.

![WF Fusion](./images/wffusion232.png)

Modifica il nome della richiesta Postman in `POST - Send Request to Workfront Fusion Webhook`.

![WF Fusion](./images/wffusion233.png)

Ora devi iniziare a utilizzare la variabile **psdTemplate**. Invece di codificare la posizione del file di input nel nodo **Testo di modifica di Photoshop**, verrà ora utilizzata la variabile in ingresso della richiesta di Postman.

Apri il nodo **Testo modifica Photoshop** e passa a **Contenuto richiesta**. Selezionare il nome di file hardcoded **citisignal-fiber.psd** in **inputs** ed eliminarlo.

![WF Fusion](./images/wffusion234.png)

Selezionare la variabile **psdTemplate**. Fai clic su **OK** e quindi salva lo scenario.

![WF Fusion](./images/wffusion235.png)

Fai clic su **ON** per attivare lo scenario. Lo scenario verrà eseguito senza interruzioni.

![WF Fusion](./images/wffusion236.png)

Torna a Postman. Immetti il nome file `citisignal-fiber.psd` come valore per la variabile **psdTemplate** e fai di nuovo clic su **Invia** per eseguire di nuovo lo scenario.

![WF Fusion](./images/wffusion237.png)

Specificando il modello di PSD come variabile fornita da un sistema esterno, è stato creato uno scenario riutilizzabile.

Hai terminato questo esercizio.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 1.2](./automation.md)

[Torna a tutti i moduli](./../../../overview.md)
