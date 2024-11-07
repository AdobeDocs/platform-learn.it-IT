---
title: 'Adobe Journey Optimizer: applicare la personalizzazione a un messaggio e-mail'
description: Questo esercizio spiega come utilizzare la personalizzazione dei segmenti all’interno di un contenuto e-mail
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 3.4.3 Applicare la personalizzazione in un messaggio e-mail

Accedi a Adobe Experience Cloud da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Adobe Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepTenantId--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.3.1 Personalizzazione basata su segmenti

In questo esercizio migliorerai il messaggio e-mail per la newsletter con un testo personalizzato in base all’iscrizione al segmento.

Vai a **Percorsi**. Trova il percorso di newsletter creato nell’esercizio precedente. Cerca `--demoProfileLdap-- - Newsletter`. Fare clic sul percorso per aprirlo.

![Journey Optimizer](./images/sbp1.png)

Poi vedrai questo. Fai clic su **Duplica**.

![Journey Optimizer](./images/sbp2.png)

Fai clic su **Duplica**.

![Journey Optimizer](./images/sbp3.png)

Seleziona l&#39;azione **Invia e-mail** e fai clic su **Modifica contenuto**.

![Journey Optimizer](./images/sbp3a.png)

Fai clic su **Invia e-mail a Designer**.

![Journey Optimizer](./images/sbp4.png)

Poi vedrai questo.

![Journey Optimizer](./images/sbp5.png)

Apri **Componenti contenuto** e trascina un componente **Testo** sotto il contenuto corrente della newsletter.

![Journey Optimizer](./images/sbp6.png)

Selezionare l&#39;intero testo predefinito ed eliminarlo. Quindi fare clic sul pulsante **Aggiungi personalizzazione** nella barra degli strumenti.

![Journey Optimizer](./images/sbp7.png)

A questo punto viene visualizzato quanto segue:

![Journey Optimizer](./images/seg1.png)

Nel menu a sinistra, fai clic su **Appartenenze a segmenti**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Se il segmento non è presente in questo elenco, scorri verso il basso per trovare le istruzioni su come recuperare manualmente l’ID segmento.

Seleziona il segmento `Luma - Women's Category Interest` e fai clic sull&#39;icona **+**, che dovrebbe essere simile alla seguente:

![Journey Optimizer](./images/seg3.png)

Lasciare quindi invariata la prima riga e sostituire le righe 2 e 3 con questo codice:

``
    Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
    Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

A questo punto si otterrà:

![Journey Optimizer](./images/seg4.png)

Fai clic su **Convalida** per verificare che il codice sia corretto. Fai clic su **Salva**.

![Journey Optimizer](./images/sbp8.png)

Per salvare il messaggio, fai clic sul pulsante **Salva** nell&#39;angolo in alto a destra. Quindi fare clic su **Simula contenuto**.

![Journey Optimizer](./images/sbp9.png)

Seleziona uno dei profili creati come parte di questa esercitazione e fai clic su **Anteprima**. Viene quindi visualizzato il risultato della configurazione.

![Journey Optimizer](./images/sbp10.png)

Poi vedrai questo. Quindi fare clic su **Chiudi**.

![Journey Optimizer](./images/sbp10fff.png)

Torna alla dashboard dei messaggi facendo clic sulla **freccia** accanto al testo dell&#39;oggetto nell&#39;angolo in alto a sinistra.

![Journey Optimizer](./images/sbp11.png)

Fai clic sulla freccia nell’angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/oc79afff.png)

Fai clic su **Ok** per chiudere l&#39;azione e-mail.

![Journey Optimizer](./images/oc79bfff.png)

Cambia la **pianificazione** in **una volta** e definisci una **data/ora**. Fare clic su **Ok**.

>[!NOTE]
>
>La data e l’ora di invio del messaggio devono essere entro più di un’ora.

![Journey Optimizer](./images/sbp18.png)

Fai clic sul pulsante **Publish** nel percorso.

![Journey Optimizer](./images/sbp19.png)

Nella finestra popup, fare di nuovo clic su **Publish**.

![Journey Optimizer](./images/sbp20.png)

Il percorso di newsletter di base è ora pubblicato. Il messaggio e-mail della newsletter verrà inviato in base alla pianificazione e il percorso verrà interrotto non appena l’ultima e-mail sarà stata inviata.

![Journey Optimizer](./images/sbp20fff.png)

Hai finito questo esercizio.

Passaggio successivo: [3.4.4 Configurare e utilizzare le notifiche push per iOS](./ex4.md)

[Torna al modulo 3.4](./journeyoptimizer.md)

[Torna a tutti i moduli](../../../overview.md)
