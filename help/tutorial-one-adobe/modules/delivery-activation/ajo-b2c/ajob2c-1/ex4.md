---
title: Aggiorna l’ID configurazione e verifica il Percorso
description: Aggiorna l’ID configurazione e verifica il Percorso
kt: 5342
doc-type: tutorial
exl-id: da018975-7421-4d70-b04d-ad8b0597f460
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# 3.1.3 Aggiorna la proprietà Data Collection e verifica il percorso

## 3.1.3.1 Aggiornare la proprietà Data Collection

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/launch/) e seleziona **Tag**.

![Pagina delle proprietà](./../../../../modules/delivery-activation/datacollection/dc1.1/images/launch1.png)

In **Guida introduttiva**, Demo System ha creato due proprietà client: una per il sito Web e una per l&#39;app mobile. Trovarli cercando `--aepUserLdap--` nella casella **[!UICONTROL Cerca]**. Fare clic per aprire la proprietà **Web**.

![Casella di ricerca](./../../../../modules/delivery-activation/datacollection/dc1.1/images/property6.png)

Poi vedrai questo.

![Configurazione lancio](./images/rule1.png)

Nel menu a sinistra, vai a **Regole** e cerca la regola **Crea account**. Fai clic sulla regola **Crea account** per aprirla.

![Configurazione lancio](./images/rule2.png)

Vedrai quindi i dettagli di questa regola. Fare clic per aprire l&#39;azione **Invia evento di registrazione all&#39;evento esperienza**.

![Configurazione lancio](./images/rule3.png)

Quando questa azione viene attivata, vedrai che viene utilizzato un elemento dati specifico per definire la struttura dati XDM. È necessario aggiornare l&#39;elemento dati e definire l&#39;**ID evento** dell&#39;evento configurato in [Esercizio 3.1.1](./ex1.md).

![Configurazione lancio](./images/rule4.png)

Ora devi andare ad aggiornare l&#39;elemento dati **XDM - Evento registrazione**. A tale scopo, passare a **Elementi dati**. Cerca **XDM - Registration** e fai clic per aprire l&#39;elemento dati.

![Configurazione lancio](./images/rule5.png)

A questo punto viene visualizzato quanto segue:

![Configurazione lancio](./images/rule6.png)

Passare al campo `_experience.campaign.orchestration.eventID`. Rimuovi il valore corrente e incolla il tuo eventID lì.

Come promemoria, l&#39;ID evento si trova in Adobe Journey Optimizer in **Configurazioni > Eventi** e troverai l&#39;ID evento nel payload di esempio del tuo evento, che si presenta così: `"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`.

![ACOP](./images/payloadeventID.png)

Dopo aver incollato l’ID evento, lo schermo dovrebbe essere simile al seguente. Fare clic su **Salva** o **Salva nella libreria**.

![Configurazione lancio](./images/rule7.png)

Infine, devi pubblicare le modifiche. Vai a **Flusso di pubblicazione** nel menu a sinistra e fai clic per aprire la libreria **Principale**.

![Configurazione lancio](./images/rule8.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi fai clic su **Salva e genera in sviluppo**.

![Configurazione lancio](./images/rule9.png)

La libreria verrà quindi aggiornata e dopo 1-2 minuti puoi procedere e verificare la configurazione.

## 3.1.3.2 Test del Percorso

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni esercizio, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Fai clic sull’icona del logo Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv1.png)

Dai un&#39;occhiata al pannello Visualizzatore profili e al Profilo cliente in tempo reale con **Experience Cloud ID** come identificatore primario per questo cliente attualmente sconosciuto. Fai clic su **Accedi**.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv2.png)

Fare clic su **CREA UN ACCOUNT**.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv9.png)

Compila i tuoi dettagli e fai clic su **Registra** dopo di che sarai reindirizzato alla pagina precedente.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv10.png)

Apri il pannello Visualizzatore profilo e passa a Profilo cliente in tempo reale. Nel pannello Visualizzatore profili dovresti visualizzare tutti i dati personali, come gli identificatori e-mail e telefonici appena aggiunti.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv11.png)

1 minuto dopo aver creato l’account, riceverai l’e-mail di creazione dell’account da Adobe Journey Optimizer.

![Configurazione lancio](./images/email.png)

Vedrai anche l’entrata nel percorso e l’avanzamento nel percorso sulla dashboard del percorso in Journey Optimizer.

![Configurazione lancio](./images/emaildash.png)

## Passaggi successivi

Vai a [Riepilogo e vantaggi](./summary.md){target="_blank"}

Torna a [Adobe Journey Optimizer: orchestrazione](./journey-orchestration-create-account.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
