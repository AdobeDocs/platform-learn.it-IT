---
title: Attivazione del segmento nell’hub eventi di Microsoft Azure - Azione
description: Attivazione del segmento nell’hub eventi di Microsoft Azure - Azione
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 989dd2e4-597b-4b80-8b17-41aa6929ed64
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 13.6 Scenario end-to-end

## 13.6.1 Avvia l&#39;attivazione di Azure Event Hub

Per mostrare il payload inviato da Adobe Experience Platform Real-time CDP al nostro Azure Event Hub al momento della qualifica del segmento, dobbiamo avviare la nostra semplice funzione di attivazione di Azure Event Hub. Questa funzione consente di &quot;scaricare&quot; semplicemente il payload nella console in Visual Studio Code. Ma ricorda che questa funzione può essere estesa in qualsiasi modo all&#39;interfaccia con tutti i tipi di ambienti utilizzando API e protocolli dedicati.

### Avviare il codice di Visual Studio e avviare il progetto

Assicurati che il progetto Codice di Visual Studio sia aperto ed in esecuzione

Per avviare/interrompere/riavviare la funzione di Azure in Visual Studio Code, fare riferimento ai seguenti esercizi:

- [Esercizio 13.5.4 - Avvia progetto Azure](./ex5.md)
- [Esercizio 13.5.5 - Arresta progetto Azure](./ex5.md)

Codice di Visual Studio **Terminale** qualcosa di simile:

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 13.6.2 Carica il tuo sito web Luma

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

## 13.6.3 Qualifica per il tuo interesse nel segmento Apparecchiature

Passa a **Attrezzatura** una volta, e **non ricaricarlo o aggiornarlo**. Questa azione deve qualificarti per `--demoProfileLdap-- - Interest in Equipment` segmento.

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

Per verificare il funzionamento, apri il pannello Visualizzatore profilo . Ora devi essere un membro del `--demoProfileLdap-- - Interest in Equipment`. Se le iscrizioni ai segmenti non sono ancora state aggiornate nel pannello Visualizzatore profilo, fai clic sul pulsante ricarica.

![6-05-luma-telco-nav-banda larga.png](./images/luma2.png)

Torna al codice di Visual Studio e osserva le **TERMINALE** dovresti visualizzare un elenco dei segmenti per il tuo **ECID**. Questo payload di attivazione viene consegnato al tuo hub eventi non appena ti qualifichi per `--demoProfileLdap-- - Interest in Equipment` segmento.

Osservando più da vicino il payload del segmento, puoi notare che `--demoProfileLdap-- - Interest in Equipment` è nello stato **realizzato**.

Lo stato di un segmento **realizzato** significa che il nostro profilo è appena entrato nel segmento. Mentre il **esistente** lo stato indica che il nostro profilo continua a trovarsi nel segmento.

![6-06-vsc-activation-Reated.png](./images/luma3.png)

## 13.6.4 Visita la pagina Attrezzature per una seconda volta

Eseguire un aggiornamento rapido del **Attrezzatura** pagina.

![6-07-back-to-sports.png](./images/luma1.png)

Ora, torna a Visual Studio Code e verifica il **TERMINALE** scheda . Noterai che il tuo segmento è ancora nello stato **esistente** il che significa che il nostro profilo continua a trovarsi nel segmento.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 13.6.5 Visita la pagina Sport per una terza volta

Se desideri rivisitare il **Sport** per una terza volta, non verrà effettuata alcuna attivazione, in quanto non vi è alcuna modifica dello stato da un punto di vista del segmento.

Le attivazioni dei segmenti si verificano solo quando lo stato del segmento cambia:

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../overview.md)
