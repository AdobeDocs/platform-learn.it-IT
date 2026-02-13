---
title: Guida introduttiva ai flussi di lavoro personalizzati per Firefly
description: Guida introduttiva ai flussi di lavoro personalizzati per Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 7d9ad7ec-7744-4ba6-9c11-c434e6cdef09
source-git-commit: 5fe2f1c413f54dd1e3c67d78460d7f2a84248005
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# 1.7.1 Guida introduttiva ai flussi di lavoro personalizzati Firefly

[!BADGE Beta]

+++Dettagli Beta
Con l&#39;utilizzo del Beta per flussi di lavoro personalizzati Firefly, l&#39;utente riconosce che il Beta viene fornito &quot;così com&#39;è&quot; senza alcuna garanzia. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Beta. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Beta e/o dei materiali di accompagnamento. Beta è considerata un&#39;informazione riservata di Adobe.  Qualsiasi &quot;Feedback&quot; (informazioni relative a Beta, compresi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

+++

Vai a [https://firefly.adobe.com](https://firefly.adobe.com). Fai clic sull&#39;icona del profilo nell&#39;angolo in alto a destra e verifica di aver selezionato l&#39;istanza corretta, che dovrebbe essere `--aepImsOrgName--`.

Vai a **Produzione**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw1.png)

Dovresti vedere questo. Fai clic su **Crea flusso di lavoro (versione beta)**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw2.png)

## 1.7.1.1 Rimuovi sfondo

Per conoscere i flussi di lavoro personalizzati di Firefly, ora implementerai un caso d’uso di base incentrato sulla rimozione dello sfondo di un’immagine specifica.

Cambia il nome del flusso di lavoro in `vangeluw - remove background`.

![Flussi di lavoro personalizzati Firefly](./images/ffcw3.png)

Apri **Immagine**

![Flussi di lavoro personalizzati Firefly](./images/ffcw4.png)

Seleziona **Rimuovi sfondo**, quindi trascina questo nodo nell&#39;area di lavoro.

È ora necessario collegare un nodo immagine di input e un nodo immagine di output a **Rimuovi sfondo**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw5.png)

Scorri verso l&#39;alto e passa a **Input e output**. Fare clic sul nodo **Immagini di input** e trascinarlo nell&#39;area di lavoro.

![Flussi di lavoro personalizzati Firefly](./images/ffcw6.png)

Dovresti avere questo. Connetti il nodo **Immagini di input** al nodo **Rimuovi sfondo** passando il puntatore del mouse sul punto blu accanto a **Immagine** nel nodo **Immagini di input** e disegnando una linea con il punto blu accanto a **Immagine di input** nel nodo **Rimuovi sfondo**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw7.png)

Dovresti avere questo. Fare clic sul nodo **Immagini di output** e trascinarlo nell&#39;area di lavoro.

![Flussi di lavoro personalizzati Firefly](./images/ffcw8.png)

Dovresti avere questo. Connetti il nodo **Rimuovi sfondo** al nodo **Immagini di output** passando il puntatore del mouse sul punto blu accanto a **Immagine di output** nel nodo **Rimuovi sfondo** e disegnando una linea con il punto blu accanto a **Immagine** nel nodo **Immagini di output**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw9.png)

Dovresti avere questo.

![Flussi di lavoro personalizzati Firefly](./images/ffcw10.png)

Il flusso di lavoro di base è ora pronto per il test. Scarica l&#39;immagine [phone.png](./assets/phone.png) sul desktop.

![Flussi di lavoro personalizzati Firefly](./images/ffcw11.png)

Torna al workflow. Fai clic sull&#39;area **Trascina e rilascia** del nodo **Immagini di input**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw11a.png)

Selezionare il file **phone.png**. Fai clic su **Apri**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw12.png)

Dovresti vedere questo. Fare clic su **Esegui**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw13.png)

Dopo 1-2 minuti, dovresti vedere questo risultato.

![Flussi di lavoro personalizzati Firefly](./images/ffcw14.png)

## 1.7.1.2 Rimuovi sfondo + Ritaglia

È ora necessario aggiungere un nodo **Ritaglio** all&#39;area di lavoro. Nel menu, vai a **Immagine** e scorri verso il basso per trovare **Ritaglio**. Trascinalo nell’area di lavoro.

![Flussi di lavoro personalizzati Firefly](./images/ffcw15.png)

Posiziona il nodo **Ritaglia** tra il nodo **Rimuovi sfondo** e il nodo **Immagine di output**.

È ora necessario rimuovere la connessione tra il nodo **Rimuovi sfondo** e il nodo **Immagine di output**. A tale scopo, fare doppio clic sulla linea tra i due nodi.

![Flussi di lavoro personalizzati Firefly](./images/ffcw16.png)

Dovresti avere questo. Connetti il nodo **Rimuovi sfondo** al nodo **Ritaglia**, quindi connetti il nodo **Ritaglia** al nodo **Immagine di output**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw17.png)

Seleziona la casella di controllo per **Ritaglio automatico**, quindi puoi verificare il flusso di lavoro facendo clic su **Esegui**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw18.png)

Dopo 1-2 minuti, dovresti vedere questo, che mostra ora un&#39;immagine con una risoluzione diversa.

![Flussi di lavoro personalizzati Firefly](./images/ffcw19.png)

## 1.7.1.3 Rimuovi sfondo + Ritaglio + Immagine composita

Nel menu, in **Immagine** seleziona un nodo **Immagini composite (2D)** e trascinalo nell&#39;area di lavoro.

![Flussi di lavoro personalizzati Firefly](./images/ffcw20.png)

Aggiungi una seconda connessione al nodo **Ritaglia**, connettendo il punto blu accanto a **Immagine ritagliata** al punto blu accanto a **Immagine di input** nel nodo **Immagini composite (2D)**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw21.png)

Nel menu, in **Input e Output**, seleziona un nodo **Testo di input** e trascinalo nell&#39;area di lavoro.

Connetti il punto verde accanto a **Testo** nel nodo **Testo di input** al punto verde accanto a **Prompt** nel nodo **Immagini composite (2D)**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw22.png)

Dovresti avere questo. Immettere il seguente prompt nel nodo **Testo di input**.

`magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts`

Nel menu, in **Input e Output**, seleziona un nodo **Immagini di output** e trascinalo nell&#39;area di lavoro.

Connetti il punto blu accanto a **Immagine composita** nel nodo **Immagini composte (2D)** al punto blu accanto a **Immagine di input** nel nodo **Immagine di output**.

Fare clic su **Esegui**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw23.png)

Dopo un paio di minuti, dovresti vedere qualcosa di simile a questo, che mostra l’immagine originale in una composizione in base al prompt fornito, in una risoluzione specifica.

![Flussi di lavoro personalizzati Firefly](./images/ffcw24.png)

## 1.7.1.4 Rimuovi sfondo + Ritaglio + Immagine composita + Genera video

Nel menu, vai a **Video**. Selezionare il nodo **Genera video** e trascinarlo nell&#39;area di lavoro.

Connetti il punto blu accanto a **Immagine composita** del nodo **Immagini composte (2D)** al punto blu accanto a **Immagine di input** del nodo **Genera video**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw25.png)

Nel menu, vai a **Input e Output**. Selezionare il nodo **Testo di input** e trascinarlo nell&#39;area di lavoro.

Connetti il punto verde accanto a **Testo** nel nodo **Testo di input** al punto verde accanto a **Prompt** del nodo **Genera video**.

Immettere il prompt `background hearts fluttering` nel nodo **Testo di input**.

Nel menu, vai a **Input e Output**. Selezionare il nodo **Video di output** e trascinarlo nell&#39;area di lavoro.

Connetti il punto viola accanto a **Output video** del nodo **Genera video** al punto viola accanto a **Video** nel nodo **Video output**.

Fare clic su **Esegui**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw26.png)

Dopo un paio di video, dovresti vedere questo che mostra un video basato sulla combinazione dell’immagine e del prompt forniti.

![Flussi di lavoro personalizzati Firefly](./images/ffcw27.png)

## Scala 1.7.1.5

Questo è stato fatto per 1 immagine. Ora usiamo questo flusso di lavoro, ma per più immagini.

Scarica queste immagini sul desktop:

- [watch.jpg](./assets/watch.jpg)
- [airpods.jpg](./assets/airpods.jpg)

![Flussi di lavoro personalizzati Firefly](./images/ffcw28.png)

Nel flusso di lavoro, torna al primo nodo, **Immagini di input**. Rimuovi l&#39;immagine attualmente selezionata.

![Flussi di lavoro personalizzati Firefly](./images/ffcw29.png)

Fai clic sull&#39;area **Trascina e rilascia**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw30.png)

Seleziona le 3 immagini scaricate. Fai clic su **Apri**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw31.png)

Dovresti vedere questo. fare clic su **Esegui**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw32.png)

Dopo alcuni minuti, dovresti vedere un output simile, con 3 immagini generate e 3 video.

![Flussi di lavoro personalizzati Firefly](./images/ffcw33.png)

## Archivio 1.7.1.5 in AEM Assets CS

In questo esercizio memorizzerete le risorse create come parte del flusso di lavoro personalizzato in AEM Assets CS.

Devi innanzitutto creare una nuova cartella nell’ambiente AEM Assets CS.

Per eseguire questa operazione, vai a [https://experience.adobe.com](https://experience.adobe.com). Fare clic per aprire **Experience Manager Assets**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw50.png)

Seleziona l&#39;ambiente AEM Assets CS, che deve essere denominato `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![Flussi di lavoro personalizzati Firefly](./images/ffcw51.png)

Vai a **Assets** e fai clic su **Crea cartella**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw52.png)

Immettere il nome: `--aepUserLdap-- - Firefly Custom Workflows`. Fai clic su **Crea**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw53.png)

Torna al flusso di lavoro personalizzato e passa al nodo **Immagini di output**. Fai clic su **Predefinito**, quindi seleziona **AEM Assets**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw57.png)

Dovresti vedere questo pop-up. Selezionare l&#39;archivio AEM Assets CS, quindi selezionare la cartella appena creata, che deve essere denominata: `--aepUserLdap-- - Firefly Custom Workflows`. Fai clic su **Seleziona**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw54.png)

Vai al nodo **Video di output**. Fai clic su **Predefinito**, quindi seleziona **AEM Assets**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw55.png)

Dovresti vedere questo pop-up. Selezionare l&#39;archivio AEM Assets CS, quindi selezionare la cartella appena creata, che deve essere denominata: `--aepUserLdap-- - Firefly Custom Workflows`. Fai clic su **Seleziona**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw56.png)

Dovresti avere questo. Fare clic su **Esegui**.

![Flussi di lavoro personalizzati Firefly](./images/ffcw56a.png)

Dopo un paio di minuti, le risorse create dovrebbero diventare disponibili nella cartella in AEM Assets CS.

![Flussi di lavoro personalizzati Firefly](./images/ffcw58.png)

## Passaggi successivi

Torna a [Workflow Builder](./workflowbuilder.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
