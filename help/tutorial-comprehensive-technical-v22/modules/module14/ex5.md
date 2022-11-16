---
title: 'Raccolta dati e inoltro eventi: eventi in avanti verso l’ecosistema AWS'
description: Inoltrare gli eventi verso l'ecosistema AWS
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 3d24e533-6eb4-40a7-a242-ba7f40839665
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2433'
ht-degree: 2%

---

# 14.5 Eventi in avanti verso l&#39;ecosistema AWS

>[!IMPORTANT]
>
>Il completamento di questo esercizio è facoltativo e comporta un costo per l’utilizzo di AWS Kinesis. Mentre AWS fornisce un account di livello gratuito che consente di testare e configurare molti servizi senza costi, AWS Kinesis non fa parte di tale account di livello gratuito. Quindi, per implementare e testare questo esercizio, sarà necessario sostenere un costo per l’utilizzo di AWS Kinesis.

## Buono a sapere

Adobe Experience Platform supporta vari servizi Amazon come destinazione.
Kinesis e S3 sono entrambi [destinazioni di esportazione del profilo](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en) e può essere utilizzato come parte di Adobe Experience Platform Real-Time CDP.
Puoi facilmente inserire nei tuoi sistemi selezionati eventi di segmento di alto valore e attributi di profilo associati.

In questa nota viene illustrato come impostare il proprio flusso Kinesis di Amazon per lo streaming dei dati degli eventi provenienti dall’ecosistema Adobe Experience Platform Edge verso una destinazione di archiviazione cloud, ad esempio Amazon S3. Questa funzione è utile nel caso in cui desideri raccogliere eventi di esperienza da proprietà web e mobili e inviarli al datalake per l’analisi e il reporting operativo. I database generalmente acquisiscono i dati in modo batch con importazioni di file giornaliere di grandi dimensioni, non espongono endpoint http pubblico che potrebbe essere utilizzato in combinazione con l’inoltro degli eventi.

Supportare i casi d’uso di cui sopra implica che i dati in streaming devono essere bufferizzati o messi in coda prima di essere scritti in un file. È necessario prestare attenzione a non aprire i file per l’accesso in scrittura in più processi. Delegare questo compito a un sistema dedicato è ideale per scalare bene garantendo al contempo un ottimo livello di servizio, è qui che Kinesis viene in soccorso.

Amazon Kinesis Data Streams si concentra sull&#39;acquisizione e la memorizzazione di flussi di dati. Kinesis Data Firehose si concentra sulla distribuzione di flussi di dati per determinate destinazioni, ad esempio bucket S3.

Come parte di questo esercizio,..

- Eseguire la configurazione di base di un flusso di dati Kinesis
- Crea un flusso di consegna Firehose e utilizza il bucket S3 come destinazione
- Configura il gateway API Amazon come endpoint api rest per ricevere i dati dell’evento
- Inoltrare i dati evento non elaborati da Adobe Edge al flusso Kinesis

## 14.5.1 Configura il bucket AWS S3

Vai a [https://console.aws.amazon.com](https://console.aws.amazon.com) e accedi con l’account Amazon creato in precedenza.

![ETL](../module6/images/awshome.png)

Dopo l&#39;accesso, verrai reindirizzato al **Console di gestione AWS**.

![ETL](../module6/images/awsconsole.png)

In **Trova servizi** menu, cerca **s3**. Fai clic sul primo risultato della ricerca: **S3 - Storage scalabile nel cloud**.

![ETL](../module6/images/awsconsoles3.png)

Vedrai il **Amazon S3** homepage. Fai clic su **Crea bucket**.

![ETL](../module6/images/s3home.png)

In **Crea bucket** è necessario configurare due elementi:

- Nome: utilizza il nome `eventforwarding---demoProfileLdap--`. Ad esempio, in questo esercizio il nome del bucket è **aepmodulertcdpvangeluw**
- Regione: utilizza la regione **UE (Francoforte) eu-central-1**

![ETL](./images/bucketname.png)

Lascia invariate tutte le altre impostazioni predefinite. Scorri verso il basso e fai clic su **Crea bucket**.

![ETL](./images/createbucket.png)

Vedrai quindi il tuo bucket creato e verrà reindirizzato alla home page di Amazon S3.

![ETL](./images/S3homeb.png)

## 14.5.2 Configurare AWS Kinesis Data Stream

In **Trova servizi** menu, cerca **cinesi**. Fai clic sul primo risultato della ricerca: **Kinesis - Utilizzo dei dati in streaming in tempo reale**.

![ETL](./images/kinesis1.png)

Seleziona **Flussi dati Kinesis**. Fai clic su **Creare un flusso di dati**.

![ETL](./images/kinesis2.png)

Per **Nome flusso dati**, utilizza `--demoProfileLdap---datastream`.

![ETL](./images/kinesis3.png)

Non è necessario modificare nessuna delle altre impostazioni. Scorri verso il basso e fai clic su **Creare un flusso di dati**.

![ETL](./images/kinesis4.png)

Vedrete questo. Una volta creato correttamente il flusso di dati, puoi passare all’esercizio successivo.

![ETL](./images/kinesis5.png)

## 14.5.3 Configura il flusso di distribuzione AWS Firehose

In **Trova servizi** menu, cerca **cinesi**. Fai clic su **Kinesis Data Firehose**.

![ETL](./images/kinesis6.png)

Fai clic su **Creare un flusso di consegna**.

![ETL](./images/kinesis7.png)

Per **Origine**, seleziona **Flussi dati Amazon Kinesis**. Per **Destinazione**, seleziona **Amazon S3**. Fai clic su **Sfoglia** per selezionare il flusso di dati.

![ETL](./images/kinesis8.png)

Seleziona il flusso di dati. Fai clic su **Scegli**.

![ETL](./images/kinesis9.png)

Vedrete questo. Ricorda **Nome del flusso di consegna** perché ne avrete bisogno più tardi.

![ETL](./images/kinesis10.png)

Scorri verso il basso fino a visualizzare **Impostazioni di destinazione**. Fai clic su **Sfoglia** per selezionare il bucket S3.

![ETL](./images/kinesis11.png)

Seleziona il tuo bucket S3 e fai clic su **Scegli**.

![ETL](./images/kinesis12.png)

Poi vedrete qualcosa del genere. Aggiorna le seguenti impostazioni:

- Partizionamento dinamico: impostato su **Abilitato**
- Disaggregazione di più record: impostato su **Disabilitato**
- Nuovo delimitatore di riga: impostato su **Abilitato**
- Analisi in linea per JSON: impostato su **Abilitato**

![ETL](./images/kinesis13.png)

Scorri un po&#39; verso il basso, poi vedrai questo. Aggiorna le seguenti impostazioni:

- Tasti di partizione dinamica
   - Nome chiave: **dynamicPartitioningKey**
   - Espressione JQ: **.dynamicPartitioningKey**
- Prefisso bucket S3: aggiungi il seguente codice:

```bash
!{partitionKeyFromQuery:dynamicPartitioningKey}/!{timestamp:yyyy}/!{timestamp:MM}/!{timestamp:dd}/!{timestamp:HH}/}
```

- Prefisso di uscita errore del bucket S3: impostato su **errore**

![ETL](./images/kinesis14.png)

Infine, scorri verso il basso e fai clic su **Creare un flusso di consegna**

![ETL](./images/kinesis15.png)

Dopo un paio di minuti, verrà creato il flusso di consegna e **Attivo**.

![ETL](./images/kinesis16.png)

## 14.5.4 Configura il tuo ruolo AWS IAM

In **Trova servizi** menu, cerca **iam**. Fai clic su **Gateway API**.

![ETL](./images/iam1.png)

Fai clic su **Ruoli**.

![ETL](./images/iam2.png)

Cerca il tuo **KinesisFirehose** ruolo. Fai clic su di esso per aprirlo.

![ETL](./images/iam3.png)

Fai clic sul nome del criterio delle autorizzazioni per aprirlo.

![ETL](./images/iam4.png)

Nella nuova schermata visualizzata, fai clic su **Modifica criterio**.

![ETL](./images/iam5.png)

Sotto **Kinesis** - **Azioni**, assicura che **Scrivi** autorizzazioni per **PutRecord** è abilitato. Fai clic su **Criteri di revisione**.

![ETL](./images/iam6.png)

Fai clic su **Salva modifiche**.

![ETL](./images/iam7.png)

Allora tornerai qui. Fai clic su **Ruoli**.

![ETL](./images/iam8.png)

Cerca il tuo **KinesisFirehose** ruolo. Fai clic su di esso per aprirlo.

![ETL](./images/iam3.png)

Vai a **Relazioni di trust** e fai clic su **Modifica criterio di attendibilità**.

![ETL](./images/iam9.png)

Sovrascrivi il criterio di attendibilità corrente incollando questo codice per sostituire il codice esistente:

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"Service": [
                    "firehose.amazonaws.com",
                    "kinesis.amazonaws.com",
                    "apigateway.amazonaws.com"
                ]
			},
			"Action": "sts:AssumeRole"
		}
	]
}
```

Fai clic su **Aggiorna criterio**

![ETL](./images/iam10.png)

Vedrete questo. È necessario specificare il **ARN** per questo ruolo nel passaggio successivo.

![ETL](./images/iam11.png)

## 14.5.5 Configurare il gateway API di AWS

Amazon API Gateway è un servizio AWS per la creazione, la pubblicazione, la manutenzione, il monitoraggio e la protezione delle API REST, HTTP e WebSocket su qualsiasi scala. Gli sviluppatori API possono creare API che accedono ad AWS o ad altri servizi web, nonché dati memorizzati in AWS Cloud.

Ora puoi esporre il flusso di dati Kinesis a Internet tramite un endpoint HTTPS che può essere utilizzato direttamente dai servizi Adobe, come Event Forwarding.

In **Trova servizi** menu, cerca **gateway api**. Fai clic su **Gateway API**.

![ETL](./images/kinesis17.png)

Poi vedrete qualcosa del genere. Fai clic su **Creare API**.

![ETL](./images/kinesis18.png)

Fai clic su **Crea** sulla **API REST** il Card.

![ETL](./images/kinesis19.png)

Vedrete questo. Compila le impostazioni come segue:

- Scegli il protocollo: select **REST**
- Crea nuova API: select **Nuova API**
- Impostazioni:
   - Nome API: use `--demoProfileLdap---eventforwarding`
   - Tipo endpoint: select **Regionale**

Fai clic su **Creare API**.

![ETL](./images/kinesis20.png)

Vedrete questo. Fai clic su **Azioni** quindi fai clic su **Crea risorsa**.

![ETL](./images/kinesis21.png)

Vedrete questo. Imposta **Nome risorsa** a **flusso**. Fai clic su **Crea risorsa**.

![ETL](./images/kinesis22.png)

Vedrete questo. Fai clic su **Azioni** quindi fai clic su **Metodo Create**.

![ETL](./images/kinesis23.png)

Nel menu a discesa , seleziona **POST** e fai clic su **v** pulsante .

![ETL](./images/kinesis24.png)

Vedrete questo. Compila le impostazioni come segue:

- Tipo di integrazione: **Servizio AWS**
- Regione AWS: seleziona la regione utilizzata dal flusso di dati Kinesis, in questo caso: **us-west-2**
- Servizio AWS: select **Kinesis**
- Sottodominio AWS: lascia vuoto
- Metodo HTTP: select **POST**
- Tipo azione: select **Usa nome azione**
- Azione: enter **PutRecord**
- Ruolo di esecuzione: incolla **ARN** del ruolo di esecuzione utilizzato dal Kinesis Data Firehose, come indicato nell&#39;esercizio precedente
- Gestione dei contenuti: select **Passaggio**
- Usa timeout predefinito: attiva la casella di controllo

Fai clic su **Salva**.

![ETL](./images/kinesis25.png)

Vedrete questo. Fai clic su **Richiesta di integrazione**.

![ETL](./images/kinesis27.png)

Fai clic su **Intestazioni HTTP**.

![ETL](./images/kinesis28.png)

Scorri verso il basso e fai clic su **Aggiungi intestazione**.

![ETL](./images/kinesis29.png)

Imposta **Nome** a **Content-Type**, set **Mappata da** a `'application/x-amz-json-1.1'`. Fai clic sul pulsante **v** per salvare le modifiche.

![ETL](./images/kinesis30.png)

Vedrete questo. Per **Richiedi passaggio del corpo**, seleziona **In assenza di modelli definiti (consigliato)**. Quindi, fai clic su **Aggiungi modello di mappatura**.

![ETL](./images/kinesis31.png)

Sotto **Content-Type**, inserisci **application/json**. Fai clic sul pulsante **v** per salvare le modifiche.

![ETL](./images/kinesis32.png)

Scorri verso il basso per trovare una finestra dell&#39;editor di codice. Incolla qui il codice seguente:

```json
{
  "StreamName": "$input.path('StreamName')",
  "Data": "$util.base64Encode($input.json('$.Data'))",
  "PartitionKey": "$input.path('$.PartitionKey')"
}
```

Fai clic su **Salva**.

![ETL](./images/kinesis33.png)

Quindi, scorri verso l’alto e fai clic su **&lt;- Esecuzione del metodo** per tornare indietro.

![ETL](./images/kinesis34.png)

Fai clic su **PROVA**.

![ETL](./images/kinesis35.png)

Scorri verso il basso e incolla questo codice in **Corpo della richiesta**. Fai clic su **Test**.

```json
{
  "Data": {
    "message": "Hello World",
    "dynamicPartitioningKey": "v2"
  },
  "PartitionKey": "1",
  "StreamName": "--demoProfileLdap---datastream"
}
```

![ETL](./images/kinesis36.png)

Verrà quindi visualizzato un risultato simile:

![ETL](./images/kinesis37.png)

Vedrete questo. Fai clic su **Azioni** quindi fai clic su **Implementare l’API**.

![ETL](./images/kinesis38.png)

Per **Fase di distribuzione**, seleziona **Nuovo stadio**. Come **Nome della fase**, inserisci **prod**. Fai clic su **Distribuzione**.

![ETL](./images/kinesis39.png)

Vedrete questo. Fai clic su **Salva modifiche**. FYI: l’URL nell’immagine è l’URL a cui inviare i dati (in questo esempio: https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod).

![ETL](./images/kinesis40.png)

Puoi testare la tua configurazione utilizzando la seguente richiesta cURL, tutto quello che devi fare è sostituire l&#39;URL seguente con il tuo, `https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod` in questo esempio, e aggiungi `/stream` alla fine dell’URL.

```json
curl --location --request POST 'https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod/stream' \
--header 'Content-Type: application/json' \
--data-raw '{
    "Data": {
        "userid": "--demoProfileLdap--@adobe.com",
        "firstName":"--demoProfileLdap--",
        "offerName":"10% off on outdoor gears",
        "offerCode": "10OFF-SPRING",
        "dynamicPartitioningKey": "campaign"
    },
    "PartitionKey": "1",
    "StreamName": "--demoProfileLdap---datastream"
}'
```

Incolla il codice aggiornato di cui sopra in una finestra Terminal e premi invio. Verrà quindi visualizzata questa risposta, simile alla risposta che potresti visualizzare durante il test precedente.

![ETL](./images/kinesis41.png)

## 14.5.6 Aggiorna la proprietà Event Forwarding

È ora possibile eseguire l’attivazione nel flusso di dati di AWS Kinesis tramite gateway API di AWS, in modo da poter inviare eventi di esperienza grezzi all’ecosistema AWS. Utilizzando Connessioni Real-Time CDP e Inoltro eventi, ora puoi facilmente abilitare l’inoltro degli eventi all’endpoint gateway API di AWS appena creato.

### 14.5.6.1 Aggiorna la proprietà Event Forwarding : Creare un elemento dati

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) e vai a **Inoltro eventi**. Cerca la proprietà Event Forwarding e fai clic su di essa per aprirla.

![SSF raccolta dati Adobe Experience Platform](./images/prop1.png)

Nel menu a sinistra, vai a **Elementi dati**. Fai clic su **Aggiungi elemento dati**.

![SSF raccolta dati Adobe Experience Platform](./images/deaws1.png)

Verrà quindi visualizzato un nuovo elemento dati da configurare.

![SSF raccolta dati Adobe Experience Platform](./images/de2.png)

Effettua la selezione seguente:

- Come **Nome**, inserisci **awsDataObject**.
- Come **Estensione**, seleziona **Core**.
- Come **Tipo di elemento dati**, seleziona **Codice personalizzato**.

Ora avrà questo. Fai clic su **&lt;/> Open Editor**.

![SSF raccolta dati Adobe Experience Platform](./images/deaws3.png)

Nell’editor, incolla il seguente codice alla riga 3. Fai clic su **Salva**.

```javascript
const newObj = {...arc.event.xdm, dynamicPartitioningKey: "event_forwarding"}
return JSON.stringify(newObj);
```

![SSF raccolta dati Adobe Experience Platform](./images/deaws4.png)

>[!NOTE]
>
>Nel percorso precedente viene fatto riferimento a **arc**. **arc** sta per contesto risorsa Adobe e **arc** sta sempre per l&#39;oggetto disponibile più alto disponibile nel contesto lato server. Arricchimenti e trasformazioni possono essere aggiunti a quello **arc** mediante le funzioni di Adobe Experience Platform Data Collection Server.
>
>Nel percorso precedente viene fatto riferimento a **event**. **event** sta per un evento univoco e Adobe Experience Platform Data Collection Server valuterà sempre ogni singolo evento. A volte è possibile visualizzare un riferimento a **events** nel payload inviato dal lato client dell’SDK per web, ma in Adobe Experience Platform Data Collection Event Forwarding, ogni evento viene valutato singolarmente.

Allora tornerai qui. Fai clic su **Salva** o **Salva nella libreria**.

![SSF raccolta dati Adobe Experience Platform](./images/deaws5.png)

### 14.5.6.2 Aggiorna la proprietà Adobe Experience Platform Data Collection Server : Aggiorna la regola

Nel menu a sinistra, vai a **Regole**. Fai clic per aprire la regola **Tutte le pagine** creato in uno degli esercizi precedenti.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws1.png)

Vedrete questo. Fai clic sul pulsante **+** per aggiungere una nuova azione.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws2.png)

Vedrete questo. Effettua la selezione seguente:

- Seleziona la **Estensione**: **Connettore cloud di Adobe**.
- Seleziona la **Tipo di azione**: **Fai una chiamata di recupero**.

Questo dovrebbe darvi questo **Nome**: **Connettore cloud di Adobe - Effettua una chiamata di recupero**. Ora dovresti vedere quanto segue:

![SSF raccolta dati Adobe Experience Platform](./images/rl4.png)

Quindi, configura quanto segue:

- Modifica il metodo di richiesta da GET a **POST**
- Inserisci l’URL dell’endpoint gateway API AWS creato in uno dei passaggi precedenti, simile al seguente: `https://vv1i5vwg2k.execute-api.us-west-2.amazonaws.com/prod/stream`

Dovrebbe avere questo ora. Quindi, vai a **Intestazioni**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws5.png)

Sotto le intestazioni, aggiungi una nuova intestazione con chiave **Content-Type** e valore **application/json**. Quindi, vai a **Corpo**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws5a.png)

Vedrete questo. Incolla il seguente codice nel campo . **Corpo (grezzo)**. Fai clic su **Mantieni modifiche**.

```json
{
    "Data":{{awsDataObject}},
    "PartitionKey": "1",
    "StreamName": "--demoProfileLdap---datastream"
}
```

![SSF raccolta dati Adobe Experience Platform](./images/rlaws7.png)

Vedrete che sarà di nuovo qui. Fai clic su **Salva** o **Salva nella libreria**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws10.png)

Ora hai configurato la tua prima regola in una proprietà Inoltro eventi. Vai a **Flusso di pubblicazione** per pubblicare le modifiche.
Apri la libreria Sviluppo facendo clic su **Principale**.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws11.png)

Fai clic sul pulsante **Aggiungi tutte le risorse modificate** , dopodiché vedrai le modifiche a Rule e Data Element apparire in questa libreria. Quindi, fai clic su **Salva e genera per sviluppo**. Le modifiche vengono ora distribuite.

![SSF raccolta dati Adobe Experience Platform](./images/rlaws13.png)

Dopo un paio di minuti, vedrai che la distribuzione è completata e pronta per essere testata.

![SSF raccolta dati Adobe Experience Platform](./images/rl14.png)

## 14.5.7 Verifica la configurazione

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, vedrai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](../module0/images/web8.png)

Ora puoi seguire il flusso seguente per accedere al sito web. Fai clic su **Integrazioni**.

![DSN](../module0/images/web1.png)

Sulla **Integrazioni** pagina , devi selezionare la proprietà Raccolta dati creata nell&#39;esercizio 0.1.

![DSN](../module0/images/web2.png)

Vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../module0/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../module0/images/web4.png)

Incolla l’URL del sito web dimostrativo che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l&#39;accesso utilizzando il tuo Adobe ID.

![DSN](../module0/images/web5.png)

Seleziona il tipo di account e completa il processo di accesso.

![DSN](../module0/images/web6.png)

Il sito web verrà quindi caricato in una finestra del browser in incognito. Per ogni dimostrazione, è necessario utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../module0/images/web7.png)

Quando apri il browser Developer View, puoi controllare le richieste di rete come indicato di seguito. Quando utilizzi il filtro **interagire**, vedrai le richieste di rete inviate dal client di raccolta dati di Adobe Experience Platform ad Adobe Edge.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hook1.png)

Se selezioni il payload non elaborato, vai a [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) e incolla il payload. Fai clic su **Rendi carino**. Vedrai quindi il payload JSON, il **events** e **xdm** oggetto. In uno dei passaggi precedenti, quando hai definito l’elemento dati, hai utilizzato il riferimento **arc.event.xdm**, che consente di analizzare il **xdm** oggetto del payload.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hook2.png)

Cambia la visualizzazione in **AWS**. Aprendo il flusso di dati e entrando nel **Monitoraggio** , verrà ora visualizzato il traffico in entrata.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hookaws3.png)

Quando poi apri il flusso di consegna e vai nel **Monitoraggio** , vedrai anche il traffico in entrata.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hookaws4.png)

Infine, quando guardi il tuo bucket S3, noterai che i file vengono creati lì come conseguenza dell’inserimento dei dati.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hookaws5.png)

Quando scarichi un file di questo tipo e lo apri utilizzando un editor di testo, vedrai che contiene il payload XDM dagli eventi inoltrati.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hookaws6.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 14](./aep-data-collection-ssf.md)

[Torna a tutti i moduli](./../../overview.md)
