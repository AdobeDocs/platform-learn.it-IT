---
title: Guida introduttiva ai servizi di Firefly
description: Guida introduttiva ai servizi di Firefly
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: 6c344db00b8296c8ea6d31c83cefd8edcddb51b1
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 1%

---

# 1.1.2 Ottimizzare il processo di Firefly utilizzando Microsoft Azure e gli URL prefirmati

## 1.1.2.1 Creare una sottoscrizione Azure

>[!NOTE]
>
>Se disponi già di una sottoscrizione Azure, puoi saltare questo passaggio. Procedere con l&#39;esercizio successivo in questo caso.

Vai a [https://portal.azure.com](https://portal.azure.com) e accedi con il tuo account di Azure. Se non ne hai uno, utilizza il tuo indirizzo e-mail personale per creare il tuo account di Azure.

![Archiviazione Azure](./images/02azureportalemail.png)

Dopo aver effettuato correttamente l’accesso viene visualizzata la seguente schermata:

![Archiviazione Azure](./images/03azureloggedin.png)

Fai clic sul menu a sinistra e seleziona **Tutte le risorse**; se non sei ancora iscritto, verrà visualizzata la schermata della sottoscrizione di Azure. In tal caso, selezionare **Inizia con una versione di valutazione gratuita di Azure**.

![Archiviazione Azure](./images/04azurestartsubscribe.png)

Compila il modulo di abbonamento Azure, fornisci il telefono cellulare e la carta di credito per l’attivazione (avrai un livello gratuito per 30 giorni e non ti verrà addebitato alcun costo, a meno che non esegui l’aggiornamento).

Al termine del processo di abbonamento, sei a posto:

![Archiviazione Azure](./images/06azuresubscriptionok.png)

## 1.1.2.2 Creare un account di archiviazione Azure

Cercare `storage account` e quindi fare clic su **Account di archiviazione**.

![Archiviazione Azure](./images/azs1.png)

Fare clic su **+ Crea**.

![Archiviazione Azure](./images/azs2.png)

Compila i seguenti dettagli:

- Seleziona la **sottoscrizione**
- Seleziona o crea un **gruppo di risorse**
- **Nome account di archiviazione**: utilizzare `--aepUserLdap--`

Fai clic su **Rivedi + crea**.

![Archiviazione Azure](./images/azs3.png)

Fai clic su **Crea**.

![Archiviazione Azure](./images/azs4.png)

Otterrai quindi una conferma simile. Fare clic su **Vai alla risorsa**.

![Archiviazione Azure](./images/azs5.png)

L’account di archiviazione Azure è ora pronto per essere utilizzato.

![Archiviazione Azure](./images/azs6.png)

Fai clic su **Archiviazione dati**, quindi vai a **Contenitori**. Fare clic su **+ Contenitore**.

![Archiviazione Azure](./images/azs7.png)

Per il nome, utilizzare `--aepUserLdap--`. Fai clic su **Crea**.

![Archiviazione Azure](./images/azs8.png)

Il contenitore è ora pronto per essere utilizzato.

![Archiviazione Azure](./images/azs9.png)

## 1.1.2.3 Installare Azure Storage Explorer

Per gestire i file, si utilizzerà Esplora archivi di Microsoft Azure. Puoi scaricarlo tramite [questo collegamento](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4). Selezionare la versione corretta per il sistema operativo specifico, scaricarla e installarla.

![Archiviazione Azure](./images/az10.png)

Una volta installata l’applicazione, aprila. Vedrete qualcosa di simile a questo. Fare clic su **Accedi con Azure**.

![Archiviazione Azure](./images/az11.png)

Fare clic su **Sottoscrizione**.

![Archiviazione Azure](./images/az12.png)

Seleziona **Azure** e fai clic su **Next**.

![Archiviazione Azure](./images/az13.png)

Selezionare l&#39;account di Microsoft Azure e completare il processo di autenticazione.

![Archiviazione Azure](./images/az14.png)

Una volta autenticato, verrà visualizzato un messaggio di questo tipo.

![Archiviazione Azure](./images/az15.png)

Tornare all&#39;app Microsoft Azure Storage Explorer. Selezionare l&#39;abbonamento e fare clic su **Apri Explorer**.

![Archiviazione Azure](./images/az16.png)

Troverai il tuo account di archiviazione in **Account di archiviazione**.

![Archiviazione Azure](./images/az17.png)

Apri **Contenitori BLOB** e fai clic sul contenitore creato nell&#39;esercizio precedente.

![Archiviazione Azure](./images/az18.png)

## 1.1.2.4 Caricamento manuale dei file e utilizzo di un file di immagine come riferimento di stile

Ora devi caricare un file di immagine di tua scelta nel contenitore. Puoi utilizzare qualsiasi file di immagine, oppure puoi utilizzare [questo file](./images/gradient.jpg) scaricandolo dal computer.

![Archiviazione Azure](./images/gradient.jpg)

Rilascia il file di immagine nel contenitore in Azure Storage Explorer.

Una volta caricato, lo visualizzerai nel tuo contenitore:

![Archiviazione Azure](./images/az19.png)

Fare clic con il pulsante destro del mouse sul file `gradient.jpg` e quindi scegliere **Ottieni firma di accesso condiviso**.

![Archiviazione Azure](./images/az20.png)

In **Autorizzazioni**, è richiesto solo **Lettura**. Fai clic su **Crea**.

![Archiviazione Azure](./images/az21.png)

Visualizzerai quindi l’URL preceduto per questo file di immagine. Copiala come ti servirà per la prossima richiesta API al Firefly.

![Archiviazione Azure](./images/az22.png)

Torna a Postman. Apri la richiesta **POST - Firefly - T2I (styleref) V3**. Visualizzerai quindi questo elemento in **Corpo**.

![Archiviazione Azure](./images/az23.png)

Sostituire l&#39;URL segnaposto con l&#39;URL preceduto del file immagine copiato da Azure Storage Explorer. Allora avrai questo. Fai clic su **Invia**.

![Archiviazione Azure](./images/az24.png)

Riceverai quindi di nuovo una risposta da Servizi di Firefly, con una nuova immagine. Apri il file di immagine nel browser.

![Archiviazione Azure](./images/az25.png)

Verrà quindi visualizzata un&#39;altra immagine con `horses in a field`, ma questa volta lo stile sarà simile al file di immagine fornito come riferimento di stile.

![Archiviazione Azure](./images/az26.png)

## 1.1.2.5 Caricamento di file programmatici

Per utilizzare il caricamento di file a livello di programmazione con gli account di archiviazione di Azure, è necessario creare un nuovo token **firma di accesso condiviso (SAS)**, con autorizzazioni che consentono di scrivere un file.

Per farlo, torna ad Azure Storage Explorer. Fare clic con il pulsante destro del mouse sul contenitore e quindi scegliere **Ottieni firma di accesso condiviso**.

![Archiviazione Azure](./images/az27.png)

In **Autorizzazioni** sono necessarie le seguenti autorizzazioni:

- **Letto**
- **Aggiungi**
- **Crea**
- **Scrittura**
- **Elenco**

Fai clic su **Crea**.

![Archiviazione Azure](./images/az28.png)

Otterrai quindi il **token SAS**. Fai clic su **Copia**.

![Archiviazione Azure](./images/az29.png)

Ora puoi utilizzare questo **token SAS** per caricare un file nell&#39;account di archiviazione Azure. Torna a Postman per farlo.

Fai clic per selezionare la cartella **FF - Firefly Services Tech Insiders**, quindi fai clic sui tre punti **...** nella cartella **Firefly** e quindi su **Aggiungi richiesta**.

![Archiviazione Azure](./images/az30.png)

Avrai quindi una richiesta vuota. Modifica il nome della richiesta in **Carica file nell&#39;account di archiviazione Azure**, modifica **Tipo di richiesta** in **PUT** e incolla l&#39;URL del token SAS nella sezione URL.

Quindi, fai clic su **Corpo**.

![Archiviazione Azure](./images/az31.png)

Ora dovrai selezionare un file dal computer locale. Puoi utilizzare un nuovo file di immagine oppure un altro file di immagine che puoi trovare [qui](./images/gradient2-p.jpg).

![File sfumatura](./images/gradient2-p.jpg)

In **Corpo**, selezionare **binario**, quindi fare clic su **Seleziona file**, quindi fare clic su **+ Nuovo file dal computer locale**.

![Archiviazione Azure](./images/az32.png)

Seleziona il file desiderato e fai clic su **Apri**.

![Archiviazione Azure](./images/az33.png)

Poi vedrai questo. Successivamente, specificare il nome del file che verrà utilizzato nell&#39;account di archiviazione Azure. Per eseguire questa operazione, è necessario posizionare il cursore davanti al punto interrogativo **?** nell&#39;URL. Attualmente è visibile qui:

![Archiviazione Azure](./images/az34.png)

L’URL ha attualmente questo aspetto, ma dovrà essere modificato.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

Il nome di file da utilizzare è `gradient2-p.jpg`, il che significa che l&#39;URL deve essere modificato per includere il nome del file, come segue:

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Archiviazione Azure](./images/az34a.png)

Quindi, vai a **Intestazioni** dove devi aggiungere manualmente una nuova intestazione. Utilizza questo:

| Chiave | Valore |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Archiviazione Azure](./images/az35.png)

Vai a **Autorizzazione** e imposta **Tipo di autenticazione** su **Nessuna autenticazione**. Fai clic su **Invia**.

![Archiviazione Azure](./images/az36.png)

Vedrai quindi questa risposta vuota in Postman, il che significa che il caricamento del file è andato bene.

![Archiviazione Azure](./images/az37.png)

Se poi torni ad Azure Storage Explorer e aggiorni il contenuto della cartella, ora troverai il file appena caricato lì.

![Archiviazione Azure](./images/az38.png)

## 1.1.2.5 Utilizzo di file programmatici

Per utilizzare i file letti a livello di programmazione dagli account di archiviazione di Azure, è necessario creare un nuovo token di **firma di accesso condiviso (SAS)**, con autorizzazioni che consentono di leggere un file. Tecnicamente puoi utilizzare il token SAS creato nell&#39;esercizio precedente, ma è consigliabile disporre di un token separato con sole autorizzazioni **Lettura**.

Per farlo, torna ad Azure Storage Explorer. Fare clic con il pulsante destro del mouse sul contenitore e quindi scegliere **Ottieni firma di accesso condiviso**.

![Archiviazione Azure](./images/az27.png)

In **Autorizzazioni** sono necessarie le seguenti autorizzazioni:

- **Letto**
- **Aggiungi**
- **Crea**
- **Scrittura**
- **Elenco**

Fai clic su **Crea**.

![Archiviazione Azure](./images/az28.png)


Passaggio successivo: [1.1.3 ...](./ex3.md)

[Torna al modulo 1.1](./firefly-services.md)

[Torna a tutti i moduli](./../../../overview.md)
