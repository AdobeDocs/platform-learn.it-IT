---
title: Guida introduttiva a Workfront, Frame.io ed ESM
description: Guida introduttiva a Workfront, Frame.io ed ESM
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2f9a3eef-16ef-497c-97f7-377ff9ed2f82
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# 1.8.1 Guida introduttiva a Workfront, Frame.io ed ESM

## Terminologia del flusso di lavoro di Workfront 1.8.1.1

Di seguito sono riportati gli oggetti e i concetti principali di Workfront:

| Nome | Ultimo aggiornamento |
| ---------------------- | ------------ | 
| Portfolio | Una raccolta di progetti che hanno caratteristiche unificanti. Questi progetti in genere competono per le stesse risorse, budget o fasce orarie. |
| Programma | Un sottogruppo all’interno di un portfolio, in cui progetti simili possono essere raggruppati per ottenere un beneficio ben definito. |
| Progetto | Una grande quantità di lavoro che deve essere completata in un arco temporale specifico e deve utilizzare un budget specifico e un numero specifico di risorse. Per renderlo gestibile, il progetto viene suddiviso in una serie di attività. Il completamento di tutte le attività comporta il completamento del progetto. |
| Modello di progetto | È possibile utilizzare i modelli di progetto per acquisire la maggior parte dei processi, delle informazioni e delle impostazioni ripetibili associati ai progetti dell&#39;organizzazione. Dopo aver creato i modelli, puoi allegarli ai progetti esistenti o utilizzarli per creare nuovi progetti. |
| Attività | Un’attività che deve essere eseguita come un passaggio verso il raggiungimento di un obiettivo finale (completamento del progetto). Le attività non possono mai esistere indipendentemente. Fanno sempre parte di un progetto. |
| Assegnazione | Un utente, una mansione o un team assegnato a un problema o a un’attività. I progetti, i portfolio o i programmi non possono avere assegnazioni. |
| Documento/Versione | Qualsiasi file allegato a un oggetto in Workfront. Ogni volta che lo stesso documento viene caricato nello stesso oggetto, gli viene assegnato un numero di versione. Gli utenti possono visualizzare e modificare diverse opzioni per una versione precedente di un documento. |
| Approvazione | Per un determinato elemento di lavoro, ad esempio un&#39;attività, un documento o una scheda orario, può essere necessario che un supervisore o un altro utente approvi l&#39;elemento di lavoro. Questo processo di approvazione è denominato approvazione. |


Vai a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Fare clic per aprire **Workfront**.

![Pianificazione Workfront](./images/wfpl1.png)

Poi vedrai questo.

![WF](./images/wfb1.png)

## 1.8.1.2 Abilita blueprint Workfront

Nel passaggio successivo, creerai un nuovo progetto utilizzando un modello. Adobe Workfront fornisce una serie di blueprint disponibili che richiedono solo l’attivazione.

Per il caso d&#39;uso di CitiSignal, devi utilizzare la blueprint **Integrated Campaign Execution**.

Per installare il blueprint, apri il menu e seleziona **Blueprint**.

![WF](./images/blueprint1.png)

Seleziona il filtro **Marketing**, quindi scorri verso il basso per trovare il blueprint **Integrated Campaign Execution**. Fare clic su **Installa**.

![WF](./images/blueprint2.png)

Fai clic su **Continua**.

![WF](./images/blueprint3.png)

Cambia il **nome modello di progetto** in `--aepUserLdap-- - Integrated Campaign Execution`.

Fare clic su **Installa blueprint**.

![WF](./images/blueprint4.png)

Dopo un paio di minuti, il blueprint verrà installato.

![WF](./images/blueprint6.png)

## 1.8.1.3 Crea un nuovo progetto

Apri il **menu** e passa a **Portafogli**.

![WF](./images/wfp6a.png)

Fare clic su **+ Nuovo Portfolio**.

![WF](./images/wfpfolio1.png)

Immettere il nome del portfolio `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfpfolio2.png)

Vai a **Programmi** e fai clic su **+ Nuovo programma**. Seleziona **Nuovo programma**.

![WF](./images/wfnp1.png)

Immettere il nome del programma: `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6b.png)

Nel tuo programma, vai a **Progetti**. Fare clic su **+ Nuovo progetto** e quindi selezionare **Nuovo progetto dal modello**.

![WF](./images/wfp6.png)

Selezionare il modello `--aepUserLdap-- - Integrated Campaign Execution` e fare clic su **Usa modello**.

![WF](./images/wfp6g.png)

Dovresti vedere questo. Cambia il nome in `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` e fai clic su **Crea progetto**.

![WF](./images/wfp6c.png)

Il progetto è stato creato. Vai a **Dettagli progetto**.

![WF](./images/wfp6h.png)

Vai a **Dettagli progetto**. Fare clic per selezionare il testo corrente in **Descrizione**.

Imposta la descrizione su `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Fai clic su **Salva modifiche**.

![WF](./images/wfp6e.png)

Il progetto è ora pronto per essere utilizzato.

![WF](./images/wfp7.png)

Le attività e le dipendenze nel progetto sono state create in base al modello scelto e impostate come. proprietario del progetto. Lo stato del progetto è stato impostato su **Pianificazione**. È possibile modificare lo stato del progetto selezionando un altro valore nell&#39;elenco.

![WF](./images/wfp7z.png)

## 1.8.1.4 visualizzazione progetto in Frame.io

Vai a [https://next.frame.io/](https://next.frame.io/){target="_blank"}. Accedi e seleziona l&#39;istanza da utilizzare in questo esempio **Experience Platform International ESM**. Noterai che esiste già una cartella in Frame.io per il progetto appena creato. La cartella prende il nome dal nome del progetto immesso in precedenza.

Si tratta di una funzione di Enterprise Storage Management, una soluzione di storage basata su cloud che funge da archivio centrale per le risorse tra i prodotti aziendali Adobe, inclusi Workfront e Frame.io.

I principali vantaggi dello storage aziendale Adobe includono:

- Livello di storage unificato per risorse creative e di gestione del lavoro
- Autorizzazioni centralizzate tramite Adobe Identity Management System (IMS) per il controllo sicuro degli accessi
- Visibilità completa delle risorse in Workfront e Frame.io
- Storage scalabile e gestione delle quote per le esigenze aziendali

![WF](./images/fio1.png)

## 1.8.1.5 Crea una nuova attività

Torna a Workfront. Vai a **Attività**, passa il puntatore sull&#39;attività **Inizia a creare modelli struttura** e fai clic sui tre punti **...**.

![WF](./images/wfp7a.png)

Selezionare l&#39;opzione **Inserisci attività sotto**.

![WF](./images/wfp7x.png)

Immettere questo nome per l&#39;attività: `Create layout using approved assets and copy`.

Imposta il campo **Assegnazioni** sul ruolo **Designer**.
Imposta il campo **Durata** su **5 giorni**.
Imposta il campo predecessore su **9**.
Immetti una data per i campi **Inizio il** e **Scadenza il** (la data di inizio di questa attività deve essere pianificata dopo la data di fine dell&#39;attività precedente).

Fai clic in un altro punto della schermata per salvare la nuova attività.

![WF](./images/wfp8.png)

Dovresti vedere questo. Fare clic sull&#39;attività per aprirla.

![WF](./images/wfp9.png)

Vai a **dettagli attività** e imposta il campo **Descrizione** su: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Fai clic su **Salva modifiche**.

![WF](./images/wfp9a.png)

Dovresti vedere questo. Fai clic sul campo **Assegnazioni** e seleziona **Assegna a me**.

![WF](./images/wfpwlb7.png)

Fai clic su **Salva**.

![WF](./images/wfpwlb8.png)

Fai clic su **Lavoraci**.

![WF](./images/wfpwlb9.png)

Dovresti vedere questo.

![WF](./images/wfpwlb10.png)

Come parte di questa attività, è necessario creare una nuova risorsa. Nel passaggio successivo, fornirai innanzitutto le immagini di riferimento in Workfront in modo che l’autore sappia cosa è previsto. Quindi, assumi il ruolo di Designer e creerai tu stesso la risorsa utilizzando Adobe Express.

## 1.8.1.6 Carica immagini di riferimento

Scarica le immagini di riferimento [qui](./assets/reference_images.zip) sul desktop e decomprimi.

![WF](./images/wfrefimg1.png)

In Workfront, passa al livello **Progetto**.

![WF](./images/wfrefimg2.png)

Vai a **Documenti**, fai clic su **+ Aggiungi nuovo**, quindi seleziona **Documento**.

![WF](./images/wfrefimg3.png)

Passare alla cartella scaricata contenente le immagini di riferimento. Seleziona tutte le immagini e fai clic su **Apri**.

![WF](./images/wfrefimg4.png)

Dopo alcuni minuti, tutte le immagini vengono caricate e allegate al progetto.

![WF](./images/wfrefimg5.png)

Con le immagini di riferimento attive, il designer può ora creare la nuova risorsa per questa campagna.

## Passaggi successivi

Passaggio successivo: [Creare una nuova risorsa, rivederla e approvarla](./ex2.md){target="_blank"}

Torna a [Revisione e approvazione unificate con Workfront, Frame.io e Enterprise Storage Management](./esm.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
