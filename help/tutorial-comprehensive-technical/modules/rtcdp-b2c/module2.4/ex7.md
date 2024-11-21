---
title: Audience Activation a Microsoft Azure Event Hub - Azione
description: Audience Activation a Microsoft Azure Event Hub - Azione
kt: 5342
doc-type: tutorial
exl-id: f5b224bf-60b9-46e0-abdb-9d96a7e8c59f
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 2.4.7 Scenario completo

## Avvia trigger dell’hub eventi di Azure

Per mostrare il payload inviato da Adobe Experience Platform Real-time CDP al nostro Azure Event Hub dopo la qualifica del pubblico, è necessario avviare la semplice funzione di attivazione dell’Azure Event Hub. Questa funzione semplifica il dump del payload nella console in Visual Studio Code. Ma ricorda che questa funzione può essere estesa in qualsiasi modo per interfacciarsi con tutti i tipi di ambienti utilizzando API e protocolli dedicati.

### Avviare Visual Studio Code e avviare il progetto

Assicurarsi che il progetto Visual Studio Code sia aperto e in esecuzione

Per avviare, arrestare e riavviare la funzione di Azure in Visual Studio Code, fare riferimento all&#39;esercizio precedente.

Il **Terminal** del codice Visual Studio deve menzionare un elemento simile al seguente:

```code
[2024-11-20T20:07:12.316Z] Debugger listening on ws://127.0.0.1:9229/86c8e251-8e2f-4c65-a063-cda77edbf2ca
[2024-11-20T20:07:12.318Z] For help, see: https://nodejs.org/en/docs/inspector
[2024-11-20T20:07:12.343Z] Worker process started and initialized.
[2024-11-20T20:07:12.359Z] Debugger attached.

Functions:

        vangeluw-aep-event-hub-trigger: eventHubTrigger

For detailed output, run func with --verbose flag.
[2024-11-20T20:07:18.150Z] Host lock lease acquired by instance ID '000000000000000000000000000C19D8'.
```

## Carica il sito Web di Citi Signal

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

## Qualificati per il pubblico

Passare alla pagina **Piani**. Questa azione ti qualificherà per il pubblico `--aepUserLdap-- - Interest in Plans`.

![6-04-luma-telco-nav-sports.png](./images/cs1.png)

Per verificare il funzionamento, apri il pannello Visualizzatore profili. Ora dovresti essere membro di `--aepUserLdap-- - Interest in Plans`. Se le appartenenze al pubblico non sono ancora state aggiornate nel pannello Visualizzatore profili, fai clic sul pulsante Ricarica.

![6-05-luma-telco-nav-broadband.png](./images/cs2.png)

Torna a Visual Studio Code e controlla la scheda **TERMINAL**. Dovresti visualizzare un elenco di tipi di pubblico per il tuo **ECID** specifico. Questo payload di attivazione viene recapitato all&#39;hub eventi non appena si è qualificati per il pubblico `--aepUserLdap-- - Interest in Plans`.

![6-06-vsc-activation-realized.png](./images/cs3.png)

Se osservi attentamente il payload del pubblico, noterai che `--aepUserLdap-- - Interest in Plans` si trova nello stato **realized**.

```json
{
  "identityMap": {
    "ecid": [
      {
        "id": "36281682065771928820739672071812090802"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "94db5aed-b90e-478d-9637-9b0fad5bba11": {
        "createdAt": 1732129904025,
        "lastQualificationTime": "2024-11-21T07:33:52Z",
        "mappingCreatedAt": 1732130611000,
        "mappingUpdatedAt": 1732130611000,
        "name": "vangeluw - Interest in Plans",
        "status": "realized",
        "updatedAt": 1732129904025
      }
    }
  }
}
```

Uno stato di pubblico di **realized** indica che il tuo profilo fa parte del pubblico, mentre lo stato di **exited** indica che il nostro profilo è stato rimosso dal pubblico.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
