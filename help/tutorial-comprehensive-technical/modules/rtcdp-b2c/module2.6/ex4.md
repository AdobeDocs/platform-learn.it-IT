---
title: Installare e configurare Kafka Connect e il connettore Adobe Experience Platform Sink
description: Installare e configurare Kafka Connect e il connettore Adobe Experience Platform Sink
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 0%

---

# 2.6.4 Installare e configurare Kafka Connect e il connettore Adobe Experience Platform Sink

## 2.6.4.1 Scaricare il connettore Adobe Experience Platform Sink

Vai a [https://github.com/adobe/experience-platform-streaming-connect/releases](https://github.com/adobe/experience-platform-streaming-connect/releases) e scarica l&#39;ultima versione ufficiale del connettore Adobe Experience Platform Sink.

![Kafka](./images/kc1.png)

Posiziona il file di download **streaming-connect-sink-0.0.14-java-11.jar** sul desktop.

![Kafka](./images/kc2.png)

## 2.6.4.2 Configurare Kafka Connect

Vai alla cartella sul desktop denominata **Kafka_AEP** e passa alla cartella `kafka_2.13-3.1.0/config`.
In tale cartella, aprire il file **connect-distribution.properties** utilizzando qualsiasi editor di testo.

![Kafka](./images/kc3a.png)

Nell&#39;editor di testo passare alle righe 34 e 35 e assicurarsi di impostare i campi `key.converter.schemas.enable` e `value.converter.schemas.enable` su `false`

```json
key.converter.schemas.enable=false
value.converter.schemas.enable=false
```

Salva le modifiche apportate al file.

![Kafka](./images/kc3.png)

Tornare alla cartella `kafka_2.13-3.1.0`, creare manualmente una nuova cartella e denominarla `connectors`.

![Kafka](./images/kc4.png)

Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Nuovo terminale nella cartella**.

![Kafka](./images/kc5.png)

Poi vedrai questo. Immettere il comando `pwd` per recuperare il percorso completo della cartella. Seleziona il percorso completo e copialo negli Appunti.

![Kafka](./images/kc6.png)

Torna all&#39;Editor di testo, al file **connect-distribution.properties** e scorri verso il basso fino all&#39;ultima riga (riga 86 nella schermata). Rimuovere il commento dalla riga che inizia con `# plugin.path=` e incollare il percorso completo della cartella denominata `connectors`. Il risultato dovrebbe essere simile al seguente:

`plugin.path=/Users/woutervangeluwe/Desktop/Kafka_AEP/kafka_2.13-3.1.0/connectors`

Salva le modifiche nel file **connect-distribution.properties** e chiudi l&#39;editor di testo.

![Kafka](./images/kc7.png)

Copiare quindi l&#39;ultima versione ufficiale del connettore Adobe Experience Platform Sink scaricato nella cartella denominata `connectors`. Il file scaricato in precedenza è denominato **streaming-connect-sink-0.0.14-java-11.jar**. È sufficiente spostarlo nella cartella `connectors`.

![Kafka](./images/kc8.png)

Aprire quindi una nuova finestra di Terminal a livello della cartella **kafka_2.13-3.1.0**. Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Nuovo terminale nella cartella**.

Nella finestra Terminal, incolla questo comando: `bin/connect-distributed.sh config/connect-distributed.properties` e fai clic su **Invio**. Questo comando avvia Kafka Connect e carica la libreria del connettore Adobe Experience Platform Sink.

![Kafka](./images/kc9.png)

Dopo un paio di secondi, vedrai qualcosa del genere:

![Kafka](./images/kc10.png)

## 2.6.4.3 Creare il connettore Adobe Experience Platform Sink con Postman

Ora puoi interagire con Kafka Connect utilizzando Postman. Per eseguire questa operazione, scaricare [questa raccolta Postman](./../../../assets/postman/postman_kafka.zip) e decomprimerla nel computer locale sul desktop. Verrà quindi creato un file denominato `Kafka_AEP.postman_collection.json`.

![Kafka](./images/kc11a.png)

Devi importare questo file in Postman. Per farlo, apri Postman, fai clic su **Importa**, trascina il file `Kafka_AEP.postman_collection.json` nel popup e fai clic su **Importa**.

![Kafka](./images/kc11b.png)

Troverai questa raccolta nel menu a sinistra di Postman. Fai clic sulla prima richiesta, **GET connettori Kafka Connect disponibili** per aprirla.

![Kafka](./images/kc11c.png)

Poi vedrai questo. Fai clic sul pulsante blu **Invia**, dopo il quale dovresti visualizzare una risposta vuota `[]`. La risposta vuota è dovuta al fatto che non sono attualmente definiti connettori Kafka Connect.

![Kafka](./images/kc11.png)

Per creare un connettore, fare clic per aprire la seconda richiesta nella raccolta Kafka, **POST Crea connettore sink AEP**. Poi vedrai questo. Alla riga 11, dove è indicato **&quot;aep.endpoint&quot;: &quot;**, è necessario incollare l&#39;URL dell&#39;endpoint di streaming API HTTP ricevuto alla fine dell&#39;esercizio [15.3](./ex3.md). L&#39;URL dell&#39;endpoint di streaming API HTTP è simile al seguente: `https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`.

![Kafka](./images/kc12a.png)

Dopo averlo incollato, il corpo della richiesta dovrebbe essere simile al seguente. Fai clic sul pulsante blu **Invia** per creare il connettore. Otterrai una risposta immediata della creazione del connettore.

![Kafka](./images/kc12.png)

Fai clic sulla prima richiesta, **GET connettori Kafka Connect disponibili** per aprirla nuovamente e fai di nuovo clic sul pulsante blu **Invia**. ora vedrai che è stato creato un connettore Kafka Connect.

![Kafka](./images/kc13.png)

Quindi, apri la terza richiesta nella raccolta Kafka, **GET lo stato del connettore Kafka Connect**. Fai clic sul pulsante blu **Invia** per ricevere una risposta simile a quella riportata di seguito, che indica che il connettore è in esecuzione.

![Kafka](./images/kc14.png)

## 2.6.4.4 Produrre un evento esperienza

Apri una nuova finestra di **Terminal** facendo clic con il pulsante destro del mouse sulla cartella **kafka_2.13-3.1.0** e scegliendo **Nuovo terminale nella cartella**.

![Kafka](./images/kafka11.png)

Immetti il comando seguente:

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aep`

![Kafka](./images/kc15.png)

Poi vedrai questo. A ogni nuova riga seguita dalla pressione del pulsante Invio, verrà inviato un nuovo messaggio nell&#39;argomento **aep**.

![Kafka](./images/kc16.png)

Ora puoi inviare un messaggio che verrà utilizzato dal connettore Adobe Experience Platform Sink e che verrà acquisito in Adobe Experience Platform in tempo reale.

Facciamo una piccola dimostrazione per testarlo.

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](./../../gettingstarted/gettingstarted/images/web8.png)

Nella pagina **Screens** fare clic su **Esegui**.

![DSN](./../../gettingstarted/gettingstarted/images/web2.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](./../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](./../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni dimostrazione, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](./../../gettingstarted/gettingstarted/images/web7.png)

Fai clic sull’icona del logo di Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](./../../../modules/datacollection/module1.2/images/pv1.png)

Dai un&#39;occhiata al pannello Visualizzatore profili e al Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore primario per questo cliente attualmente sconosciuto.

![Demo](./../../../modules/datacollection/module1.2/images/pv2.png)

Vai alla pagina di registrazione/accesso. Fare clic su **CREA UN ACCOUNT**.

![Demo](./../../../modules/datacollection/module1.2/images/pv9.png)

Compila i tuoi dettagli e fai clic su **Registra** dopo di che sarai reindirizzato alla pagina precedente.

![Demo](./../../../modules/datacollection/module1.2/images/pv10.png)

Apri il pannello Visualizzatore profilo e passa a Profilo cliente in tempo reale. Nel pannello Visualizzatore profili dovresti visualizzare tutti i dati personali, come gli identificatori e-mail e telefonici appena aggiunti.

![Demo](./../../../modules/datacollection/module1.2/images/pv11.png)

Potresti visualizzare alcuni eventi di esperienza in base all’attività passata.

![Kafka](./images/kc19.png)

Cambiiamo questa impostazione e inviamo un evento di esperienza Callcenter da Kafka a Adobe Experience Platform.

Prendi il payload dell’evento di esperienza di esempio riportato di seguito e copialo in un editor di testo.

```json
{
  "header": {
    "datasetId": "61fe23fd242870194a6d779c",
    "imsOrgId": "--aepImsOrgID--",
    "source": {
      "name": "Launch"
    },
    "schemaRef": {
      "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
      "contentType": "application/vnd.adobe.xed-full+json;version=1"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    },
    "xdmEntity": {
      "eventType": "callCenterInteractionKafka",
      "_id": "",
      "timestamp": "2022-02-23T09:54:12.232Z",
      "_experienceplatform": {
        "identification": {
          "core": {
            "phoneNumber": ""
          }
        },
        "interactionDetails": {
          "core": {
            "callCenterAgent": {
              "callID": "Support Contact - 3767767",
              "callTopic": "contract",
              "callFeeling": "negative"
            }
          }
        }
      }
    }
  }
}
```

Poi vedrai questo. È necessario aggiornare manualmente 2 campi:

- **_id**: impostalo su un ID casuale, ad esempio `--demoProfileLdap--1234`
- **timestamp**: aggiorna la marca temporale alla data e all&#39;ora correnti
- **phoneNumber**: immettere phoneNumber dell&#39;account appena creato nel sito Web demo. Puoi trovarlo nel pannello Visualizzatore profili in **Identità**.

Devi anche controllare e forse aggiornare questi campi:
- **datasetId**: è necessario copiare l&#39;ID del set di dati per il sistema demo del set di dati - Set di dati evento per il call center (Global v1.1)
- **imsOrgID**: ID organizzazione IMS: `--aepImsOrgId--`

>[!NOTE]
>
>Il campo **_id** deve essere univoco per ogni acquisizione di dati. Se crei più eventi, assicurati di aggiornare ogni volta il campo **_id** a un nuovo valore univoco.

![Kafka](./images/kc20.png)

Dovresti quindi avere qualcosa del genere:

![Kafka](./images/kc21.png)

Quindi, copia l’evento di esperienza completo negli Appunti. È necessario eliminare lo spazio vuoto del payload JSON e a tale scopo verrà utilizzato uno strumento online. Vai a [http://jsonviewer.stack.hu/](http://jsonviewer.stack.hu/) per farlo.

![Kafka](./images/kc22.png)

Incolla l&#39;evento esperienza nell&#39;editor e fai clic su **Rimuovi spazio vuoto**.

![Kafka](./images/kc22a.png)

Quindi, selezionare tutto il testo di output e copiarlo negli Appunti.

![Kafka](./images/kc23.png)

Torna alla finestra Terminal.

![Kafka](./images/kc16.png)

Incolla il nuovo payload senza spazi nella finestra di Terminal e fai clic su **Invio**.

![Kafka](./images/kc23a.png)

Quindi, torna al tuo sito web demo e aggiorna la pagina. Dovresti ora visualizzare un evento esperienza sul tuo profilo, in **Altri eventi**, proprio come quello seguente:

![Kafka](./images/kc24.png)

>[!NOTE]
>
>Se desideri che le interazioni del call center vengano visualizzate nel pannello Visualizzatore profili, devi aggiungere l&#39;etichetta seguente e filtrare nel progetto in [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects), dalla scheda **Visualizzatore profili**.

![Kafka](./images/kc25.png)

Hai finito questo esercizio.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2.6](./aep-apache-kafka.md)

[Torna a tutti i moduli](../../../overview.md)
