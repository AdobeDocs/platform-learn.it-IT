---
title: Attivazione segmento in Microsoft Azure Event Hub - Azione
description: Attivazione segmento in Microsoft Azure Event Hub - Azione
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.4.6 Scenario end-to-end

## 2.4.6.1 Avvio del trigger dell’hub eventi di Azure

Per mostrare il payload inviato da Adobe Experience Platform Real-time CDP al nostro Azure Event Hub al momento della qualificazione del segmento, è necessario avviare la semplice funzione di attivazione dell’Azure Event Hub. Questa funzione semplifica il dump del payload nella console in Visual Studio Code. Ma ricorda che questa funzione può essere estesa in qualsiasi modo per interfacciarsi con tutti i tipi di ambienti utilizzando API e protocolli dedicati.

### Avviare Visual Studio Code e avviare il progetto

Assicurarsi che il progetto Visual Studio Code sia aperto e in esecuzione

Per avviare, arrestare e riavviare la funzione di Azure in Visual Studio Code, fare riferimento agli esercizi seguenti:

- [Esercizio 13.5.4: Avviare il progetto Azure](./ex5.md)
- [Esercizio 13.5.5 - Arrestare il progetto Azure](./ex5.md)

Il **Terminal** del codice Visual Studio deve menzionare un elemento simile al seguente:

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 2.4.6.2 Caricare il sito web Luma

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Ora puoi seguire il flusso seguente per accedere al sito web. Fai clic su **Integrazioni**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

Nella pagina **Integrazioni** è necessario selezionare la proprietà Raccolta dati creata nell&#39;esercizio 0.1.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni dimostrazione, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

## 2.4.6.3 Partecipazione al segmento Apparecchiature

Passare alla pagina **Apparecchiature** una volta e **non ricaricarla o aggiornarla**. Questa azione ti qualificherà per il tuo segmento `--aepUserLdap-- - Interest in Equipment`.

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

Per verificare il funzionamento, apri il pannello Visualizzatore profili. Ora dovresti essere membro di `--aepUserLdap-- - Interest in Equipment`. Se le appartenenze al segmento non sono ancora state aggiornate nel pannello Visualizzatore profili, fai clic sul pulsante Ricarica.

![6-05-luma-telco-nav-broadband.png](./images/luma2.png)

Torna a Visual Studio Code e controlla la scheda **TERMINAL**. Dovresti visualizzare un elenco di segmenti per il tuo **ECID** specifico. Questo payload di attivazione viene recapitato all&#39;hub eventi non appena si è qualificati per il segmento `--aepUserLdap-- - Interest in Equipment`.

Se osservi attentamente il payload del segmento, noterai che `--aepUserLdap-- - Interest in Equipment` si trova nello stato **realized**.

Uno stato di segmento **realized** indica che il nostro profilo è appena entrato nel segmento. Mentre lo stato **existing** indica che il nostro profilo continua a essere nel segmento.

![6-06-vsc-activation-realized.png](./images/luma3.png)

## 2.4.6.4 Visitare la pagina Apparecchiature per la seconda volta

Eseguire un aggiornamento rapido della pagina **Apparecchiature**.

![6-07-back-to-sports.png](./images/luma1.png)

Tornare a Visual Studio Code e verificare la scheda **TERMINAL**. Vedrai che il tuo segmento è ancora presente, ma ora si trova nello stato **existing**, il che significa che il nostro profilo continua a trovarsi nel segmento.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 2.4.6.5 Visita la pagina Sport per la terza volta

Se visiti nuovamente la pagina **Sport** per la terza volta, non verrà eseguita alcuna attivazione, perché non vi è alcuna modifica dello stato dal punto di vista di un segmento.

Le attivazioni dei segmenti si verificano solo quando cambia lo stato del segmento:

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
