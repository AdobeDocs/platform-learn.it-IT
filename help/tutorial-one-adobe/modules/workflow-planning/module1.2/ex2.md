---
title: Verifica con Workfront
description: Verifica con Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: da966703aed5342000c19732b6b48682c3958c7f
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# 1.2.2 Strumenti di correzione con Workfront

>[!IMPORTANT]
>
>Se in precedenza hai configurato un programma AEM CS con un ambiente AEM Assets CS, è possibile che la sandbox AEM CS sia stata sospesa. Dato che la disattivazione di una sandbox di questo tipo richiede 10-15 minuti, sarebbe opportuno avviare subito il processo di disattivazione in modo da non doverlo attendere in un secondo momento.

## 1.2.2.1 Crea un nuovo flusso di approvazione

Torna a **Adobe Workfront**. Fai clic sull&#39;icona **menu** e seleziona **Strumenti di correzione**.

![WF](./images/wfp1.png)

Vai a **Flussi di lavoro**, fai clic su **+ Nuovo**, quindi seleziona **Nuovo modello**.

![WF](./images/wfp2.png)

Imposta **Nome modello** su `--aepUserLdap-- - Approval Workflow` e imposta il **Proprietario modello** su se stesso.

![WF](./images/wfp3.png)

Scorri verso il basso e, in **Fasi** > **Fase 1**, modifica il ruolo **Autore bozza** in **Revisore e approvatore**. Puoi anche aggiungere altri utenti, ad esempio se sei un utente e vuoi impostare il **Ruolo** di **Revisore e Approvatore**.

Fai clic su **Crea**.

![WF](./images/wfp4.png)

Il flusso di lavoro di approvazione di base è ora pronto per essere utilizzato.

![WF](./images/wfp5.png)

## 1.2.2.2 Abilita blueprint Workfront

Nel passaggio successivo, creerai un nuovo progetto utilizzando un modello. Adobe Workfront fornisce una serie di blueprint disponibili che richiedono solo l’attivazione.

Per il caso d&#39;uso di CitiSignal, devi utilizzare la blueprint **Integrated Campaign Execution**.

Per installare il blueprint, apri il menu e seleziona **Blueprint**.

![WF](./images/blueprint1.png)

Seleziona il filtro **Marketing**, quindi scorri verso il basso per trovare il blueprint **Integrated Campaign Execution**. Fare clic su **Installa**.

![WF](./images/blueprint2.png)

Fai clic su **Continua**.

![WF](./images/blueprint3.png)

Fare clic su **Installa come è...**.

![WF](./images/blueprint4.png)

Dovresti vedere questo. L&#39;installazione potrebbe richiedere alcuni minuti.

![WF](./images/blueprint5.png)

Dopo un paio di minuti, il blueprint verrà installato.

![WF](./images/blueprint6.png)

## 1.2.2.3 Crea un nuovo progetto

Apri il **menu** e passa a **Programmi**.

![WF](./images/wfp6a.png)

Fare clic sul programma creato in precedenza, denominato `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Hai creato un programma nell&#39;ambito dell&#39;esercizio su [Workfront Planning](./../module1.1/ex1.md) con l&#39;automazione creata ed eseguita. Se non l&#39;avete ancora fatto, potete trovare le istruzioni.

![WF](./images/wfp6b.png)

Nel tuo programma, vai a **Progetti**. Fare clic su **+ Nuovo progetto** e quindi selezionare **Nuovo progetto dal modello**.

![WF](./images/wfp6.png)

Seleziona il modello **Esecuzione campagna integrata** e fai clic su **Usa modello**.

![WF](./images/wfp6g.png)

Dovresti vedere questo. Cambia il nome in `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` e fai clic su **Crea progetto**.

![WF](./images/wfp6c.png)

Il progetto è stato creato. Vai a **Dettagli progetto**.

![WF](./images/wfp6h.png)

Vai a **Dettagli progetto**. Fare clic per selezionare il testo corrente in **Descrizione**.

![WF](./images/wfp6d.png)

Imposta la descrizione su `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Fai clic su **Salva modifiche**.

![WF](./images/wfp6e.png)

Il progetto è ora pronto per essere utilizzato.

![WF](./images/wfp7.png)

Le attività e le dipendenze nel progetto sono state create in base al modello scelto e impostate come. proprietario del progetto. Lo stato del progetto è stato impostato su **Pianificazione**. È possibile modificare lo stato del progetto selezionando un altro valore nell&#39;elenco.

![WF](./images/wfp7z.png)

## 1.2.2.4 Crea una nuova attività

Passa il puntatore del mouse sull&#39;attività **Inizia a creare modelli struttura** e fai clic sui tre punti **...**.

![WF](./images/wfp7a.png)

Selezionare l&#39;opzione **Inserisci attività sotto**.

![WF](./images/wfp7x.png)

Immettere questo nome per l&#39;attività: `Create layout using approved assets and copy`.

Imposta il campo **Assegnazioni** sul ruolo **Designer**.
Imposta il campo **Durata** su **5 giorni**.
Imposta il campo predecessore su **9**.
Immetti una data per i campi **Inizio il** e **Scadenza il**.

Fai clic in un altro punto della schermata per salvare la nuova attività.

![WF](./images/wfp8.png)

Dovresti vedere questo. Fare clic sull&#39;attività per aprirla.

![WF](./images/wfp9.png)

Vai a **dettagli attività** e imposta il campo **Descrizione** su: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Fai clic su **Salva modifiche**.

![WF](./images/wfp9a.png)

Dovresti vedere questo. Fai clic sul campo **Progetto** per tornare al progetto.

![WF](./images/wfp9b.png)

Nella visualizzazione **Progetto**, passa a **Bilanciatore dei carichi di lavoro**.

![WF](./images/wfpwlb1.png)

Fai clic su **Assegnazioni in blocco**.

![WF](./images/wfpwlb2.png)

Seleziona l&#39;**Assegnazione ruolo** di **Designer**, quindi fai clic nel campo **Utente per assegnare**. Verranno visualizzati tutti gli utenti con un ruolo **Designer** nell&#39;istanza di Workfront. In questo caso, seleziona l&#39;utente fittizio **Melissa Jenkins**.

![WF](./images/wfpwlb3.png)

Fai clic su **Assegna**. L&#39;utente selezionato verrà ora assegnato alle attività del progetto collegate al ruolo **Designer**.

![WF](./images/wfpwlb4.png)

Le attività sono ora assegnate. Fai clic su **Attività** per tornare alla pagina della panoramica delle **Attività**.

![WF](./images/wfpwlb5.png)

Fare clic sull&#39;attività creata, denominata
**Crea layout utilizzando risorse approvate e copia**.

![WF](./images/wfpwlb6.png)

Inizierai a lavorare su questa attività come parte di questo esercizio. Puoi vedere che Melissa Jenkins è attualmente assegnata a questa attività. Per modificare l&#39;impostazione, fare clic sul campo **Assegnazioni** e selezionare **Assegna a me**.

![WF](./images/wfpwlb7.png)

Fai clic su **Salva**.

![WF](./images/wfpwlb8.png)

Fai clic su **Lavoraci**.

![WF](./images/wfpwlb9.png)

Dovresti vedere questo.

![WF](./images/wfpwlb10.png)

Come parte di questa attività, devi creare una nuova immagine e quindi caricarla come documento in Workfront. Ora creerai la risorsa da solo utilizzando Adobe Express.

## 1.2.2.5 Aggiungi un nuovo documento al progetto e avvia il flusso di approvazione

Per questo esercizio, devi scaricare e utilizzare questa risorsa: [timetravelnow.png](./images/timetravelnow.png)

![WF](./images/timetravelnow.png)

Vai a **Documenti** per la tua attività. Fare clic su **+ Aggiungi nuovo** e quindi selezionare **Documento**.

![WF](./images/wfp10.png)

Fare clic per selezionare il file `timetravelnow.png`. Fai clic su **Apri**.

![WF](./images/wfp10a.png)

Dovresti avere questo.

![WF](./images/wfp10b.png)

Passa il cursore del mouse sul documento caricato. Fai clic su **Crea bozza** e scegli **Advanced Proof**.

![WF](./images/wfp13.png)

Nella finestra **nuova bozza**, selezionare **Automatizzata**, quindi selezionare il modello di workflow creato in precedenza, che deve essere denominato `--aepUserLdap-- - Approval Workflow`. Fare clic su **Crea bozza**.

![WF](./images/wfp14.png)

Fai clic su **Apri bozza**

![WF](./images/wfp18.png)

È ora possibile rivedere la bozza. Selezionare **Aggiungi commento** per aggiungere un commento che richiede la modifica del documento.

![WF](./images/wfp19.png)

Inserisci il commento e fai clic su **Post**. Fare clic su **Prendi una decisione**.

![WF](./images/wfp20.png)

Seleziona **Modifiche richieste** e fai clic su **prendi decisione**.

![WF](./images/wfp24.png)

Torna alla **Attività** e al **Documento**. Qui verrà visualizzato anche il testo **Modifiche richieste**.

![WF](./images/wfp25.png)

Ora devi apportare modifiche alla progettazione e caricare una nuova versione dell’immagine.

## 1.2.2.6 Aggiungere una nuova versione del documento all&#39;attività

Per questo esercizio, devi scaricare e utilizzare questa risorsa: [getonboard.png](./images/getonboard.png)

![WF](./images/getonboard.png)

Nella vista Attività in Adobe Workfront, seleziona il file immagine precedente che non è stato approvato. Quindi fare clic su **+ Aggiungi nuovo**, selezionare **Versione** e quindi scegliere **Documento**.

![WF](./images/wfp26.png)

Fare clic per selezionare il file `getonboardnow.png`. Fai clic su **Apri**.

![WF](./images/wfp26a.png)

Dovresti avere questo. Fai clic su **Crea bozza**, quindi seleziona di nuovo **Advanced Proof**.

![WF](./images/wfp28.png)

Poi vedrai questo. Il modello di **flusso di lavoro** è ora preselezionato in quanto Workfront presuppone che il flusso di lavoro di approvazione precedente sia ancora valido. Fare clic su **Crea bozza**.

![WF](./images/wfp29.png)

Seleziona **Apri bozza**.

![WF](./images/wfp30.png)

Ora puoi vedere due versioni del file una accanto all’altra. Fare clic sul pulsante **Confronta bozze**.

![WF](./images/wfp31.png)

Dovresti quindi vedere entrambe le versioni dell’immagine una accanto all’altra. Fai clic su **Prendi una decisione**.

![WF](./images/wfp32.png)

Seleziona **Approvato** e fai di nuovo clic su **Prendi decisione**.

![WF](./images/wfp32a.png)

Chiudere la visualizzazione **Confronta bozze** chiudendo la versione a sinistra dell&#39;immagine. Fai clic su **Nome attività** per tornare alla panoramica attività.

![WF](./images/wfp33.png)

Tornerai quindi nella vista Attività, con una risorsa approvata. Questa risorsa ora deve essere condivisa con AEM Assets.

![WF](./images/wfp34.png)

Selezionare il documento approvato. Fai clic sull&#39;icona **Condividi freccia** e seleziona l&#39;integrazione AEM Assets, che deve essere denominata `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![WF](./images/wfp35.png)

Fare doppio clic sulla cartella creata in precedenza, che deve essere denominata `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![WF](./images/wfp36.png)

Fare clic su **Seleziona cartella**.

![WF](./images/wfp37.png)

Dopo 1-2 minuti, il documento verrà pubblicato in AEM Assets. Accanto al nome del documento verrà visualizzata l&#39;icona AEM.

![WF](./images/wfp37a.png)

Fai clic su **Contrassegna come completato** per completare l&#39;attività.

![WF](./images/wfp37b.png)

Dovresti vedere questo.

![WF](./images/wfp37c.png)

## 1.2.2.7 Visualizza il file in AEM Assets

Vai alla cartella in AEM Assets CS, denominata `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![WF](./images/wfppaem1.png)

Selezionare l&#39;immagine, quindi scegliere **Dettagli**.

![WF](./images/wfppaem2.png)

Viene quindi visualizzato il Modulo metadati creato in precedenza, con i valori che sono stati compilati automaticamente dall’integrazione tra Workfront e AEM Assets.

![WF](./images/wfppaem3.png)

Torna a [Gestione dei flussi di lavoro con Adobe Workfront](./workfront.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
