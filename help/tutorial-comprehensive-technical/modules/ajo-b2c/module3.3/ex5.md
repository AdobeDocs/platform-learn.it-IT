---
title: 'Offer decisioning: utilizzare la decisione in un messaggio e-mail'
description: Utilizza la tua decisione in un messaggio e-mail
kt: 5342
doc-type: tutorial
exl-id: 7eddb239-2666-485a-b81a-1f7e6f3aeed2
source-git-commit: fc24f3c9fb1683db35026dc53d0aaa055aa87e34
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 1%

---

# 3.3.5 Utilizzare la propria decisione in un messaggio e-mail

In questo esercizio, utilizzerai la tua decisione per personalizzare la consegna di un’e-mail e di un SMS.

Vai a **Percorsi**. Trovare il percorso creato nell&#39;esercizio 3.1.3, denominato `--aepUserLdap-- - Registration Journey`. Fare clic sul percorso per aprirlo.

![Journey Optimizer](./images/emailoffer1.png)

Poi vedrai questo. Fare clic su **... Altro** e quindi fare clic su **Crea una nuova versione**.

![Journey Optimizer](./images/journey1.png)

Fai clic su **Crea una nuova versione**.

![Journey Optimizer](./images/journey2.png)

Fai clic sull&#39;azione **E-mail** e quindi su **Modifica contenuto**.

![Journey Optimizer](./images/journey3.png)

Viene quindi visualizzata la dashboard dei messaggi. Fai clic su **Modifica corpo dell&#39;e-mail**.

![Journey Optimizer](./images/emailoffer2.png)

Poi vedrai questo. Trascinare un nuovo componente struttura **1:1 column** nell&#39;area di lavoro.

![Journey Optimizer](./images/emailoffer6.png)

Nel menu, vai a **Sommario**. Seleziona il componente **Decisione offerta** e trascina e rilascia questo componente nel segnaposto dell&#39;offerta di contenuto dell&#39;e-mail come indicato. Quindi fare clic su **Aggiungi**.

![Journey Optimizer](./images/emailoffer7.png)

Seleziona il tipo di posizionamento da includere nell’e-mail. Nel menu a discesa **Posizionamenti**, seleziona **E-mail - Immagine**, quindi seleziona la decisione `--aepUserLdap-- - CitiSignal Decision`. Fai clic su **Aggiungi**.

![Journey Optimizer](./images/emailoffer8.png)

Ora puoi passare in rassegna tutte le offerte personalizzate e l’offerta di fallback, tutte visualizzate all’interno dell’e-mail designer. Fai clic su **Salva**.

![Journey Optimizer](./images/emailoffer9.png)

Fare clic sulla freccia per tornare alla schermata precedente.

![Journey Optimizer](./images/emailoffer13.png)

Fai clic sulla freccia nell’angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/emailoffer14.png)

Fai clic su **Salva** per chiudere l&#39;azione **Invia e-mail**.

![Journey Optimizer](./images/emailoffer14a.png)

Fai clic su **Publish** per pubblicare il percorso aggiornato.

![Journey Optimizer](./images/emailoffer14b.png)

Conferma facendo nuovamente clic su **Publish**.

![Journey Optimizer](./images/emailoffer15.png)

Il messaggio è stato pubblicato.

![Journey Optimizer](./images/emailoffer16.png)

Quando crei un nuovo account sul sito web demo, riceverai questa e-mail:

![Journey Optimizer](./images/emailoffer17.png)

Hai finito questo esercizio.

Passaggio successivo: [3.3.6 Verifica la decisione utilizzando l&#39;API](./ex6.md)

[Torna al modulo 3.3](./offer-decisioning.md)

[Torna a tutti i moduli](./../../../overview.md)
