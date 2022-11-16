---
title: 'offer decisioning: utilizza la tua decisione in un’e-mail'
description: Utilizza la tua decisione in un messaggio e-mail
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0fb8c244-1025-479f-b82e-374d1aa5e4dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 11%

---

# 9.5 Utilizza la tua decisione in un messaggio e-mail

In questo esercizio, utilizzerai la tua decisione per personalizzare la consegna di un’e-mail e di un SMS.

Vai a **Percorsi**. Trova il percorso creato nell&#39;esercizio 7.2, denominato `--demoProfileLdap-- - Account Creation Journey`. Fai clic sul percorso per aprirlo.

![Journey Optimizer](./images/emailoffer1.png)

Vedrete questo. Fai clic su **Creare una nuova versione**.

![Journey Optimizer](./images/journey1.png)

Fai clic su **Creare una nuova versione**.

![Journey Optimizer](./images/journey2.png)

Fai clic sul pulsante **E-mail** , quindi fai clic su **Modifica contenuto**.

![Journey Optimizer](./images/journey3.png)

Viene quindi visualizzato il dashboard dei messaggi. Fai clic su **E-mail Designer**.

![Journey Optimizer](./images/emailoffer2.png)

Vedrete questo.

![Journey Optimizer](./images/emailoffer5.png)

Vedrete questo. Trascina un nuovo **Colonna 1:1** componente struttura nell’area di lavoro.

![Journey Optimizer](./images/emailoffer6.png)

Nel menu , vai a **Componenti contenuto**. Seleziona la **Decisione di offerta** , quindi trascina e rilascia questo componente nel segnaposto dell’offerta di contenuti dell’e-mail come indicato. Quindi, fai clic su **Aggiungi**.

![Journey Optimizer](./images/emailoffer7.png)

Seleziona il tipo di posizionamento da includere nell’e-mail. In **Posizionamenti** menu a discesa, seleziona **E-mail - Immagine**, quindi seleziona la tua decisione `--demoProfileLdap-- - Luma Decision`. Fai clic su **Aggiungi**.

![Journey Optimizer](./images/emailoffer8.png)

Ora puoi visualizzare tutte le offerte personalizzate e l’offerta di fallback all’interno della finestra di progettazione e-mail. Fai clic su  **Simula contenuto** per visualizzare in anteprima il messaggio e-mail con un profilo cliente reale.

![Journey Optimizer](./images/emailoffer9.png)

Per iniziare, identifica il profilo da utilizzare per l’anteprima. Seleziona la **email** Inserisci lo spazio dei nomi e l’indirizzo e-mail di un profilo cliente creato sul sito web demo. Quindi, fai clic su **Anteprima**.

![Journey Optimizer](./images/emailoffer10.png)

Una volta visualizzato il messaggio e-mail e visualizzato correttamente l’offerta, fai clic sul pulsante **Chiudi** pulsante .

![Journey Optimizer](./images/emailoffer11.png)

Infine, fai clic su **Salva**.

![Journey Optimizer](./images/emailoffer12.png)

Ora fai clic sulla freccia per tornare alla schermata precedente.

![Journey Optimizer](./images/emailoffer13.png)

Vedrete questo. Fai clic sulla freccia nell&#39;angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/emailoffer14.png)

Fai clic su **Ok** per chiudere **E-mail** azione.

![Journey Optimizer](./images/emailoffer14a.png)

Fai clic su **Pubblica** per pubblicare il percorso aggiornato.

![Journey Optimizer](./images/emailoffer14b.png)

Conferma facendo clic su **Pubblica** di nuovo.

![Journey Optimizer](./images/emailoffer15.png)

Il messaggio è ora pubblicato.

![Journey Optimizer](./images/emailoffer16.png)

Quando crei un nuovo account sul sito web demo, riceverai questa e-mail:

![Journey Optimizer](./images/emailoffer17.png)

Ha finito questo esercizio.

Passaggio successivo: [9.6 Verifica la tua decisione utilizzando l&#39;API](./ex6.md)

[Torna al modulo 9](./offer-decisioning.md)

[Torna a tutti i moduli](./../../overview.md)
