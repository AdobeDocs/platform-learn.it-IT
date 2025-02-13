---
title: Raccolta dati - FAC - Creare una composizione federata
description: Foundation - FAC - Creare una composizione federata
kt: 5342
doc-type: tutorial
exl-id: 293bf825-d0d6-48cf-9cbf-69f622597678
source-git-commit: e32d415d2997b43834e9fc2495c4394b13f4d49f
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 3%

---

# 1.3.3 Creare una composizione federata

Ora puoi configurare la composizione del pubblico federato in AEP.

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../module1.2/images/sb1.png)

## 1.3.3.1 Creare il pubblico

Nel menu a sinistra, vai a **Tipi di pubblico** e quindi vai a **Composizioni federate**. Fare clic su **Crea composizione**.

![FAC](./images/fedcomp1.png)

Per l&#39;etichetta, utilizzare: `--aepUserLdap-- - CitiSignal Fiber`. Selezionare il modello dati creato nell&#39;esercizio precedente, denominato `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Fai clic su **Crea**.

![FAC](./images/fedcomp2.png)

Poi vedrai questo.

![FAC](./images/fedcomp3.png)

Fai clic sull&#39;icona **+** e fai clic su **Genera pubblico**.

![FAC](./images/fedcomp4.png)

Poi vedrai questo. Seleziona **Crea pubblico**. Fai clic sull&#39;icona **cerca** per selezionare uno schema.

![FAC](./images/fedcomp5.png)

Selezionare lo schema **—aepUserLdap—_HOUSEHOLDS**. Fai clic su **Conferma**.

![FAC](./images/fedcomp6.png)

Fare clic su **Continua**.

![FAC](./images/fedcomp7.png)

Ora puoi iniziare a creare la query che verrà inviata a Snowflake. Fare clic sull&#39;icona **+** e quindi su **Condizione personalizzata**.

![FAC](./images/fedcomp8.png)

Selezionare l&#39;attributo **ISELIGIBLEFORFIBER** Fare clic su **Confirm**.

![FAC](./images/fedcomp9.png)

Poi vedrai questo. Imposta il campo **Value** su **True**. Fai clic su **Calcola** per inviare la query a Snowflake e ottenere una stima dei profili idonei.

![FAC](./images/fedcomp10.png)

Quindi fare di nuovo clic sull&#39;icona **+** e fare di nuovo clic su **Condizione personalizzata** per aggiungere un&#39;altra condizione.

![FAC](./images/fedcomp11.png)

La seconda condizione da aggiungere è: `Is the user an existing CitiSignal Mobile subscriber?`. Per rispondere a questa domanda, utilizzare la relazione tra la famiglia e il cliente principale della famiglia, definita in un&#39;altra tabella, **—aepUserLdap—_PERSONS**. Puoi eseguire il drill-down nel menu degli attributi utilizzando il collegamento **family2person**.

![FAC](./images/fedcomp12.png)

Selezionare l&#39;attributo **ISMOBILESUB** e fare clic su **Conferma**.

![FAC](./images/fedcomp13.png)

Imposta il campo **Valore** su **Vero** Fai clic di nuovo su **Calcola** per aggiornare il numero di profili di destinazione. Fai clic su **Conferma**.

![FAC](./images/fedcomp14.png)

Fai clic sull&#39;icona **+** e quindi su **Salva pubblico**.

![FAC](./images/fedcomp15.png)

Imposta **etichetta pubblico** su `--aepUserLdap-- - CitiSignal Eligible for Fiber`.

Fare clic su **+ Aggiungi mapping pubblico**.

![FAC](./images/fedcomp16.png)

Seleziona **HOUSEHOLD_ID** e fai clic su **Conferma**.

![FAC](./images/fedcomp17.png)

Fare clic su **+ Aggiungi mapping pubblico**.

![FAC](./images/fedcomp18.png)

Espandere facendo clic su **Dimensione targeting**.

![FAC](./images/fedcomp18a.png)

Espandere facendo clic sul collegamento **family2person**.

![FAC](./images/fedcomp18b.png)

Selezionare il campo **NAME**. Fai clic su **Conferma**.

![FAC](./images/fedcomp18c.png)

Fare clic su **+ Aggiungi mapping pubblico**.

![FAC](./images/fedcomp20.png)

Espandere facendo clic su **Dimensione targeting**.

![FAC](./images/fedcomp20a.png)

Espandere facendo clic sul collegamento **family2person**.

![FAC](./images/fedcomp20b.png)

Seleziona il campo **EMAIL**. Fai clic su **Conferma**.

![FAC](./images/fedcomp20c.png)

Poi vedrai questo. È ora necessario impostare il campo **Identità primaria** su **Household2person_EMAIL**. Imposta **Spazio dei nomi identità** su **E-mail**.

Fai clic su **Salva**.

![FAC](./images/fedcomp21.png)

La tua composizione ora è finita. Fare clic su **Inizio** per eseguirlo.

![FAC](./images/fedcomp21a.png)

La query verrà ora inviata a Snowflake, che eseguirà la query sui dati di origine. I risultati verranno inviati nuovamente ad AEP, ma i dati di origine rimangono in Snowflake.

Il pubblico ora è popolato e può essere indirizzato dall’interno dell’ecosistema AEP.

![FAC](./images/fedcomp22.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 1.3](./fac.md)

[Torna a tutti i moduli](../../../overview.md)
