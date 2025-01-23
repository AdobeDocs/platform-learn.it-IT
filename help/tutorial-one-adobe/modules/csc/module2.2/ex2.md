---
title: Verifica con Workfront
description: Verifica con Workfront
kt: 5342
doc-type: tutorial
source-git-commit: 246bb91496104818f357848f41b79523b7771638
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 2.2.2 Strumenti di correzione con Workfront

## 2.2.2.1 Creare un nuovo flusso di approvazione

Vai a [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Fai clic sull&#39;icona dei 9 punti **hamburger** e seleziona **Strumenti di correzione**.

![WF](./images/wfp1.png)

Vai a **Flussi di lavoro**, fai clic su **+ Nuovo**, quindi seleziona **Nuovo modello**.

![WF](./images/wfp2.png)

Imposta **Nome modello** su `--aepUserLdap-- - Approval Workflow` e imposta il **Proprietario modello** su se stesso.

![WF](./images/wfp3.png)

Scorri verso il basso e, in **Stadi** > **Stadio 1**, aggiungi **Wouter Van Geluwe** con il **Ruolo** di **Revisore e Approvatore**.

Fai clic su **Crea**.

![WF](./images/wfp4.png)

Il flusso di lavoro di approvazione di base è ora pronto per essere utilizzato.

![WF](./images/wfp5.png)

## 2.2.2.2 Creare un nuovo progetto

Dalla home page di Workfront, fare clic su **Nuovo** nella scheda **Progetti**. Seleziona **Progetto vuoto**.

![WF](./images/wfp6.png)

Dovresti vedere questo. Cambia il nome in `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6a.png)

Il progetto è stato creato.

![WF](./images/wfp7.png)

## 2.2.2.3 Creare una nuova attività

Immetti questo nome per l&#39;attività: **Crea risorse per la campagna fiber**. Fai clic su **Crea attività**.

![WF](./images/wfp8.png)

Dovresti vedere questo.

![WF](./images/wfp9.png)

## 2.2.2.4 Aggiungere un nuovo documento all’attività per tutta la durata del flusso di approvazione

Fare clic su **+ Aggiungi nuovo** e quindi selezionare **Documento**.

![WF](./images/wfp10.png)

Scarica [questo file](./images/2048x2048.png) sul desktop.

![WF](./images/2048x2048.png){width="50px" align="left"}

Seleziona il file **2048x2048.png** e fai clic su **Apri**.

![WF](./images/wfp12.png)

Dovresti avere questo. Fai clic su **Crea bozza** e scegli **Advanced Proof**.

![WF](./images/wfp13.png)

Nella finestra **nuova bozza** selezionare il modello di workflow creato in precedenza, che deve essere denominato `--aepuserLdap-- - Approval Workflow`. Fare clic su **Crea bozza**.

![WF](./images/wfp14.png)

Tornerai al tuo compito. Fai clic sul pulsante **Assegna a** e seleziona **Assegna a me**.

![WF](./images/wfp15.png)

Fai clic su **Salva**.

![WF](./images/wfp16.png)

Fai clic su **Lavoraci**.

![WF](./images/wfp17.png)

Fai clic su **Apri bozza**

![WF](./images/wfp18.png)

È ora possibile rivedere la bozza. Selezionare **Aggiungi commento** per aggiungere un commento che richiede la modifica del documento.

![WF](./images/wfp19.png)

Inserisci il commento e fai clic su **Post**. Fai clic su **Chiudi**.

![WF](./images/wfp20.png)

Successivamente, devi cambiare il tuo ruolo da **Revisore** a **Revisore e Approvatore**. Per eseguire questa operazione, torna all&#39;attività e fai clic su **Flusso di lavoro di verifica**.

![WF](./images/wfp21.png)

Cambia il tuo ruolo da **Revisore** a **Revisore e Approvatore**.

![WF](./images/wfp22.png)

Torna all’Attività e apri nuovamente la bozza. Viene visualizzato un nuovo pulsante, **Decidi**. Fai clic su di esso.

![WF](./images/wfp23.png)

Seleziona **Modifiche richieste** e fai clic su **prendi decisione**.

![WF](./images/wfp24.png)

Allora dovresti tornare qui. Ora devi caricare una seconda immagine che tenga conto dei commenti forniti.

![WF](./images/wfp25.png)

Scarica [questo file](./images/2048x2048_buynow.png) sul desktop.

![questo file](./images/2048x2048_buynow.png){width="50px" align="left"}

Nella visualizzazione Attività, selezionare il file di immagine precedente che non è stato approvato. Quindi fare clic su **+ Aggiungi nuovo**, selezionare **Versione** e quindi selezionare **Documento**.

![WF](./images/wfp26.png)

Seleziona il file **2048x2048_buynow.png** e fai clic su **Apri**.

![WF](./images/wfp27.png)

Dovresti avere questo. Fai clic su **Crea bozza**, quindi seleziona di nuovo **Advanced Proof**.

![WF](./images/wfp28.png)

Poi vedrai questo. Il modello di **flusso di lavoro** è ora preselezionato in quanto Workfront presuppone che il flusso di lavoro di approvazione precedente sia ancora valido. Fare clic su **Crea bozza**.

![WF](./images/wfp29.png)

Seleziona **Apri bozza**.

![WF](./images/wfp30.png)

Ora puoi vedere due versioni del file una accanto all’altra.

![WF](./images/wfp31.png)

Fai clic su **Prendi una decisione**, seleziona **Approvato**, quindi fai di nuovo clic su **Prendi una decisione**.

![WF](./images/wfp32.png)

Chiudi l’anteprima della bozza.

![WF](./images/wfp33.png)

Tornerai quindi nella vista Attività, con una risorsa approvata. Questa risorsa ora deve essere condivisa con AEM Assets.

![WF](./images/wfp34.png)

Fai clic sull&#39;icona **Condividi freccia** e seleziona l&#39;integrazione AEM Assets, che deve essere denominata `--aepUserLdap-- - Citi Signal AEM`.

![WF](./images/wfp35.png)

Fare doppio clic sulla cartella creata in precedenza, che deve essere denominata `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfp36.png)

Fare clic su **Seleziona cartella**.

![WF](./images/wfp37.png)

Dopo 1-2 minuti, il documento verrà pubblicato in AEM Assets. Accanto al nome del documento verrà visualizzata l&#39;icona AEM.

![WF](./images/wfp37a.png)

Fare clic su **Apri riepilogo**.

![WF](./images/wfp38.png)

Vai a **Metadati**. Dovresti visualizzare:

![WF](./images/wfp39.png)

Vai a **Panoramica** e fai clic su **+ Aggiungi** per aggiungere una descrizione.

![WF](./images/wfp40.png)

Immetti la descrizione. Le impostazioni della bozza e del documento sono completate.

![WF](./images/wfp41.png)

## 2.2.2.5 Visualizza il file in AEM Assets

Vai alla cartella in AEM Assets, denominata `--aepUserLdap - Workfront Assets`.

![WF](./images/wfppaem1.png)

Fai clic sui 3 punti sotto l&#39;immagine, quindi seleziona **Dettagli**.

![WF](./images/wfppaem2.png)

Viene quindi visualizzato il Modulo metadati creato in precedenza, con i valori che sono stati compilati automaticamente dall’integrazione tra Workfront e AEM Assets.

![WF](./images/wfppaem3.png)

[Torna al modulo 2.2](./workfront.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
