---
title: Raccolta dati - FAC - Creare schemi, modelli dati e collegamenti
description: Foundation - FAC - Creare schemi, modelli dati e collegamenti
kt: 5342
doc-type: tutorial
exl-id: e863ab3a-44df-4bb4-b081-a62616aaa1f1
source-git-commit: 1c91cb2129f827fd39dc065baf5d8ea067a5731a
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---

# 1.3.2 Creare schemi, modelli di dati e collegamenti

È ora possibile configurare il database federato in AEP.

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../module1.2/images/sb1.png)

## 1.3.2.1 Configurare un database federato in AEP

Fai clic su **Federated databases** nel menu a sinistra. Quindi fare clic su **Aggiungi database federato**.

![FAC](./images/fdb1.png)

Come **Etichetta**, usa `--aepUserLdap-- - CitiSignal Snowflake` e per il tipo scegli **Snowflake**.

Nella sezione dei dettagli, devi compilare le credenziali, che avranno un aspetto simile a questo:

![FAC](./images/fdb2.png)

**Server**:

In Snowflake, vai a **Amministratore > Account**. Fai clic sul 3 **...** accanto al tuo account e fai clic su **Gestisci URL**.

![FAC](./images/fdburl1.png)

Poi vedrai questo. Copia l&#39;**URL corrente** e incollalo nel campo **Server** in AEP.

![FAC](./images/fdburl2.png)

**Utente**: il nome utente creato in precedenza nell&#39;esercizio 1.3.1.1
**Password**: password creata in precedenza nell&#39;esercizio 1.3.1.1
**Database**: utilizzare **CITISIGNAL**

Quindi, alla fine, dovresti avere questo. Fare clic su **Verifica connessione**. Se il test ha esito positivo, fare clic su **Distribuisci funzioni**, per creare sul lato Snowflake le funzioni necessarie per il motore del flusso di lavoro.

Una volta verificata la connessione e distribuite le funzioni, la configurazione verrà archiviata.

![FAC](./images/fdb3.png)

Tornando al menu **Database federati**, la connessione verrà visualizzata.

![FAC](./images/fdb4.png)

## 1.3.2.2 Creare schemi in AEP

Nel menu a sinistra, fai clic su **Modelli**, quindi vai a **Schemi**. Fare clic su **Crea schema**.

![FAC](./images/fdb5.png)

Selezionare il database federato e fare clic su **+ Aggiungi tabelle**.

![FAC](./images/fdb6.png)

Poi vedrai questo. Selezionare le 5 tabelle create nel Snowflake prima:

- `CK_HOUSEHOLDS`
- `CK_MOBILE_DATA_USAGE`
- `CK_MONTHLY_DATA_USAGE`
- `CK_PERSONS`
- `CK_USERS`

Fai clic su **Aggiungi**.

![FAC](./images/fdb7.png)

AEP carica quindi le informazioni di ciascuna tabella e le mostra nell’interfaccia utente.

Per ogni tabella è possibile:

- modificare l’etichetta dello schema
- aggiungi una descrizione
- rinominare tutti i campi e impostarne la visibilità
- seleziona la chiave primaria per lo schema

Per questo esercizio non sono necessarie modifiche.

Fai clic su **Crea**.

![FAC](./images/fdb8.png)

Poi vedrai questo. Puoi fare clic su qualsiasi schema e rivedere le informazioni. Ad esempio, fai clic su **CK_PERSONS**.

![FAC](./images/fdb9.png)

Vedrai questo, con la possibilità di modificare la configurazione. Fai clic su **Dati** per visualizzare un esempio dei dati presenti nel database di Snowflake.

![FAC](./images/fdb10.png)

Viene quindi visualizzato un esempio dei dati.

![FAC](./images/fdb11.png)

## 1.3.2.3 Creare un modello in AEP

Nel menu a sinistra, vai a **Modelli** e quindi vai a **Modello dati**. Fare clic su **Crea modello dati**.

![FAC](./images/fdb12.png)

Per l&#39;etichetta, utilizzare `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Fai clic su **Crea**.

![FAC](./images/fdb13.png)

Fare clic su **Aggiungi schemi**.

![FAC](./images/fdb14.png)

Seleziona gli schemi e fai clic su **Aggiungi**.

![FAC](./images/fdb15.png)

Poi vedrai questo. Fai clic su **Salva**.

Ora puoi iniziare a definire i collegamenti tra schemi. Per iniziare a definire un collegamento, fai clic su **Crea collegamenti**.

![FAC](./images/fdb16.png)

Definiamo innanzitutto il collegamento tra la tabella `CK_USERS` e `CK_PERSONS`.

Fai clic su **Aggiungi**.

![FAC](./images/fdb18.png)

Allora tornerai qui. Fai clic su **Crea collegamenti** per creare un altro collegamento.

![FAC](./images/fdb17.png)

Definiamo quindi il collegamento tra la tabella `CK_HOUSEHOLDS` e `CK_PERSONS`.

![FAC](./images/fdb19.png)

Allora tornerai qui. Fai clic su **Crea collegamenti** per creare un altro collegamento.

![FAC](./images/fdb20.png)

Definiamo quindi il collegamento tra la tabella `CK_MONTHLY_DATA_USAGE` e `CK_USERS`.

![FAC](./images/fdb21.png)

Allora tornerai qui. Fai clic su **Crea collegamenti** per creare un altro collegamento.

![FAC](./images/fdb22.png)

Definiamo quindi il collegamento tra la tabella `CK_USERS` e `CK_HOUSEHOLDS`.

![FAC](./images/fdb23.png)

Allora tornerai qui. Fai clic su **Salva**.
![FAC](./images/fdb24.png)

La configurazione in AEP è terminata. Ora puoi iniziare a utilizzare i dati federati in una composizione di pubblico federato.

Passaggio successivo: [1.3.3 Creare una composizione federata](./ex3.md)

[Torna al modulo 1.3](./fac.md)

[Torna a tutti i moduli](../../../overview.md)
