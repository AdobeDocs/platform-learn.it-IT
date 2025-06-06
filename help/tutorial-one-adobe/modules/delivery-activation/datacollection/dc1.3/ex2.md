---
title: Raccolta dati - FAC - Creare schemi, modelli dati e collegamenti
description: Foundation - FAC - Creare schemi, modelli dati e collegamenti
kt: 5342
doc-type: tutorial
exl-id: 3b999c1a-cf9e-44a3-8fc1-6a070c3aeb24
source-git-commit: 915054a0342a0e5bb003d2fbc73d1540725aa5f0
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 3%

---

# 1.3.2 Creare schemi, modelli di dati e collegamenti

È ora possibile configurare il database federato in Adobe Experience Platform.

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../dc1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata `--aepSandboxName--`. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../dc1.2/images/sb1.png)

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

**Utente**: il nome utente creato in precedenza, nell&#39;esercizio 1.3.1.1
**Password**: la password creata in precedenza, nell&#39;esercizio 1.3.1.1
**Database**: utilizzare **CITISIGNAL**

Quindi, alla fine, dovresti avere questo. Fare clic su **Verifica connessione**. Se il test ha esito positivo, fare clic su **Distribuisci funzioni**, per creare sul lato Snowflake le funzioni necessarie per il motore del flusso di lavoro.

Una volta verificata la connessione e distribuite le funzioni, la configurazione verrà archiviata.

![FAC](./images/fdb3.png)

Tornando al menu **Database federati**, la connessione verrà visualizzata.

![FAC](./images/fdb4.png)

## 1.3.2.2 Creazione di schemi in AEP

Nel menu a sinistra, fai clic su **Modelli**, quindi vai a **Schemi**. Fare clic su **Crea schema**.

![FAC](./images/fdb5.png)

Seleziona il database federato e fai clic su **Avanti**.

![FAC](./images/fdb6.png)

Poi vedrai questo. Seleziona le 5 tabelle create in Snowflake prima:

- `--aepUserLdap--_HOUSEHOLDS`
- `--aepUserLdap--_MOBILE_DATA_USAGE`
- `--aepUserLdap--_MONTHLY_DATA_USAGE`
- `--aepUserLdap--_PERSONS`
- `--aepUserLdap--_USERS`

Fai clic su **Avanti**.

![FAC](./images/fdb7.png)

AEP carica quindi le informazioni di ciascuna tabella e le mostra nell’interfaccia utente.

Per ogni tabella è possibile:

- modificare l’etichetta dello schema
- aggiungi una descrizione
- rinominare tutti i campi e impostarne la visibilità
- seleziona la chiave primaria per lo schema

Per questo esercizio non sono necessarie modifiche.

Fai clic su **Fine**.

![FAC](./images/fdb8.png)

Poi vedrai questo. Puoi fare clic su qualsiasi schema e rivedere le informazioni. Ad esempio, fare clic su **`--aepUserLdap--_PERSONS`**.

![FAC](./images/fdb9.png)

Vedrai questo, con la possibilità di modificare la configurazione. Fai clic su **Dati** per visualizzare un esempio dei dati presenti nel database di Snowflake.

![FAC](./images/fdb10.png)

Viene quindi visualizzato un esempio dei dati. Questi dati vengono caricati direttamente da Snowflake e non vengono mantenuti in AEP.

![FAC](./images/fdb11.png)

## 1.3.2.3 Crea un modello in AEP

Nel menu a sinistra, vai a **Modelli** e quindi vai a **Modello dati**. Fare clic su **Crea modello dati**.

![FAC](./images/fdb12.png)

Per l&#39;etichetta, utilizzare `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Fai clic su **Crea**.

![FAC](./images/fdb13.png)

Fare clic su **Aggiungi schemi**.

![FAC](./images/fdb14.png)

Seleziona gli schemi e fai clic su **Aggiungi**.

![FAC](./images/fdb15.png)

Poi vedrai questo. Fai clic su **Salva**.

![FAC](./images/fdb16.png)

### PERSONE - UTENTI

Ora puoi iniziare a definire i collegamenti tra schemi. Per iniziare a definire un collegamento, fai clic su **Crea collegamenti**.

![FAC](./images/fdb16a.png)

È innanzitutto necessario definire il collegamento tra la tabella `--aepUserLdap--_USERS` e `--aepUserLdap--_PERSONS`.

Fai clic su **Aggiungi**.

![FAC](./images/fdb18.png)

### FAMIGLIE - PERSONE

Allora tornerai qui. Fai clic su **Crea collegamenti** per creare un altro collegamento.

![FAC](./images/fdb17.png)

Definire quindi il collegamento tra la tabella `--aepUserLdap--_HOUSEHOLDS` e `--aepUserLdap--_PERSONS`.

Fai clic su **Aggiungi**.

![FAC](./images/fdb19.png)

### UTENTI - MONTHLY_DATA_USAGE

Allora tornerai qui. Fai clic su **Crea collegamenti** per creare un altro collegamento.

![FAC](./images/fdb20.png)

Definire quindi il collegamento tra la tabella `--aepUserLdap--_USERS` e `--aepUserLdap--_MONTHLY_DATA_USAGE`.

Fai clic su **Aggiungi**.

![FAC](./images/fdb21.png)

### UTENTI - FAMIGLIE

Allora tornerai qui. Fai clic su **Crea collegamenti** per creare un altro collegamento.

![FAC](./images/fdb22.png)

Definire quindi il collegamento tra la tabella `--aepUserLdap--_USERS` e `--aepUserLdap--_HOUSEHOLDS`.

Fai clic su **Aggiungi**.

![FAC](./images/fdb23.png)

### UTENTI - MOBILE_DATA_USAGE

Allora tornerai qui. Fai clic su **Crea collegamenti** per creare un altro collegamento.

![FAC](./images/fdb24.png)

Definire quindi il collegamento tra la tabella `--aepUserLdap--_USERS` e `--aepUserLdap--_MOBILE_DATA_USAGE`.

Fai clic su **Aggiungi**.

![FAC](./images/fdb25.png)

Dovresti vedere questo. Fai clic su **Salva**.

![FAC](./images/fdb26.png)

L’impostazione del Federated Database in Adobe Experience Platform è ora completata. Ora puoi iniziare a utilizzare i dati federati in una composizione di pubblico federato.

## Passaggi successivi

Vai a [1.3.3 Crea una composizione federata](./ex3.md){target="_blank"}

Torna a [Composizione pubblico federato](./fac.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
