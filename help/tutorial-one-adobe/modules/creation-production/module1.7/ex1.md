---
title: Guida introduttiva a Firefly Creative Production for Enterprise
description: Guida introduttiva a Firefly Creative Production for Enterprise
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 7d9ad7ec-7744-4ba6-9c11-c434e6cdef09
source-git-commit: 7850713bf116c8a9aa9dc4e055d0e501aa783cb0
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---

# 1.7.1 Guida introduttiva a Firefly Creative Production for Enterprise

Vai a [https://firefly.adobe.com](https://firefly.adobe.com). Fai clic sull&#39;icona del profilo nell&#39;angolo in alto a destra e verifica di aver selezionato l&#39;istanza corretta, che dovrebbe essere `--aepImsOrgName--`.

Vai a **Produzione**.

![Firefly Creative Production for Enterprise](./images/ffcw1.png)

Dovresti vedere questo. Fai clic su **Crea flusso di lavoro (versione beta)**.

![Firefly Creative Production for Enterprise](./images/ffcw2.png)

## 1.7.1.1 Rimuovi sfondo

Per conoscere Firefly Creative Production for Enterprise, ora implementerai un caso d’uso di base incentrato sulla rimozione dello sfondo di un’immagine specifica.

Cambia il nome del flusso di lavoro in `vangeluw - remove background`.

![Firefly Creative Production for Enterprise](./images/ffcw3.png)

Apri **Immagine**

![Firefly Creative Production for Enterprise](./images/ffcw4.png)

Seleziona **Rimuovi sfondo**, quindi trascina questo nodo nell&#39;area di lavoro.

È ora necessario collegare un nodo immagine di input e un nodo immagine di output a **Rimuovi sfondo**.

![Firefly Creative Production for Enterprise](./images/ffcw5.png)

Scorri verso l&#39;alto e passa a **Input e output**. Fare clic sul nodo **Immagini di input** e trascinarlo nell&#39;area di lavoro.

![Firefly Creative Production for Enterprise](./images/ffcw6.png)

Dovresti avere questo. **&#x200B;**&#x200B;**&#x200B;**&#x200B;**&#x200B;**&#x200B;**&#x200B;**&#x200B;**&#x200B;**&#x200B;**&#x200B;**

![](./images/ffcw7.png)

You should then have this. Fare clic sul nodo **Immagini di output** e trascinarlo nell&#39;area di lavoro.

![Firefly Creative Production for Enterprise](./images/ffcw8.png)

Dovresti avere questo. Connetti il nodo **Rimuovi sfondo** al nodo **Immagini di output** passando il puntatore del mouse sul punto blu accanto a **Immagine di output** nel nodo **Rimuovi sfondo** e disegnando una linea con il punto blu accanto a **Immagine** nel nodo **Immagini di output**.

![Firefly Creative Production for Enterprise](./images/ffcw9.png)

Dovresti avere questo.

![Firefly Creative Production for Enterprise](./images/ffcw10.png)

Il flusso di lavoro di base è ora pronto per il test. Scarica l&#39;immagine [phone.png](./assets/phone.png) sul desktop.

![Firefly Creative Production for Enterprise](./images/ffcw11.png)

Torna al workflow. Fai clic sull&#39;area **Trascina e rilascia** del nodo **Immagini di input**.

![Firefly Creative Production for Enterprise](./images/ffcw11a.png)

Selezionare il file **phone.png**. Fai clic su **Apri**.

![Firefly Creative Production for Enterprise](./images/ffcw12.png)

Dovresti vedere questo. Fare clic su **Esegui**.

![Firefly Creative Production for Enterprise](./images/ffcw13.png)

Dopo 1-2 minuti, dovresti vedere questo risultato.

![Firefly Creative Production for Enterprise](./images/ffcw14.png)

## 1.7.1.2 Rimuovi sfondo + Ritaglia

È ora necessario aggiungere un nodo **Ritaglio** all&#39;area di lavoro. Nel menu, vai a **Immagine** e scorri verso il basso per trovare **Ritaglio**. Trascinalo nell’area di lavoro.

![Firefly Creative Production for Enterprise](./images/ffcw15.png)

Posiziona il nodo **Ritaglia** tra il nodo **Rimuovi sfondo** e il nodo **Immagine di output**.

È ora necessario rimuovere la connessione tra il nodo **Rimuovi sfondo** e il nodo **Immagine di output**. A tale scopo, fare doppio clic sulla linea tra i due nodi.

![Firefly Creative Production for Enterprise](./images/ffcw16.png)

Dovresti avere questo. Connetti il nodo **Rimuovi sfondo** al nodo **Ritaglia**, quindi connetti il nodo **Ritaglia** al nodo **Immagine di output**.

![Firefly Creative Production for Enterprise](./images/ffcw17.png)

Seleziona la casella di controllo per **Ritaglio automatico**, quindi puoi verificare il flusso di lavoro facendo clic su **Esegui**.

![Firefly Creative Production for Enterprise](./images/ffcw18.png)

Dopo 1-2 minuti, dovresti vedere questo, che mostra ora un&#39;immagine con una risoluzione diversa.

![Firefly Creative Production for Enterprise](./images/ffcw19.png)

## 1.7.1.3 Rimuovi sfondo + Ritaglio + Immagine composita

Nel menu, in **Immagine** seleziona un nodo **Immagini composite (2D)** e trascinalo nell&#39;area di lavoro.

![Firefly Creative Production for Enterprise](./images/ffcw20.png)

Aggiungi una seconda connessione al nodo **Ritaglia**, connettendo il punto blu accanto a **Immagine ritagliata** al punto blu accanto a **Immagine di input** nel nodo **Immagini composite (2D)**.

![Firefly Creative Production for Enterprise](./images/ffcw21.png)

Nel menu, in **Input e Output**, seleziona un nodo **Testo di input** e trascinalo nell&#39;area di lavoro.

Connetti il punto verde accanto a **Testo** nel nodo **Testo di input** al punto verde accanto a **Prompt** nel nodo **Immagini composite (2D)**.

![Firefly Creative Production for Enterprise](./images/ffcw22.png)

Dovresti avere questo. Immettere il seguente prompt nel nodo **Testo di input**.

`magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts`

Nel menu, in **Input e Output**, seleziona un nodo **Immagini di output** e trascinalo nell&#39;area di lavoro.

Connetti il punto blu accanto a **Immagine composita** nel nodo **Immagini composte (2D)** al punto blu accanto a **Immagine di input** nel nodo **Immagine di output**.

Fare clic su **Esegui**.

![Firefly Creative Production for Enterprise](./images/ffcw23.png)

Dopo un paio di minuti, dovresti vedere qualcosa di simile a questo, che mostra l’immagine originale in una composizione in base al prompt fornito, in una risoluzione specifica.

![Firefly Creative Production for Enterprise](./images/ffcw24.png)

## 1.7.1.4 Rimuovi sfondo + Ritaglio + Immagine composita + Genera video

Nel menu, vai a **Video**. Selezionare il nodo **Genera video** e trascinarlo nell&#39;area di lavoro.

Connetti il punto blu accanto a **Immagine composita** del nodo **Immagini composte (2D)** al punto blu accanto a **Immagine di input** del nodo **Genera video**.

![Firefly Creative Production for Enterprise](./images/ffcw25.png)

Nel menu, vai a **Input e Output**. Selezionare il nodo **Testo di input** e trascinarlo nell&#39;area di lavoro.

Connetti il punto verde accanto a **Testo** nel nodo **Testo di input** al punto verde accanto a **Prompt** del nodo **Genera video**.

Immettere il prompt `background hearts fluttering` nel nodo **Testo di input**.

Nel menu, vai a **Input e Output**. Selezionare il nodo **Video di output** e trascinarlo nell&#39;area di lavoro.

Connetti il punto viola accanto a **Output video** del nodo **Genera video** al punto viola accanto a **Video** nel nodo **Video output**.

**&#x200B;**

![](./images/ffcw26.png)

Dopo un paio di video, dovresti vedere questo che mostra un video basato sulla combinazione dell’immagine e del prompt forniti.

![Firefly Creative Production for Enterprise](./images/ffcw27.png)

## Scala 1.7.1.5

Questo è stato fatto per 1 immagine. Ora usiamo questo flusso di lavoro, ma per più immagini.

Scarica queste immagini sul desktop:

- [watch.jpg](./assets/watch.jpg)
- [airpods.jpg](./assets/airpods.jpg)

![Firefly Creative Production for Enterprise](./images/ffcw28.png)

Nel flusso di lavoro, torna al primo nodo, **Immagini di input**. Rimuovi l&#39;immagine attualmente selezionata.

![Firefly Creative Production for Enterprise](./images/ffcw29.png)

Fai clic sull&#39;area **Trascina e rilascia**.

![Firefly Creative Production for Enterprise](./images/ffcw30.png)

Seleziona le 3 immagini scaricate. Fai clic su **Apri**.

![Firefly Creative Production for Enterprise](./images/ffcw31.png)

You should then see this. **&#x200B;**

![](./images/ffcw32.png)

Dopo alcuni minuti, dovresti vedere un output simile, con 3 immagini generate e 3 video.

![Firefly Creative Production for Enterprise](./images/ffcw33.png)

## Archivio 1.7.1.5 in AEM Assets CS

In questo esercizio memorizzerete le risorse create come parte del flusso di lavoro personalizzato in AEM Assets CS.

Devi innanzitutto creare una nuova cartella nell’ambiente AEM Assets CS.

Per eseguire questa operazione, vai a [https://experience.adobe.com](https://experience.adobe.com). Fare clic per aprire **Experience Manager Assets**.

![Firefly Creative Production for Enterprise](./images/ffcw50.png)

Seleziona l&#39;ambiente AEM Assets CS, che deve essere denominato `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![Firefly Creative Production for Enterprise](./images/ffcw51.png)

Vai a **Assets** e fai clic su **Crea cartella**.

![Firefly Creative Production for Enterprise](./images/ffcw52.png)

Immettere il nome: `--aepUserLdap-- - Firefly Creative Production for Enterprise`. Fai clic su **Crea**.

![Firefly Creative Production for Enterprise](./images/ffcw53.png)

Torna al flusso di lavoro personalizzato e passa al nodo **Immagini di output**. Fai clic su **Predefinito**, quindi seleziona **AEM Assets**.

![Firefly Creative Production for Enterprise](./images/ffcw57.png)

Dovresti vedere questo pop-up. Selezionare l&#39;archivio AEM Assets CS, quindi selezionare la cartella appena creata, che deve essere denominata: `--aepUserLdap-- - Firefly Creative Production for Enterprise`. Fai clic su **Seleziona**.

![Firefly Creative Production for Enterprise](./images/ffcw54.png)

Vai al nodo **Video di output**. Fai clic su **Predefinito**, quindi seleziona **AEM Assets**.

![Firefly Creative Production for Enterprise](./images/ffcw55.png)

Dovresti vedere questo pop-up. Selezionare l&#39;archivio AEM Assets CS, quindi selezionare la cartella appena creata, che deve essere denominata: `--aepUserLdap-- - Firefly Creative Production for Enterprise`. Fai clic su **Seleziona**.

![Firefly Creative Production for Enterprise](./images/ffcw56.png)

Dovresti avere questo. Fare clic su **Esegui**.

![Firefly Creative Production for Enterprise](./images/ffcw56a.png)

Dopo un paio di minuti, le risorse create dovrebbero diventare disponibili nella cartella in AEM Assets CS.

![Firefly Creative Production for Enterprise](./images/ffcw58.png)

Torna al workflow. Fai clic su **Pubblica**.

![Firefly Creative Production for Enterprise](./images/ffcw59.png)

Dovresti vedere questo.

![Firefly Creative Production for Enterprise](./images/ffcw60.png)

Il flusso di lavoro viene ora pubblicato e può essere eseguito programmaticamente come parte dell’esercizio successivo.

## Passaggi successivi

Vai a [1.7.2 Esegui il flusso di lavoro personalizzato a livello di programmazione](./ex2.md){target="_blank"}

Torna a [Firefly Creative Production for Enterprise](./workflowbuilder.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
