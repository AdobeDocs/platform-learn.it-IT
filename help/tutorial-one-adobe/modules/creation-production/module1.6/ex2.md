---
title: GenStudio for Performance Marketing Crea il bucket Amazon AWS S3
description: GenStudio for Performance Marketing Crea il bucket Amazon AWS S3
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 1dd8b487cbd16e438e9c006c34e458ddb82cce64
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 6%

---

# 1.6.2 Creare il bucket AWS S3

## 1.6.2.1 Crea il bucket S3

Vai a [https://console.aws.amazon.com](https://console.aws.amazon.com) e accedi.

>[!NOTE]
>
>Se non disponi ancora di un account AWS, crea un nuovo account AWS utilizzando il tuo indirizzo e-mail personale.

![ETL](./images/awshome.png)

Dopo l&#39;accesso, verrai reindirizzato a **AWS Management Console**.

![ETL](./images/awsconsole.png)

Nella barra di ricerca, cerca **s3**. Fare clic sul primo risultato della ricerca: **S3 - Storage scalabile nel cloud**.

![ETL](./images/awsconsoles3.png)

Verrà quindi visualizzata la home page di **Amazon S3**. Fai clic su **Crea bucket**.

![ETL](./images/s3home.png)

Nella schermata **Crea bucket**, utilizza il nome `--aepUserLdap---gspem-dam`.

![ETL](./images/bucketname.png)

Lascia invariate tutte le altre impostazioni predefinite. Scorri verso il basso e fai clic su **Crea bucket**.

![ETL](./images/createbucket.png)

Vedrai quindi il tuo bucket in fase di creazione e verrà reindirizzato alla home page di Amazon S3.

![ETL](./images/S3homeb.png)

## Impostare le autorizzazioni per accedere al bucket S3

Il passaggio successivo consiste nel configurare l’accesso al bucket S3.

Per eseguire questa operazione, vai a [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

L’accesso alle risorse di AWS è controllato da Amazon Identity and Access Management (IAM).

Ora vedrai questa pagina.

![ETL](./images/iam.png)

Nel menu a sinistra, fai clic su **Utenti**. Viene visualizzata la schermata **Utenti**. Fare clic su **Crea utente**.

![ETL](./images/iammenu.png)

Quindi, configura l’utente:

- Nome utente: utilizzare `s3_--aepUserLdap--_gspem_dam`

Fai clic su **Avanti**.

![ETL](./images/configuser.png)

Viene quindi visualizzata questa schermata delle autorizzazioni. Fai clic su **Allega criteri direttamente**.

![ETL](./images/perm1.png)

Immettere il termine di ricerca **s3** per visualizzare tutti i criteri S3 correlati. Selezionare il criterio **AmazonS3FullAccess**. Scorri verso il basso e fai clic su **Avanti**.

![ETL](./images/perm2.png)

Controlla la configurazione. Fare clic su **Crea utente**.

![ETL](./images/review.png)

Poi vedrai questo. Fare clic su **Visualizza utente**.

![ETL](./images/review1.png)

Fare clic su **Credenziali di protezione** e quindi su **Crea chiave di accesso**.

![ETL](./images/cred.png)

Selezionare **l&#39;applicazione in esecuzione all&#39;esterno di AWS**. Scorri verso il basso e fai clic su **Avanti**.

![ETL](./images/creda.png)

Fai clic su **Crea chiave di accesso**

![ETL](./images/credb.png)

Poi vedrai questo. Fai clic su **Mostra** per visualizzare la chiave di accesso segreta:

![ETL](./images/cred1.png)

È ora visualizzata la **chiave di accesso segreta**.

>[!IMPORTANT]
>
>Memorizzare le credenziali in un file di testo nel computer.
>
> - ID chiave di accesso: ...
> - Chiave di accesso segreta: ...
>
> Dopo aver fatto clic su **Fine** non verranno più visualizzate le credenziali.

Fai clic su **Fine**.

![ETL](./images/cred2.png)

Ora hai creato correttamente un bucket AWS S3 e hai creato un utente con autorizzazioni di accesso a questo bucket.

## 1.6.2.2 Carica Assets nel bucket S3

Nella barra di ricerca, cerca **s3**. Fare clic sul primo risultato della ricerca: **S3 - Storage scalabile nel cloud**.

![ETL](./images/bucket1.png)

Fai clic su per aprire il nuovo bucket S3 creato, che deve essere denominato `--aepUserLdap---gspem-dam`.

![ETL](./images/bucket2.png)

Fai clic su **Carica**.

![ETL](./images/bucket3.png)

Dovresti vedere questo.

![ETL](./images/bucket4.png)

È possibile scaricare i file immagine CitiSignal [qui](./../../asset-mgmt/module2.2/images/CitiSignal_Neon_Rabbit.zip){target="_blank"}.

Esportare i file sul desktop.

![ETL](./images/bucket5.png)

Prendi i 2 file di immagini in quella cartella e rilasciali nella finestra di caricamento del bucket S3. Fai clic su **Carica**.

![ETL](./images/bucket6.png)

Dovresti vedere questo. Il bucket S3, i file immagine e l’utente IAM sono ora pronti per essere utilizzati dall’app DAM esterna.

![ETL](./images/bucket7.png)

## Passaggi successivi

Vai a [Crea la tua app DAM esterna](./ex3.md){target="_blank"}

Torna a [GenStudio for Performance Marketing - Estensibilità](./genstudioext.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
