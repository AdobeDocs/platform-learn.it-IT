---
title: Introduzione ad Apache Kafka
description: Introduzione ad Apache Kafka
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 2.6.1 Introduzione ad Apache Kafka

## 2.6.1.1 Introduzione

Ogni organizzazione inizia in modo molto semplice dal punto di vista dei dati. L’ecosistema di dati di un’organizzazione inizia con un sistema di origine e un target. Il sistema di origine invia i dati al sistema di destinazione, e basta. Facile, vero?
Se solo restasse così semplice. Le aziende crescono rapidamente di più rispetto alla semplice configurazione e il numero di sistemi di origine e di destinazione aumenta rapidamente. Tutte queste diverse origini e destinazioni devono scambiarsi dati, e le cose diventano rapidamente molto complesse.
Ad esempio, se un’organizzazione dispone di 4 origini e 6 destinazioni e tutte queste applicazioni devono parlare tra loro, dovrai creare 24 integrazioni... Ognuna di queste integrazioni presenta le proprie difficoltà:

- protocollo: come vengono trasportati i dati (TCP, HTTP, REST, FTP, ...)
- formato dati: come vengono analizzati i dati (binario, CSV, JSON, Parquet, ...)
- schema dati ed evoluzione: qual è il modello dati e come si evolverà?

Inoltre, ogni volta che si collega un sistema di origine a un sistema di destinazione, si verifica un aumento del carico su tali sistemi da tale connessione.

Quindi, come si risolve questo problema? È qui che entra in scena Apache Kafka. Apache Kafka consente a un’organizzazione di disaccoppiare flussi di dati e sistemi fornendo un sistema di messaggistica distribuito comune e ad alta velocità. I sistemi Source invieranno i loro dati ad Apache Kafka, mentre i sistemi di destinazione utilizzeranno i dati da Apache Kafka.

Pensa a tutti i tipi di origini dati che le aziende devono gestire:

- eventi del sito web
- eventi app mobile
- Eventi POS
- Dati CRM
- dati del centro chiamate
- cronologia delle transazioni
- ...

E pensa a tutti i tipi di destinazioni che le aziende usano nel loro ecosistema e che potrebbero aver bisogno dei dati di quei sistemi di origine:

- CRM
- data lake
- sistema e-mail
- audit
- analytics
- ...

Apache Kafka è stato creato da LinkedIn ed è ora un progetto open source gestito principalmente da Confluent.
Apache Kafka fornisce un’architettura distribuita, resiliente e a tolleranza di errore. Può scalare orizzontalmente fino a 100 secondi di broker e può scalare fino a milioni di messaggi al secondo. Offre prestazioni elevate con latenze inferiori a 10 ms, ideale per casi di utilizzo in tempo reale.

Un paio di esempi di casi d’uso:

- Sistema di messaggistica
- Tracciamento attività
- Raccogliere metriche da diverse posizioni
- Raccolta dei registri dell’applicazione
- Elaborazione del flusso (con API Streams Kafka o Spark)
- Disaccoppiamento delle dipendenze del sistema
- Integrazione con Spark, Flink, Storm, Hadoop e molte altre tecnologie Big Data.

Ad esempio:

- Netflix utilizza Kafka per applicare i consigli in tempo reale mentre stai guardando programmi TV
- Uber utilizza Kafka per raccogliere i dati di utenti, taxi e viaggi in tempo reale per calcolare e prevedere la domanda e calcolare i prezzi delle impennate in tempo reale
- LinkedIn utilizza Kafka per prevenire lo spam e raccogliere le interazioni degli utenti per fornire raccomandazioni di connessione migliori in tempo reale

Per tutti questi casi d’uso, Kafka è utilizzato solo come meccanismo di trasporto. Kafka è veramente bravo a spostare i dati tra le applicazioni.

## 2.6.1.2 Terminologia Kafka

### Messaggio

Un messaggio è una comunicazione inviata da un sistema a Kafka. Un messaggio contiene un payload e un payload contiene elementi di dati. Ad esempio, un evento esperienza inviato da un sito web a Adobe Experience Platform viene considerato un messaggio.

### Argomento, partizioni, offset

Un argomento è un particolare flusso di dati, simile a una tabella in un database. È possibile disporre di tutti gli argomenti desiderati e un argomento è identificato dal relativo nome. Gli argomenti vengono suddivisi in partizioni. Ogni partizione viene ordinata e ogni messaggio all&#39;interno di essa riceve un ID incrementale, denominato **offset**. I messaggi vengono memorizzati in un argomento, in una partizione e vi si fa riferimento utilizzando un offset. I messaggi vengono conservati solo per un periodo di tempo limitato (il valore predefinito è 1 settimana). Una volta scritto in una partizione, il messaggio non può più essere modificato.

### Broker

Un broker è simile a un server. Un cluster Kafka è composto da più broker (server). Ogni broker è identificato da un ID e contiene determinate partizioni di argomenti.

### Replica

Kafka è un sistema distribuito. Una delle caratteristiche più importanti di un sistema distribuito è che i dati vengono archiviati in modo sicuro e, di conseguenza, è necessaria la replica. Dopo tutto, quando un broker (server) si blocca, un altro broker (server) dovrebbe ancora essere in grado di fornire accesso ai messaggi inizialmente memorizzati sul broker che si è interrotto. La replica crea copie dei messaggi tra più broker per garantire che non venga persa alcuna informazione.

### Produttori

Come vengono inviati i dati a Kafka? Questo è il ruolo di un produttore. Un produttore si connette a un sistema di origine e prende i dati dal sistema di origine, quindi li scrive su argomenti nelle partizioni. In base alla configurazione del cluster Kafka, i produttori sapranno automaticamente in quale broker e partizione scrivere. In un sistema distribuito con più broker e una strategia di replica, un produttore archivia i dati in modo casuale tra più broker, il che significa che esegue automaticamente il bilanciamento del carico.

### Tasti messaggio

I produttori possono scegliere di inviare una chiave con il messaggio. Una chiave può essere qualsiasi stringa, numero, ecc. Se non viene fornita alcuna chiave, verrà inviato un messaggio casuale ai broker. Se viene inviata una chiave, tutti i messaggi relativi a tale chiave andranno sempre alla stessa partizione. Una chiave di messaggio viene utilizzata per ordinare i messaggi in base a un campo specifico.

### Consumatori

I consumatori leggono i dati da un argomento di Apache Kafka e li condividono con i sistemi di destinazione. I consumatori sanno da quale broker leggere. I dati vengono letti da un consumatore in ordine, all’interno di ogni partizione. I consumatori leggono i dati in gruppi di consumatori.

### Zookeeper

ZooKeeper è essenzialmente un servizio per sistemi distribuiti che offre un archivio chiave-valore gerarchico, utilizzato per fornire un servizio di configurazione distribuito, un servizio di sincronizzazione e un registro dei nomi per sistemi distribuiti di grandi dimensioni. Zookeeper deve essere in esecuzione prima di poter utilizzare Apache Kafka, e Zookeeper è una sorta di maestro di cerimonia per Kafka, gestendo servizi distribuiti nel backend mentre Kafka produce e consuma eventi.

Hai finito questo esercizio.

Passaggio successivo: [2.6.2 Installa e configura il cluster Kafka](./ex2.md)

[Torna al modulo 2.6](./aep-apache-kafka.md)

[Torna a tutti i moduli](../../../overview.md)
