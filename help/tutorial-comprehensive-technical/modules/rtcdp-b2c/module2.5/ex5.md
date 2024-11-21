---
title: 'Raccolta dati e inoltro eventi: inoltro di eventi verso l’ecosistema AWS'
description: Inoltra gli eventi verso l’ecosistema AWS
kt: 5342
doc-type: tutorial
exl-id: 87c2c85d-f624-4972-a9c6-32ddf8a39570
source-git-commit: 7779e249b4ca03c243cf522811cd81370002d51a
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 2%

---

# 2.5.5 Inoltrare gli eventi ad AWS Kinesis e AWS S3

>[!IMPORTANT]
>
>Il completamento di questo esercizio è facoltativo e implica un costo per l’utilizzo di AWS Kinesis. AWS offre un account di livello gratuito che consente di testare e configurare molti servizi senza costi aggiuntivi, ma AWS Kinesis non fa parte di tale account di livello gratuito. Pertanto, al fine di implementare e testare questo esercizio, sarà coinvolto un costo per l’utilizzo di AWS Kinesis.

## Buono a sapersi

Adobe Experience Platform supporta vari servizi Amazon come destinazione.
Kinesis e S3 sono entrambe [destinazioni di esportazione profilo](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en) e possono essere utilizzate come parte di Adobe Experience Platform Real-Time CDP.
Puoi inserire facilmente eventi di segmento di alto valore e gli attributi di profilo associati nei sistemi preferiti.

In questo esercizio imparerai a configurare il tuo flusso Kinesis di Amazon per inviare in streaming i dati dell’evento provenienti dall’ecosistema Edge di Adobe Experience Platform a una destinazione di archiviazione cloud, come Amazon S3. Questa funzione è utile quando desideri raccogliere eventi di esperienza da proprietà web e mobili e inviarli nel data lake per l’analisi e il reporting operativo. I Datalake generalmente acquisiscono i dati in modalità batch con importazioni giornaliere di file di grandi dimensioni, non espongono un endpoint http pubblico che potrebbe essere utilizzato insieme all’inoltro di eventi.

Il supporto dei casi d’uso di cui sopra implica che i dati in streaming devono essere inseriti nel buffer o in una coda prima di essere scritti in un file. Fare attenzione a non aprire il file per l&#39;accesso in scrittura in più processi. La delega di questa attività a un sistema dedicato è ideale per garantire una buona scalabilità e un livello di servizio elevato, ed è qui che Kinesis interviene in caso di emergenza.

I flussi di dati di Amazon Kinesis si concentrano sull’acquisizione e l’archiviazione dei flussi di dati. Kinesis Data Firehose si concentra sulla distribuzione di flussi di dati a destinazioni selezionate, ad esempio bucket S3.

Come parte di questo esercizio...

- Eseguire una configurazione di base di un flusso di dati Kinesis
- Creare un flusso di consegna Firehose e utilizzare il bucket S3 come destinazione
- Configurare il gateway API di Amazon come endpoint API rest per ricevere i dati dell’evento
- Inoltrare i dati grezzi dell’evento da Edge di Adobe al flusso Kinesis

## Configurare il bucket AWS S3

Vai a [https://console.aws.amazon.com](https://console.aws.amazon.com) e accedi con il tuo account Amazon.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awshome.png)

Dopo l&#39;accesso, verrai reindirizzato a **AWS Management Console**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awsconsole.png)

Nel menu **Trova servizi**, cerca **s3**. Fare clic sul primo risultato della ricerca: **S3 - Storage scalabile nel cloud**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awsconsoles3.png)

Verrà quindi visualizzata la home page di **Amazon S3**. Fai clic su **Crea bucket**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/s3home.png)

Nella schermata **Crea bucket**, è necessario configurare due elementi:

- Nome: utilizzare il nome `eventforwarding---aepUserLdap--`.

![ETL](./images/bucketname.png)

Lascia invariate tutte le altre impostazioni predefinite. Scorri verso il basso e fai clic su **Crea bucket**.

![ETL](./images/createbucket.png)

Vedrai quindi il tuo bucket in fase di creazione e verrà reindirizzato alla home page di Amazon S3.

![ETL](./images/S3homeb.png)

## Configurare il flusso di dati di AWS Kinesis

Nel menu **Trova servizi**, cerca **kinesis**. Fare clic sul primo risultato della ricerca: **Kinesis - Utilizzare dati in streaming in tempo reale**.

![ETL](./images/kinesis1.png)

Selezionare **Flussi dati Kinesis**. Fare clic su **Crea flusso di dati**.

![ETL](./images/kinesis2.png)

Per il **nome flusso dati**, utilizzare `--aepUserLdap---datastream`.

![ETL](./images/kinesis3.png)

Non è necessario modificare nessuna delle altre impostazioni. Scorri verso il basso e fai clic su **Crea flusso di dati**.

![ETL](./images/kinesis4.png)

Poi vedrai questo. Una volta creato correttamente il flusso di dati, puoi passare all’esercizio successivo.

![ETL](./images/kinesis5.png)

## Configurare il flusso di consegna AWS Firehose

Nel menu **Trova servizi**, cerca **kinesis**. Fare clic su **Kinesis Data Firehose**.

![ETL](./images/kinesis6.png)

Fare clic su **Crea flusso Firehose**.

![ETL](./images/kinesis7.png)

Per **Source**, selezionare **Flussi dati Amazon Kinesis**. Per **Destinazione**, selezionare **Amazon S3**. Fai clic su **Sfoglia** per selezionare il flusso di dati.

![ETL](./images/kinesis8.png)

Seleziona il flusso di dati. Fai clic su **Scegli**.

![ETL](./images/kinesis9.png)

Poi vedrai questo. Ricorda il nome di flusso **Firehose**, che ti servirà in seguito.

![ETL](./images/kinesis10.png)

Scorri verso il basso fino a visualizzare **Impostazioni di destinazione**. Fai clic su **Sfoglia** per selezionare il bucket S3.

![ETL](./images/kinesis11.png)

Seleziona il bucket S3 e fai clic su **Scegli**.

![ETL](./images/kinesis12.png)

Poi vedrai qualcosa del genere. Aggiorna le seguenti impostazioni:

- Nuovo delimitatore di riga: impostato su **Abilitato**
- Partizionamento dinamico: impostato su **Non abilitato**

![ETL](./images/kinesis13.png)

Scorri verso il basso ancora e fai clic su **Crea flusso Firehose**

![ETL](./images/kinesis15.png)

Dopo alcuni minuti verrà creato il flusso Firehose e **Attivo**.

![ETL](./images/kinesis16.png)

## Crea utente IAM

Nel menu IAM di AWS a sinistra, fai clic su **Utenti**. Viene visualizzata la schermata **Utenti**. Fare clic su **Crea utente**.

![ETL](./images/iammenu.png)

Quindi, configura l’utente:

- Nome utente: utilizzare `--aepUserLdap--_kinesis_forwarding`

Fai clic su **Avanti**.

![ETL](./images/configuser.png)

Viene quindi visualizzata questa schermata delle autorizzazioni. Fai clic su **Allega criteri direttamente**.

Immettere il termine di ricerca **kinesisfirehose** per visualizzare tutti i criteri correlati. Seleziona il criterio **AmazonKinesisFirehoseFullAccess**. Scorri verso il basso e fai clic su **Avanti**.

![ETL](./images/perm2.png)

Controlla la configurazione. Fare clic su **Crea utente**.

![ETL](./images/review.png)

Poi vedrai questo. Fare clic su **Visualizza utente**.

![ETL](./images/review1.png)

Fare clic su **Aggiungi autorizzazioni** e su **Crea criterio in linea**.

![ETL](./images/pol1.png)

Poi vedrai questo. Selezionare il servizio **Kinesis**.

![ETL](./images/pol2.png)

Vai a **Scrivi** e seleziona la casella di controllo per **PutRecord**.

![ETL](./images/pol3.png)

Scorri verso il basso fino a **Risorse** e seleziona **Tutto**. Fai clic su **Avanti**.

![ETL](./images/pol4.png)

Assegna un nome al criterio: **Kinesis_PutRecord** e fai clic su **Crea criterio**.

![ETL](./images/pol5.png)

Poi vedrai questo. Fare clic su **Credenziali di protezione**.

![ETL](./images/pol6.png)

Fai clic su **Crea chiave di accesso**.

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

Ora hai creato correttamente un utente IAM con le autorizzazioni appropriate, che dovrai specificare durante la configurazione dell&#39;estensione AWS nella proprietà Inoltro eventi.

## Aggiorna la proprietà di Inoltro eventi: Extension

Con il segreto e l’elemento dati configurati, ora puoi impostare l’estensione per Google Cloud Platform nella proprietà Inoltro eventi.

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/), vai a **Inoltro eventi** e apri la tua proprietà Inoltro eventi.

![SSF raccolta dati Adobe Experience Platform](./images/prop1.png)

Quindi, vai a **Estensioni**, a **Catalogo**. Fai clic sull&#39;estensione **AWS** e fai clic su **Installa**.

![SSF raccolta dati Adobe Experience Platform](./images/awsext1.png)

Immettere le credenziali utente IAM generate nell&#39;esercizio precedente. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/awsext2.png)

Successivamente, devi configurare una regola che avvii l’inoltro dei dati dell’evento a Kinesis.

## Aggiorna la proprietà di inoltro eventi: regola

Nel menu a sinistra, vai a **Regole**. Fare clic per aprire la regola **Tutte le pagine** creata in uno degli esercizi precedenti.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws1.png)

Poi vedrai questo. Fai clic sull&#39;icona **+** per aggiungere una nuova azione.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws2.png)

Poi vedrai questo. Effettua la seguente selezione:

- Seleziona l&#39;**estensione**: **AWS**
- Seleziona il **Tipo azione**: **Invia dati al flusso di dati di Kinesis**
- Nome: **AWS - Invia dati al flusso di dati Kinesis**

Ora dovresti vedere:

![SSF raccolta dati Adobe Experience Platform](./images/rlaws4.png)

Quindi, configura quanto segue:

- Nome flusso: `--aepUserLdap---datastream`
- Area geografica di AWS: controlla la tua area geografica nella configurazione del flusso di dati di AWS
- Chiave partizione: **0**

Puoi visualizzare la tua regione AWS qui:

![SSF raccolta dati Adobe Experience Platform](./images/partkey.png)

Ora dovresti avere questo. Fare clic sull&#39;icona dell&#39;elemento dati per il campo **Dati**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws5.png)

Seleziona **Evento XDM** e fai clic su **Seleziona**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws5a.png)

Allora avrai questo. Fai clic su **Mantieni modifiche**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws5b.png)

Poi vedrai questo. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws7.png)

Vai a **Flusso di pubblicazione** per pubblicare le modifiche.
Apri la libreria di sviluppo facendo clic su **Principale**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws11.png)

Fai clic sul pulsante **Aggiungi tutte le risorse modificate**, dopo di che le modifiche apportate alla regola e all&#39;elemento dati verranno visualizzate in questa libreria. Fare clic su **Salva e genera per sviluppo**. Le modifiche sono ora in fase di implementazione.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws13.png)

Dopo un paio di minuti, vedrai che l’implementazione è completata e pronta per essere testata.

![SSF raccolta dati Adobe Experience Platform](./images/rl14.png)

## Verifica la configurazione

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni esercizio, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Passa a **AWS**. Aprendo il flusso di dati e andando nella scheda **Monitoraggio**, ora vedrai il traffico in arrivo.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hookaws3.png)

Quando apri il flusso Data Firehose e vai alla scheda **Monitoraggio**, verrà visualizzato anche il traffico in arrivo.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hookaws4.png)

Infine, quando analizzi il bucket S3, noterai che i file vengono creati lì in seguito all’acquisizione dei dati.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hookaws5.png)

Quando scarichi tale file e lo apri utilizzando un editor di testo, vedrai che contiene il payload XDM dagli eventi inoltrati.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hookaws6.png)

>[!IMPORTANT]
>
>Una volta che la configurazione funziona come previsto, non dimenticare di attivare AWS Kinesis Data Stream e Data Firehose per evitare di essere caricati!

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2.5](./aep-data-collection-ssf.md)

[Torna a tutti i moduli](./../../../overview.md)
