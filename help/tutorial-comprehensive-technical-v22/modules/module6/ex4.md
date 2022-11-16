---
title: Real-time CDP - Crea un segmento e azione - Invia il segmento a una destinazione S3
description: Real-time CDP - Crea un segmento e azione - Invia il segmento a una destinazione S3
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 5b0bcd69-7131-48a3-bd3e-773ba95cc42b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 3%

---

# 6.4 Intervenire: invia il segmento a una destinazione S3

Adobe Experience Platform può anche condividere i tipi di pubblico per e-mail Marketing Destinations come Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys e Adobe Campaign.

Puoi utilizzare FTP o SFTP come parte delle destinazioni dedicate per ciascuna di queste destinazioni di e-mail marketing, oppure puoi utilizzare AWS S3 per scambiare elenchi di clienti tra Adobe Experience Platform e queste destinazioni di e-mail marketing.

In questo modulo, configurerai tale destinazione utilizzando un bucket AWS S3.

## 6.4.1 Crea il tuo bucket S3

Vai a [https://console.aws.amazon.com](https://console.aws.amazon.com) e accedi con l’account Amazon creato in precedenza.

![ETL](./images/awshome.png)

Dopo l&#39;accesso, verrai reindirizzato al **Console di gestione AWS**.

![ETL](./images/awsconsole.png)

In **Trova servizi** menu, cerca **s3**. Fai clic sul primo risultato della ricerca: **S3 - Storage scalabile nel cloud**.

![ETL](./images/awsconsoles3.png)

Vedrai il **Amazon S3** homepage. Fai clic su **Crea bucket**.

![ETL](./images/s3home.png)

In **Crea bucket** è necessario configurare due elementi:

- Nome: utilizza il nome `aepmodulertcdp--demoProfileLdap--`. Ad esempio, in questo esercizio il nome del bucket è **aepmodulertcdpvangeluw**
- Regione: utilizza la regione **UE (Francoforte) eu-central-1**

![ETL](./images/bucketname.png)

Lascia invariate tutte le altre impostazioni predefinite. Scorri verso il basso e fai clic su **Crea bucket**.

![ETL](./images/createbucket.png)

Vedrai quindi il tuo bucket creato e verrà reindirizzato alla home page di Amazon S3.

![ETL](./images/S3homeb.png)

## 6.4.2 Imposta le autorizzazioni per accedere al tuo bucket S3

Il passaggio successivo consiste nel configurare l’accesso al bucket S3.

Per farlo, vai a [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

L’accesso alle risorse AWS è controllato da Amazon Identity and Access Management (IAM).

Ora visualizzerai questa pagina.

![ETL](./images/iam.png)

Nel menu a sinistra, fai clic su **Utenti**. Vedrai il **Utenti** schermo. Fai clic su **Aggiungi utenti**.

![ETL](./images/iammenu.png)

Quindi, configura l&#39;utente:

- Nome utente: use `s3_--demoProfileLdap--_rtcdp` come nome, quindi in questo esempio il nome è `s3_vangeluw_rtcdp`.
- Tipo di accesso AWS: select **Chiave di accesso - Accesso programmatico**.

Fai clic su **Avanti: Autorizzazioni**.

![ETL](./images/configuser.png)

Verrà visualizzata la schermata delle autorizzazioni. Fai clic su **Allegare direttamente le politiche esistenti**.

![ETL](./images/perm1.png)

Inserisci il termine di ricerca **s3** per visualizzare tutti i criteri S3 correlati. Selezionare il criterio **AmazonS3FullAccess**. Fai clic su **Avanti: Tag**.

![ETL](./images/perm2.png)

Sulla **Tag** non è necessario configurare nulla. Fai clic su **Avanti: Revisione**.

![ETL](./images/perm3.png)

Rivedi la tua configurazione. Fai clic su **Crea utente**.

![ETL](./images/review.png)

L&#39;utente viene creato e vengono visualizzate le credenziali per accedere all&#39;ambiente S3. Questa è l&#39;unica volta che vedrete le vostre credenziali, quindi vi prego di annotarle.

![ETL](./images/cred.png)

Fai clic su **Mostra** per visualizzare la chiave di accesso segreta:

![ETL](./images/cred1.png)

>[!IMPORTANT]
>
>Memorizzare le credenziali in un file di testo nel computer.
>
> - ID chiave di accesso: ...
> - Chiave di accesso segreta: ...
>
> Una volta fatto clic **Chiudi** non vedrai mai più le tue credenziali!

Fai clic su **Chiudi**.

![ETL](./images/close.png)

Ora hai creato correttamente un bucket AWS S3 e hai creato un utente con le autorizzazioni per accedere a questo bucket.

## 6.4.3 Configurare la destinazione in Adobe Experience Platform

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](../module2/images/sb1.png)

Nel menu a sinistra, vai a **Destinazioni**, quindi vai a **Catalogo**. Vedrai il **Catalogo delle destinazioni**.

![RTCDP](./images/rtcdpmenudest.png)

Fai clic su **Archiviazione cloud**, quindi fai clic su **Configurazione** pulsante (o attivato) **Attiva segmenti**, a seconda dell&#39;ambiente) **Amazon S3** il Card.

![RTCDP](./images/rtcdp2.png)

A seconda dell’ambiente, potrebbe essere necessario fare clic su **+ Configura nuova destinazione** per iniziare a creare la destinazione.

![RTCDP](./images/rtcdp2a.png)

Seleziona **Nuovo account** come Tipo di conto. Utilizza le credenziali S3 che ti sono state fornite nel passaggio precedente:

| ID chiave di accesso | Chiave di accesso segreto |
|:-----------------------:| :-----------------------:|
| AKIA.... | Cm5Ln.... |

Fai clic su **Connetti alla destinazione**.

![RTCDP](./images/rtcdpsfs3.png)

Viene quindi visualizzata una conferma visiva della connessione della destinazione.

![RTCDP](./images/rtcdpsfs3connected.png)

È necessario specificare un nome e una cartella in modo che Adobe Experience Platform possa connettersi al bucket S3.

Come convenzione di denominazione, utilizza quanto segue:

| ID chiave di accesso | Chiave di accesso segreto |
|:-----------------------:| :-----------------------:|
| Nome | `AWS - S3 - --demoProfileLdap--` |
| Descrizione | `AWS - S3 - --demoProfileLdap--` |
| Nome blocco | `aepmodulertcdp--demoProfileLdap--` |
| Percorso cartella | / |

Fai clic su **Avanti**.

![RTCDP](./images/rtcdpsfs3connect2.png)

È ora possibile allegare facoltativamente un criterio di governance dei dati alla nuova destinazione. Fai clic su **Avanti**.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

Nell’elenco dei segmenti, cerca il segmento creato nell’esercizio 1 e selezionalo. Fai clic su **Avanti**.

![RTCDP](./images/s3a.png)

Vedrete questo. Se lo desideri, puoi modificare la pianificazione facendo clic sul pulsante **matita** icona. **Crea pianificazione**.

![RTCDP](./images/s3bb.png)

Definisci il tuo programma di scelta. Seleziona **Esportare file incrementali** e impostare la frequenza su **Orario** ogni **3 ore**. Fai clic su **Crea**.

![RTCDP](./images/s3bbc.png)

Poi avrai questo. Fai clic su **Avanti**.

![RTCDP](./images/s3bbca.png)

Ora puoi selezionare gli attributi per l’esportazione in AWS S3. Fai clic su **Aggiungi nuovo campo** e garantire il campo `--aepTenantId--.identification.core.ecid` viene aggiunto e contrassegnato come **Chiave di deduplicazione**.

Facoltativamente, puoi aggiungere tutti gli altri campi necessari.

Dopo aver aggiunto tutti i campi, fai clic su **Successivo**.

![RTCDP](./images/s3c.png)

Rivedi la tua configurazione. Fai clic su **Fine** per completare la configurazione.

![RTCDP](./images/s3g.png)

Tornerai quindi alla schermata Attivazione destinazione e vedrai il segmento aggiunto a questa destinazione.

![RTCDP](./images/s3j.png)

Per aggiungere altre esportazioni di segmenti, puoi fare clic su **Attiva segmenti** per riavviare il processo e aggiungere altri segmenti.

![RTCDP](./images/s3k.png)

Passaggio successivo: [6.5 Intervenire: inviare il segmento ad Adobe Target](./ex5.md)

[Torna al modulo 6](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../overview.md)
