---
title: Ottimizzare il processo di Firefly utilizzando Microsoft Azure e gli URL predefiniti
description: Scopri come ottimizzare il processo di Firefly utilizzando Microsoft Azure e gli URL prefirmati
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: e7f83f362e5c9b2dff93d43a7819f6c23186b456
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 0%

---

# 1.1.2 Ottimizzare il processo Firefly utilizzando Microsoft Azure e gli URL prefirmati

Scopri come ottimizzare il processo di Firefly utilizzando Microsoft Azure e gli URL prefirmati.

## 1.1.2.1 Cosa sono gli URL prefirmati?

Un URL preceduto è un URL che consente l&#39;accesso temporaneo a un oggetto specifico in un percorso di archiviazione. Utilizzando l’URL, un utente può ad esempio LEGGERE l’oggetto o SCRIVERE un oggetto (o aggiornare un oggetto esistente). L’URL contiene parametri specifici impostati dall’applicazione.

Nel contesto della creazione dell&#39;automazione della supply chain dei contenuti, spesso è necessario eseguire più operazioni sui file per un caso d&#39;uso specifico. Ad esempio, potrebbe essere necessario modificare lo sfondo di un file, il testo di vari livelli, ecc. Non è sempre possibile eseguire tutte le operazioni sui file contemporaneamente, il che rende necessario un approccio in più passaggi. Dopo ogni passaggio intermedio, l’output è quindi un file temporaneo necessario per l’esecuzione del passaggio successivo. Una volta eseguito il passaggio successivo, il file temporaneo perde rapidamente valore e spesso non è più necessario, pertanto deve essere eliminato.

Adobe Firefly Services attualmente supporta i seguenti domini:

- Amazon AWS: *.amazonaws.com
- Microsoft Azure: *.windows.net
- Dropbox: *.dropboxusercontent.com

Il motivo per cui spesso vengono utilizzate soluzioni di archiviazione cloud è che le risorse intermedie che vengono create perdono valore rapidamente. Il problema che viene risolto tramite URL prefirmati è spesso risolto al meglio con una soluzione di storage di base, che in genere è uno dei servizi cloud sopra indicati.

All’interno dell’ecosistema Adobe sono inoltre disponibili soluzioni di storage come Frame.io, Workfront Fusion e Adobe Experience Manager assets. Queste soluzioni supportano anche URL prefirmati, che spesso diventano una scelta da effettuare durante l’implementazione. La scelta è spesso basata su una combinazione di applicazioni già disponibili e costi di storage.

Di conseguenza, gli URL prefirmati vengono utilizzati in combinazione con le operazioni di Adobe Firefly Services per i seguenti motivi:

- le organizzazioni spesso devono elaborare più modifiche alla stessa immagine in fasi intermedie, e lo storage intermedio è necessario per rendere possibile tale operazione.
- l’accesso in lettura e scrittura da posizioni di archiviazione cloud deve essere sicuro e in un ambiente lato server non è possibile effettuare l’accesso manualmente, pertanto la sicurezza deve essere salvata direttamente nell’URL.

Un URL prefirmato utilizza tre parametri per limitare l’accesso all’utente:

- Percorso di archiviazione: potrebbe trattarsi di un percorso bucket AWS S3, un percorso account di archiviazione Microsoft Azure con contenitore
- Nome file: il file specifico che deve essere letto, aggiornato ed eliminato.
- Parametro stringa query: un parametro stringa query inizia sempre con un punto interrogativo ed è seguito da una serie complessa di parametri

Esempio:

- **Amazon AWS**: `https://bucket.s3.eu-west-2.amazonaws.com/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AXXXXXXXXXX%2Feu-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250510T171315Z&X-Amz-Expires=1800&X-Amz-Signature=XXXXXXXXX&X-Amz-SignedHeaders=host`
- **Microsoft Azure**: `https://storageaccount.blob.core.windows.net/container/image.png?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=XXXXXX%3D`

## 1.1.2.2 Crea una sottoscrizione Azure

>[!NOTE]
>
>Se disponi già di una sottoscrizione Azure, puoi saltare questo passaggio. Procedere con l&#39;esercizio successivo in questo caso.

>[!NOTE]
>
>Se segui questa esercitazione come parte di un workshop guidato di persona o di un corso di formazione guidato su richiesta, probabilmente hai già accesso a un account di archiviazione di Microsoft Azure. In tal caso, non è necessario creare un account personale: utilizza l’account fornito come parte del corso di formazione.

Vai a [https://portal.azure.com](https://portal.azure.com){target="_blank"} e accedi con il tuo account di Azure. Se non ne hai uno, utilizza il tuo indirizzo e-mail personale per creare il tuo account di Azure.

![Archiviazione Azure](./images/02azureportalemail.png){zoomable="yes"}

Dopo aver effettuato l’accesso, viene visualizzata la seguente schermata:

![Archiviazione Azure](./images/03azureloggedin.png){zoomable="yes"}

Nel menu a sinistra, seleziona **Tutte le risorse**. Se non hai ancora effettuato l&#39;abbonamento, viene visualizzata la schermata dell&#39;abbonamento di Azure.

Se non sei abbonato, seleziona **Inizia con una versione di valutazione gratuita di Azure**.

![Archiviazione Azure](./images/04azurestartsubscribe.png){zoomable="yes"}

Compila il modulo di abbonamento Azure e fornisci il telefono cellulare e la carta di credito per l’attivazione (avrai un livello gratuito per 30 giorni e non ti verrà addebitato alcun importo, a meno che non esegui l’aggiornamento).

Al termine del processo di abbonamento, sei a posto.

![Archiviazione Azure](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.3 Crea account di archiviazione Azure

Cercare `storage account` e selezionare **Account di archiviazione**.

![Archiviazione Azure](./images/azs1.png){zoomable="yes"}

Selezionare **+ Crea**.

![Archiviazione Azure](./images/azs2.png){zoomable="yes"}

Seleziona la **sottoscrizione** e seleziona (o crea) un **gruppo di risorse**.

In **Nome account di archiviazione** utilizzare `--aepUserLdap--`.

Seleziona **Rivedi + crea**.

![Archiviazione Azure](./images/azs3.png){zoomable="yes"}

Seleziona **Crea**.

![Archiviazione Azure](./images/azs4.png){zoomable="yes"}

Dopo la conferma, seleziona **Vai alla risorsa**.

![Archiviazione Azure](./images/azs5.png){zoomable="yes"}

L’account di archiviazione Azure è ora pronto per essere utilizzato.

![Archiviazione Azure](./images/azs6.png){zoomable="yes"}

Selezionare **Archiviazione dati**, quindi passare a **Contenitori**. Selezionare **+ Contenitore**.

![Archiviazione Azure](./images/azs7.png){zoomable="yes"}

Utilizza `--aepUserLdap--` per il nome e seleziona **Crea**.

![Archiviazione Azure](./images/azs8.png){zoomable="yes"}

Il contenitore è ora pronto per essere utilizzato.

![Archiviazione Azure](./images/azs9.png){zoomable="yes"}

## 1.1.2.4 Installare Azure Storage Explorer

[Scarica Microsoft Azure Storage Explorer per gestire i file](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. Selezionare la versione corretta per il sistema operativo specifico, scaricarla e installarla.

![Archiviazione Azure](./images/az10.png){zoomable="yes"}

Apri l&#39;applicazione e seleziona **Accedi con Azure**.

![Archiviazione Azure](./images/az11.png){zoomable="yes"}

Selezionare **Sottoscrizione**.

![Archiviazione Azure](./images/az12.png){zoomable="yes"}

Selezionare **Azure** e quindi **Next**.

![Archiviazione Azure](./images/az13.png){zoomable="yes"}

Selezionare l&#39;account di Microsoft Azure e completare il processo di autenticazione.

![Archiviazione Azure](./images/az14.png){zoomable="yes"}

Dopo l’autenticazione, viene visualizzato questo messaggio.

![Archiviazione Azure](./images/az15.png){zoomable="yes"}

Nell&#39;app Microsoft Azure Storage Explorer, selezionare la sottoscrizione e scegliere **Apri Explorer**.

>[!NOTE]
>
>Se il tuo account non viene visualizzato, fai clic sull&#39;icona **ingranaggio** accanto al tuo indirizzo e-mail e seleziona **Rimuovi filtro**.

![Archiviazione Azure](./images/az16.png){zoomable="yes"}

L&#39;account di archiviazione viene visualizzato in **Account di archiviazione**.

![Archiviazione Azure](./images/az17.png){zoomable="yes"}

Apri **Contenitori BLOB** e seleziona il contenitore creato nell&#39;esercizio precedente.

![Archiviazione Azure](./images/az18.png){zoomable="yes"}

## 1.1.2.5 Caricamento manuale del file e utilizzo di un file immagine come riferimento di stile

Carica un file di immagine di tua scelta o [questo file](./images/gradient.jpg){target="_blank"} nel contenitore.

![Archiviazione Azure](./images/gradient.jpg)

Una volta caricato, puoi visualizzarlo nel contenitore:

![Archiviazione Azure](./images/az19.png){zoomable="yes"}

Fare clic con il pulsante destro del mouse su `gradient.jpg`, quindi selezionare **Ottieni firma di accesso condiviso**.

![Archiviazione Azure](./images/az20.png){zoomable="yes"}

In **Autorizzazioni**, è richiesto solo **Lettura**. Seleziona **Crea**.

![Archiviazione Azure](./images/az21.png){zoomable="yes"}

Copia l’URL prefirmato del file di immagine per la successiva richiesta API in Firefly.

![Archiviazione Azure](./images/az22.png){zoomable="yes"}

In Postman apri la richiesta **POST - Firefly - T2I (styleref) V3**.
Viene visualizzato in **Corpo**.

![Archiviazione Azure](./images/az23.png){zoomable="yes"}

Sostituisci l&#39;URL segnaposto con l&#39;URL preceduto per il file di immagine e seleziona **Invia**.

![Archiviazione Azure](./images/az24.png){zoomable="yes"}

Apri la nuova immagine del Firefly Services di risposta nel browser.

![Archiviazione Azure](./images/az25.png){zoomable="yes"}

Un&#39;altra immagine viene visualizzata con `horses in a field`, ma questa volta lo stile è simile al file di immagine fornito come riferimento di stile.

![Archiviazione Azure](./images/az26.png){zoomable="yes"}

## Caricamento file programmatico 1.1.2.6

Per utilizzare il caricamento di file a livello di programmazione con gli account di archiviazione di Azure, è necessario creare un nuovo token **firma di accesso condiviso (SAS)** con autorizzazioni che consentono di scrivere un file.

In Azure Storage Explorer, fare clic con il pulsante destro del mouse sul contenitore e selezionare **Ottieni firma di accesso condiviso**.

![Archiviazione Azure](./images/az27.png){zoomable="yes"}

In **Autorizzazioni**, seleziona le seguenti autorizzazioni richieste:

- **Letto**
- **Aggiungi**
- **Crea**
- **Scrittura**
- **Elenco**

Seleziona **Crea**.

![Archiviazione Azure](./images/az28.png){zoomable="yes"}

Dopo aver ricevuto la **firma di accesso condiviso**, seleziona **Copia** per copiare l&#39;URL.

![Archiviazione Azure](./images/az29.png){zoomable="yes"}

Utilizza il **token SAS** per caricare un file nell&#39;account di archiviazione Azure.

In Postman, seleziona la cartella **FF - Firefly Services Tech Insiders**, quindi **...** nella cartella **Firefly**, quindi seleziona **Aggiungi richiesta**.

![Archiviazione Azure](./images/az30.png){zoomable="yes"}

Modifica il nome della richiesta vuota in **Carica file nell&#39;account di archiviazione Azure**, cambia il **Tipo di richiesta** in **PUT** e incolla l&#39;URL del token SAS nella sezione URL, quindi seleziona **Corpo**.

![Archiviazione Azure](./images/az31.png){zoomable="yes"}

Quindi, seleziona un file dal computer locale o usa un altro file di immagine che si trova [qui](./images/gradient2-p.jpg){target="_blank"}.

![File sfumatura](./images/gradient2-p.jpg)

In **Body**, selezionare **binary**, **Seleziona file**, quindi selezionare **+ Nuovo file dal computer locale**.

![Archiviazione Azure](./images/az32.png){zoomable="yes"}

Selezionare il file desiderato e selezionare **Apri**.

![Archiviazione Azure](./images/az33.png){zoomable="yes"}

Specificare quindi il nome del file da utilizzare nell&#39;account di archiviazione Azure posizionando il cursore davanti al punto interrogativo **?** nell&#39;URL come segue:

![Archiviazione Azure](./images/az34.png){zoomable="yes"}

L’URL ha attualmente questo aspetto, ma deve essere modificato.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

Cambia il nome del file in `gradient2-p.jpg` e cambia l&#39;URL in modo da includere il nome del file come segue:

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![Archiviazione Azure](./images/az34a.png){zoomable="yes"}

Quindi, vai a **Intestazioni** per aggiungere manualmente una nuova intestazione come questa:

| Chiave | Valore |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![Archiviazione Azure](./images/az35.png){zoomable="yes"}

Vai a **Autorizzazione** e imposta il **Tipo di autenticazione** su **Nessuna autenticazione**, quindi seleziona **Invia**.

![Archiviazione Azure](./images/az36.png){zoomable="yes"}

Successivamente, questa risposta vuota viene visualizzata in Postman, il che significa che il caricamento del file è corretto.

![Archiviazione Azure](./images/az37.png){zoomable="yes"}

In Azure Storage Explorer aggiorna il contenuto della cartella e viene visualizzato il file appena caricato.

![Archiviazione Azure](./images/az38.png){zoomable="yes"}

## 1.1.2.7 utilizzo file programmatico

Per leggere a livello di programmazione i file dagli account di archiviazione di Azure nel lungo termine, è necessario creare un nuovo token **firma di accesso condiviso (SAS)**, con autorizzazioni che consentono di leggere un file. Tecnicamente puoi utilizzare il token SAS creato nell&#39;esercizio precedente, ma è consigliabile disporre di un token separato con solo autorizzazioni **Lettura** e un token separato con solo autorizzazioni **Scrittura**.

### Token SAS lettura a lungo termine

Torna ad Azure Storage Explorer, fai clic con il pulsante destro del mouse sul contenitore, quindi seleziona **Ottieni firma di accesso condiviso**.

![Archiviazione Azure](./images/az27.png){zoomable="yes"}

In **Autorizzazioni**, seleziona le seguenti autorizzazioni richieste:

- **Letto**
- **Elenco**

Imposta **Scadenza** su 1 anno a partire da ora.

Seleziona **Crea**.

![Archiviazione Azure](./images/az100.png){zoomable="yes"}

Copiare l&#39;URL e scriverlo in un file sul computer per ottenere il token SAS a lungo termine con autorizzazioni di lettura.

![Archiviazione Azure](./images/az101.png){zoomable="yes"}

L’URL deve essere simile al seguente:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

Puoi derivare un paio di valori dall’URL precedente:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Token SAS scrittura a lungo termine

Torna ad Azure Storage Explorer, fai clic con il pulsante destro del mouse sul contenitore e seleziona **Ottieni firma di accesso condiviso**.

![Archiviazione Azure](./images/az27.png){zoomable="yes"}

In **Autorizzazioni**, seleziona le seguenti autorizzazioni richieste:

- **Letto**
- **Elenco**
- **Aggiungi**
- **Crea**
- **Scrittura**

Imposta **Scadenza** su 1 anno a partire da ora.

Seleziona **Crea**.

![Archiviazione Azure](./images/az102.png){zoomable="yes"}

Copiare l&#39;URL e scriverlo in un file sul computer per ottenere il token SAS a lungo termine con autorizzazioni di lettura.

![Archiviazione Azure](./images/az103.png){zoomable="yes"}

L’URL deve essere simile al seguente:

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Puoi derivare un paio di valori dall’URL precedente:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variabili in Postman

Come puoi vedere nella sezione precedente, esistono alcune variabili comuni sia nel token di lettura che in quello di scrittura.

Successivamente, devi creare in Postman le variabili che memorizzano i vari elementi dei token SAS di cui sopra. Alcuni valori sono identici in entrambi gli URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Per le interazioni API future, la cosa principale che cambia è il nome della risorsa, mentre le variabili di cui sopra rimangono le stesse. In tal caso, ha senso creare variabili in Postman in modo da non doverle specificare manualmente ogni volta.

In Postman, seleziona **Ambienti**, apri **Tutte le variabili** e seleziona **Ambiente**.

![Archiviazione Azure](./images/az104.png){zoomable="yes"}

Crea queste 4 variabili nella tabella visualizzata e per le colonne **Valore iniziale** e **Valore corrente**, immetti i tuoi valori personali specifici.

- `AZURE_STORAGE_URL`: l&#39;URL
- `AZURE_STORAGE_CONTAINER`: nome contenitore
- `AZURE_STORAGE_SAS_READ`: token di lettura SAS
- `AZURE_STORAGE_SAS_WRITE`: token di scrittura SAS

Seleziona **Salva**.

![Archiviazione Azure](./images/az105.png){zoomable="yes"}

### Variabili in PostBuster

Come puoi vedere nella sezione precedente, esistono alcune variabili comuni sia nel token di lettura che in quello di scrittura.

Successivamente è necessario creare variabili in PostBuster che memorizzino i vari elementi dei token SAS di cui sopra. Alcuni valori sono identici in entrambi gli URL:

- `AZURE_STORAGE_URL`: `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER`: `vangeluw`
- `AZURE_STORAGE_SAS_READ`: `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE`: `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Aprire PostBuster. Seleziona **Ambiente base**, quindi fai clic sull&#39;icona **modifica** per aprire l&#39;Ambiente base.

![Archiviazione Azure](./images/pbbe1.png)

Vedrai quindi 4 variabili vuote. Immetti qui i dettagli dell’account di archiviazione Azure.

![Archiviazione Azure](./images/pbbe2.png)

Il file dell’ambiente di base dovrebbe ora avere questo aspetto. Fai clic su **Chiudi**.

![Archiviazione Azure](./images/pbbe3.png)

### Verifica la configurazione

In uno degli esercizi precedenti, il **Corpo** della richiesta **Firefly - T2I (styleref) V3** era simile al seguente:

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![Archiviazione Azure](./images/az24.png){zoomable="yes"}

Modifica l’URL in:

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

Seleziona **Invia** per verificare le modifiche apportate.

![Archiviazione Azure](./images/az106.png){zoomable="yes"}

Se le variabili sono state configurate correttamente, viene restituito un URL immagine.

![Archiviazione Azure](./images/az107.png){zoomable="yes"}

Apri l’URL dell’immagine per verificarla.

![Archiviazione Azure](./images/az108.jpg)

## Passaggi successivi

Vai a [Utilizzo delle API di Photoshop](./ex3.md){target="_blank"}

Torna a [Panoramica di Adobe Firefly Services](./firefly-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}