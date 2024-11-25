---
title: Installare e configurare il cluster Kafka
description: Installare e configurare il cluster Kafka
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: adffeead-9bcb-4632-9a2c-c6da1c40b7f2
source-git-commit: be5a7dec47a83a14d74024015a15a9c24d04cd95
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# 2.6.2 Installare e configurare il cluster Kafka

## Scarica Apache Kafka

Vai a [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads) e scarica l&#39;ultima versione rilasciata. Selezionare la versione binaria più recente, in questo caso **3.9.0**. Verrà avviato il download.

![Kafka](./images/kafka1.png)

Crea sul desktop una cartella denominata **Kafka_AEP** e inserisci il file scaricato in tale directory.

![Kafka](./images/kafka3.png)

Apri una finestra di **Terminal** facendo clic con il pulsante destro del mouse sulla cartella e scegliendo **New Terminal at Folder**.

![Kafka](./images/kafka4.png)

Esegui questo comando nella finestra di Terminal per decomprimere il file scaricato:

`tar -xvf kafka_2.13-3.9.0.tgz`

>[!NOTE]
>
>Verifica che il comando di cui sopra corrisponda alla versione del file scaricato. Se la tua versione è più recente, dovrai aggiornare il comando precedente per farla corrispondere a quella versione.

![Kafka](./images/kafka5.png)

A questo punto viene visualizzato quanto segue:

![Kafka](./images/kafka6.png)

Dopo aver decompresso il file, ora disponi di una directory come questa:

![Kafka](./images/kafka7.png)

E in quella directory, vedrai queste sottodirectory:

![Kafka](./images/kafka8.png)

Torna alla finestra Terminal. Immetti il comando seguente:

`cd kafka_2.13-3.9.0`

>[!NOTE]
>
>Verifica che il comando di cui sopra corrisponda alla versione del file scaricato. Se la tua versione è più recente, dovrai aggiornare il comando precedente per farla corrispondere a quella versione.

![Kafka](./images/kafka9.png)

Immettere quindi il comando `bin/kafka-topics.sh`.

![Kafka](./images/kafka10a.png)

Dovresti quindi visualizzare questa risposta. Ciò significa che Kafka è installato correttamente e che Java funziona correttamente. (Promemoria: è necessario che Java 23 JDK sia installato affinché funzioni correttamente!). È possibile visualizzare la versione Java installata utilizzando il comando `java -version`.)

![Kafka](./images/kafka10.png)

## Avvia Kafka

Per avviare Kafka, è necessario avviare Kafka Zookeeper e Kafka, in questo ordine.

Apri una finestra di **Terminal** facendo clic con il pulsante destro del mouse sulla cartella **kafka_2.13-3.9.0** e scegliendo **Nuovo terminale nella cartella**.

![Kafka](./images/kafka11.png)

Immetti questo comando:

`bin/zookeeper-server-start.sh config/zookeeper.properties`

![Kafka](./images/kafka12.png)

A questo punto viene visualizzato quanto segue:

![Kafka](./images/kafka13.png)

Tieni aperta questa finestra mentre segui questi esercizi!

Aprire un&#39;altra nuova finestra di **Terminal** facendo clic con il pulsante destro del mouse sulla cartella **kafka_2.13-3.9.0** e scegliendo **Nuovo terminale nella cartella**.

![Kafka](./images/kafka11.png)

Immetti questo comando:

`bin/kafka-server-start.sh config/server.properties`

![Kafka](./images/kafka14.png)

A questo punto viene visualizzato quanto segue:

![Kafka](./images/kafka15.png)

Tieni aperta questa finestra mentre segui questi esercizi!

## Creare un argomento Kafka

Apri una finestra di **Terminal** facendo clic con il pulsante destro del mouse sulla cartella **kafka_2.13-3.9.0** e scegliendo **Nuovo terminale nella cartella**.

![Kafka](./images/kafka11.png)

Immetti questo comando per creare un nuovo argomento Kafka denominato **aeptest**. Questo argomento verrà utilizzato per il test in questo esercizio.

`bin/kafka-topics.sh --create --topic aeptest --bootstrap-server localhost:9092`

Viene quindi visualizzata una conferma:

![Kafka](./images/kafka17a.png)

Immettere questo comando per creare un nuovo argomento Kafka denominato **aep**. Questo argomento verrà utilizzato dal connettore sink di Adobe Experience Platform che verrà configurato negli esercizi successivi.

`bin/kafka-topics.sh --create --topic aep --bootstrap-server localhost:9092`

Viene quindi visualizzata una conferma simile:

![Kafka](./images/kafka17.png)

## Produrre eventi

Torna alla finestra Terminale in cui hai creato il tuo primo argomento Kafka e immetti il seguente comando:

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aeptest`

![Kafka](./images/kafka18.png)

Poi vedrai questo. A ogni nuova riga seguita dalla pressione del pulsante Invio, verrà inviato un nuovo messaggio nell&#39;argomento **aeptest**.

![Kafka](./images/kafka19.png)

Immetti `Hello AEP` e premi Invio. Il primo evento è stato inviato all&#39;istanza Kafka locale, nell&#39;argomento **aeptest**.

![Kafka](./images/kafka20.png)

Immetti `Hello AEP again.` e premi Invio.

Immetti `AEP Data Collection is the best.` e premi Invio.

Hai prodotto 3 eventi nell&#39;argomento **aeptest**. Questi eventi possono ora essere utilizzati da un’applicazione che potrebbe aver bisogno di tali dati.

![Kafka](./images/kafka21.png)

Sulla tastiera, fare clic contemporaneamente su `Control` e `C` per chiudere il producer.

![Kafka](./images/kafka22.png)

## Eventi di consumo

Nella stessa finestra di Terminal utilizzata per produrre gli eventi, immettere il comando seguente:

`bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic aeptest --from-beginning`

Verranno quindi visualizzati nel consumatore tutti i messaggi generati nell&#39;esercizio precedente per l&#39;argomento **aeptest**. Apache Kafka funziona in questo modo: un produttore crea gli eventi in una pipeline e un consumatore li consuma.

![Kafka](./images/kafka23.png)

Sulla tastiera, fare clic contemporaneamente su `Control` e `C` per chiudere il producer.

![Kafka](./images/kafka24.png)

In questo esercizio, hai esaminato tutte le nozioni di base per configurare un cluster Kafka locale, creare un argomento Kafka, produrre eventi e utilizzare eventi.

L’obiettivo di questo modulo è simulare ciò che accade se un’organizzazione reale ha già implementato un cluster Apache Kafka e desidera inviare in streaming i dati dal proprio cluster Kafka a Adobe Experience Platform.

Per facilitare tale implementazione, è stato creato un connettore Adobe Experience Platform Sink che può essere implementato utilizzando Kafka Connect. La documentazione del connettore Adobe Experience Platform Sink è disponibile qui: [https://github.com/adobe/experience-platform-streaming-connect](https://github.com/adobe/experience-platform-streaming-connect).

Negli esercizi successivi, implementerai tutto il necessario per utilizzare il connettore Adobe Experience Platform Sink dal tuo cluster Kafka locale.

Chiudere la finestra del terminale.

Hai finito questo esercizio.

Passaggio successivo: [2.6.3 Configurare l&#39;endpoint API HTTP in Adobe Experience Platform](./ex3.md)

[Torna al modulo 2.6](./aep-apache-kafka.md)

[Torna a tutti i moduli](../../../overview.md)
