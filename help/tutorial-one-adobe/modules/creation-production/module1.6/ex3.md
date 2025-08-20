---
title: Creare l’app DAM esterna
description: Creare l’app DAM esterna
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 6823e8a0-dde7-460a-a48a-6787e65e4104
source-git-commit: fe162f285d67cc2a37736f80715a5c5717835e95
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 1.6.3 Creare e distribuire l’app DAM esterna

## 1.6.3.1 Scarica i file di app di esempio

Vai a [https://github.com/adobe/genstudio-extensibility-examples](https://github.com/adobe/genstudio-extensibility-examples). Fai clic su **Codice**, quindi seleziona **Scarica ZIP**.

![Est DAM](./images/extdam1.png)

Decomprimi il file zip sul desktop.

![Est DAM](./images/extdam2.png)

Apri la cartella **genstudio-extensibility-examples-main**. Vedrai più app di esempio. Quello di interesse per questo esercizio è **genstudio-external-dam-app**.

Copia la directory e incollala sul desktop.

![Est DAM](./images/extdam4.png)

Ora dovresti avere questo sul desktop:

![Est DAM](./images/extdam3.png)

Per gli esercizi successivi, utilizzerai solo la cartella **genstudio-external-dam-app**.

## 1.6.3.2 Configurare l&#39;interfaccia della riga di comando di Adobe Developer

Fare clic con il pulsante destro del mouse sulla cartella **genstudio-external-dam-app** e selezionare **New Terminal at Folder**.

![Est DAM](./images/extdam5.png)

Dovresti vedere questo. Immettere il comando `aio login`. Questo comando reindirizzerà al browser e prevede l’accesso.

![Est DAM](./images/extdam6.png)

Dopo aver effettuato correttamente l’accesso, dovresti visualizzarlo nel browser.

![Est DAM](./images/extdam7.png)

Il browser reindirizzerà alla finestra del terminale. Dovresti visualizzare un messaggio che indica che l&#39;accesso è stato eseguito correttamente **1} e un token lungo restituito dal browser.**

![Est DAM](./images/extdam8.png)

Il passaggio successivo consiste nel configurare l’istanza e il progetto Adobe IO da utilizzare per l’app DAM esterna.

A questo scopo, è necessario scaricare un file dal progetto Adobe IO configurato in precedenza.

Vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects){target="_blank"} e apri il progetto creato in precedenza, denominato `--aepUserLdap-- GSPeM EXT`. Apri l&#39;area di lavoro **Produzione**.

![Est DAM](./images/extdam9.png)

Fai clic su **Scarica tutto**. Verrà scaricato un file JSON.

![Est DAM](./images/extdam10.png)

Copia il file JSON dalla directory **Download** nella directory principale dell&#39;app DAM esterna.

![Est DAM](./images/extdam11.png)

Tornare alla finestra del terminale. Immettere il comando `aio app use XXX-YYY-Production.json`.

>[!NOTE]
>
>È necessario modificare il nome del file in modo che corrisponda al nome del file.

Una volta eseguito il comando, l’app DAM esterna ora sarà connessa al progetto Adobe IO con App Builder creato in precedenza.

![Est DAM](./images/extdam12.png)

## 1.6.3.3 Installare GenStudio Extensibility SDK

È quindi necessario installare **GenStudio Extensibility SDK**. Ulteriori dettagli su SDK sono disponibili qui: [https://github.com/adobe/genstudio-extensibility-sdk](https://github.com/adobe/genstudio-extensibility-sdk).

Per installare SDK, esegui questo comando nella finestra del terminale:

`npm install @adobe/genstudio-extensibility-sdk`

![Est DAM](./images/extdam13.png)

Dopo alcuni minuti, il SDK verrà installato.

![Est DAM](./images/extdam14.png)

## 1.6.3.4 Esaminare l&#39;app DAM esterna in Visual Studio Code

Aprire Visual Studio Code. Fare clic su **Apri...** per aprire una cartella.

![Est DAM](./images/extdam15.png)

Seleziona la cartella **genstudio-external-dam-app** contenente l&#39;app scaricata in precedenza.

![Est DAM](./images/extdam16.png)

Fare clic per aprire il file **.env**.

![Est DAM](./images/extdam17.png)

Il file **.env** è stato creato dal comando `aio app use` eseguito nel passaggio precedente e contiene le informazioni necessarie per connettersi al progetto Adobe IO con App Builder.

![Est DAM](./images/extdam18.png)

Ora devi creare 2 nuovi file nella directory principale della cartella:

- `.env.dev`. Fare clic sul pulsante **Nuovo file** e quindi immettere il nome file `.env.dev`.

![Est DAM](./images/extdam19.png)

- `.env.prod`.  Fare clic sul pulsante **Nuovo file** e quindi immettere il nome file `.env.prod`.

![Est DAM](./images/extdam20.png)

Questi file conterranno le credenziali necessarie per la connessione al bucket AWS S3 creato in precedenza.

```
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
AWS_BUCKET_NAME=
```

I campi **`AWS_ACCESS_KEY_ID`** e **`AWS_SECRET_ACCESS_KEY`** erano disponibili dopo la creazione dell&#39;utente IAM nell&#39;esercizio precedente. Vi è stato chiesto di annotarli, ora potete copiare i valori.

![ETL](./images/cred1.png)

Il campo **`AWS_REGION`** può essere preso dalla vista Home di AWS S3, accanto al nome del bucket. In questo esempio, la regione è **us-west-2**.

![ETL](./images/bucket2.png)

Il campo **`AWS_BUCKET_NAME`** deve essere `--aepUserLdap---gspem-dam`.

Queste informazioni ti consentono di aggiornare i valori di ciascuna di queste variabili.

```
AWS_ACCESS_KEY_ID=XXX
AWS_SECRET_ACCESS_KEY=YYY
AWS_REGION=us-west-2
AWS_BUCKET_NAME=--aepUserLdap---gspem-dam
```

Incollare il testo in entrambi i file, `.env.dev` e `.env.prod`. Non dimenticare di salvare le modifiche.

![Est DAM](./images/extdam21.png)


![Est DAM](./images/extdam22.png)

Quindi, tornare alla finestra del terminale. Esegui questo comando:

`export $(grep -v '^#' .env.dev | xargs)`

![Est DAM](./images/extdam23.png)

## 1.6.3.5 Esegui l&#39;app DAM esterna

Nella finestra del terminale, eseguire il comando `aio app run`. Dovrebbe vedere questo dopo 1-2 minuti.

![Est DAM](./images/extdam24.png)

Ora hai confermato che l’app è in esecuzione. Il passaggio successivo è quello di distribuirlo.

Innanzitutto, premi **CTRL+C** per interrompere l&#39;esecuzione dell&#39;app. Immettere quindi il comando `aio app deploy`. Questo comando distribuirà il codice in Adobe IO.

Di conseguenza, riceverai un URL simile per accedere all’applicazione distribuita:

`https://133309-201burgundyguan.adobeio-static.net/index.html`

![Est DAM](./images/extdam27.png)

A scopo di test, è ora possibile utilizzare tale URL come parametro della stringa di query aggiungendo `?ext=` come prefisso all&#39;URL precedente. Questo determina il parametro della stringa di query:

`?ext=https://133309-201burgundyguan.adobeio-static.net/index.html`

Vai a [https://experience.adobe.com/genstudio/create](https://experience.adobe.com/genstudio/create).

![Est DAM](./images/extdam25.png)

Quindi, aggiungi il parametro della stringa di query immediatamente prima del **#**. Il nuovo URL deve essere simile al seguente:

`https://experience.adobe.com/?ext=https://133309-201burgundyguan.adobeio-static.net/index.html#/@experienceplatform/genstudio/create`

La pagina verrà caricata come di consueto. Fai clic su **Banner** per iniziare a creare un nuovo banner.

![Est DAM](./images/extdam26.png)

Seleziona un modello e fai clic su **Usa**.

![Est DAM](./images/extdam28.png)

Fai clic su **Seleziona dal contenuto**.

![Est DAM](./images/extdam29.png)

Dovresti quindi essere in grado di selezionare il DAM esterno dall’elenco a discesa.

![Est DAM](./images/extdam30.png)

Quando apporti modifiche al codice nel computer locale, dovrai ridistribuire l’app. Quando ridistribuisci, utilizza questo comando del terminale:

`aio app deploy --force-build --force-deploy`

L&#39;app è ora pronta per essere pubblicata.

## Passaggi successivi

Vai a [Pubblica la tua app privatamente](./ex4.md){target="_blank"}

Torna a [GenStudio for Performance Marketing - Estensibilità](./genstudioext.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
