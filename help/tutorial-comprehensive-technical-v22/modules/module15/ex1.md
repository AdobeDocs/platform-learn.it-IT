---
title: Introduzione a Apache Kafka
description: Introduzione a Apache Kafka
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 7b600c79-03c5-46fc-9ac9-a15599608c35
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 15.1 Introduzione ad Apache Kafka

## 15.1.1 Introduzione

Ogni organizzazione inizia in un modo molto semplice dal punto di vista dei dati. L&#39;ecosistema dati di un&#39;organizzazione inizia con un sistema di origine e un target. Il sistema di origine invia i dati al sistema di destinazione, ed è tutto. Facile, vero?
Se solo rimarrebbe così semplice. Le organizzazioni superano rapidamente quella semplice configurazione e il numero di sistemi di origine e di destinazione aumenta rapidamente. Tutte queste diverse fonti e destinazioni devono scambiarsi i dati l&#39;una con l&#39;altra, e le cose diventano rapidamente molto complesse.
Ad esempio, se un’organizzazione dispone di 4 sorgenti e 6 destinazioni e tutte queste applicazioni devono comunicare tra loro, dovrai creare 24 integrazioni... Ognuna di queste integrazioni presenta le proprie difficoltà:

- protocollo: come vengono trasportati i dati (TCP, HTTP, REST, FTP, ...)
- formato dati: come vengono analizzati i dati (binario, CSV, JSON, Parquet, ...)
- schema ed evoluzione dei dati: qual è il modello dati e come si evolverà?

Inoltre, ogni volta che si collega un sistema di origine a un sistema di destinazione, si verifica un carico maggiore su tali sistemi da tale connessione.

Quindi, come si risolve questo? Ecco dove Apache Kafka entra nella foto. Apache Kafka consente a un&#39;organizzazione di separare flussi di dati e sistemi fornendo un sistema di messaggistica comune, ad alta velocità e distribuito. I sistemi di origine invieranno i loro dati ad Apache Kafka, e i sistemi di destinazione consumeranno i dati da Apache Kafka.

Pensa a tutti i tipi di origini dati che le aziende devono gestire:

- eventi del sito web
- eventi app mobili
- Eventi POS
- Dati CRM
- dati del call center
- cronologia delle transazioni
- ...

E pensate a tutti i tipi di destinazioni che le aziende usano nel loro ecosistema, che tutti potrebbero aver bisogno di dati da questi sistemi di origine:

- CRM
- lago dati
- sistema di posta elettronica
- audit
- analytics
- ...

Apache Kafka è stata creata da LinkedIn ed è ora un progetto open source gestito principalmente da Confluent.
Apache Kafka fornisce un&#39;architettura distribuita e resiliente che è tollerante agli errori. Può scalare orizzontalmente a 100 di broker e può scalare a milioni di messaggi al secondo. Offre prestazioni elevate con latenze inferiori a 10 ms, ideale per casi d&#39;uso in tempo reale.

Un paio di esempi di casi d’uso:

- Sistema di messaggistica
- Tracciamento delle attività
- Raccogliere metriche da diverse posizioni
- Raccolta di registri applicazioni
- Elaborazione in streaming (con API Kafka Streams o Spark)
- Disaccoppiamento delle dipendenze del sistema
- Integrazione con Spark, Flink, Storm, Hadoop e molte altre tecnologie Big Data.

Per esempio:

- Netflix utilizza Kafka per applicare consigli in tempo reale mentre stai guardando i programmi TV
- Uber utilizza Kafka per raccogliere i dati di utenti, taxi e viaggi in tempo reale per calcolare e prevedere la domanda e calcolare il prezzo di impennata in tempo reale
- linkedIn utilizza Kafka per prevenire lo spam, raccogliere le interazioni degli utenti per migliorare le raccomandazioni di connessione in tempo reale

Per tutti questi casi d&#39;uso, Kafka è utilizzato solo come meccanismo di trasporto. Kafka è davvero brava a spostare i dati tra le applicazioni.

## 15.1.2 Terminologia Kafka

### Messaggio

Un messaggio è una comunicazione inviata da un sistema a Kafka. Un messaggio contiene un payload e un payload contiene elementi di dati. Ad esempio, un evento di esperienza inviato da un sito web a Adobe Experience Platform è considerato un messaggio.

### Argomento, partizioni, offset

Un argomento è un particolare flusso di dati, simile a una tabella di un database. Puoi avere tutti gli argomenti desiderati e un argomento viene identificato dal suo nome. Gli argomenti sono suddivisi in partizioni. Ogni partizione viene ordinata e ogni messaggio all&#39;interno di una partizione ottiene un id incrementale, che viene chiamato **offset**. I messaggi vengono memorizzati in un argomento, in una partizione e viene fatto riferimento tramite un offset. I messaggi vengono conservati solo per un periodo di tempo limitato (l’impostazione predefinita è 1 settimana). Una volta scritto un messaggio in una partizione, non può più essere modificato.

### Broker

Un broker è simile a un server. Un cluster Kafka è composto da più broker (server). Ogni broker è identificato con un ID e contiene alcune partizioni di argomenti.

### Replica

Kafka è un sistema distribuito. Una delle cose importanti di un sistema distribuito è che i dati sono memorizzati in modo sicuro e, come tale, la replica è necessaria. Dopotutto, quando un broker (server) si abbassa, un altro broker (server) dovrebbe comunque essere in grado di fornire l&#39;accesso ai messaggi inizialmente memorizzati sul broker che è andato giù. La replica creerà copie dei messaggi tra più broker per garantire che non venga perso alcun dato.

### Produttori

Come vengono inviati i dati a Kafka? Questo è il ruolo di un produttore. Un produttore si connette a un sistema di origine e prende i dati dal sistema di origine, quindi scrive tali dati su argomenti su partizioni. In base alla configurazione del tuo cluster Kafka, i produttori sapranno automaticamente a quale broker e partizione scrivere. In un sistema distribuito con più broker e strategia di replica, un produttore memorizzerà i dati in modo casuale tra più broker, il che significa che eseguirà automaticamente il bilanciamento del carico.

### Chiavi messaggi

I produttori possono scegliere di inviare una chiave con il messaggio. Una chiave può essere qualsiasi stringa, numero, ecc. Se non viene fornita alcuna chiave, un messaggio verrà inviato in modo casuale ai broker. Se viene inviata una chiave, tutti i messaggi relativi a tale chiave verranno sempre inviati alla stessa partizione. Una chiave di messaggio in quanto tale viene utilizzata per ordinare i messaggi in base a un campo specifico.

### Consumatori

I consumatori leggono i dati da un argomento di Apache Kafka e li condividono con i sistemi di destinazione. I consumatori sanno da quale broker leggere. I dati vengono letti da un consumatore in ordine, all&#39;interno di ogni partizione. I consumatori leggono i dati in gruppi di consumatori.

### Zoodiano

ZooKeeper è essenzialmente un servizio per i sistemi distribuiti che offrono un archivio chiave-valore gerarchico, che viene utilizzato per fornire un servizio di configurazione distribuito, un servizio di sincronizzazione e un registro di denominazione per i sistemi distribuiti di grandi dimensioni. Zookeeper deve essere in esecuzione prima di poter utilizzare Apache Kafka, e Zookeeper è una specie di padrone di cerimonia per Kafka, gestire i servizi distribuiti nel backend mentre Kafka produce e consuma eventi.

Ha finito questo esercizio.

Passaggio successivo: [15.2 Installare e configurare il cluster Kafka](./ex2.md)

[Torna al modulo 15](./aep-apache-kafka.md)

[Torna a tutti i moduli](../../overview.md)
