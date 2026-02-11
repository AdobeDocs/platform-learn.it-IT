---
title: Adobe Journey Optimizer - Origini dati esterne e azioni personalizzate
description: Adobe Journey Optimizer - Origini dati esterne e azioni personalizzate
kt: 5342
doc-type: tutorial
exl-id: 5c8cbec6-58c1-4992-a0c7-1a2b7c34e5b6
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# 3.2.5 Attivare il percorso

In questo esercizio, verificherai e attiverai il percorso configurato in questo modulo.

## 3.2.5.1 Aggiorna la configurazione dell&#39;evento del recinto geografico

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/launch/) e seleziona **Tag**.

Questa è la pagina Proprietà raccolta dati di Adobe Experience Platform che hai visto prima.

![Pagina delle proprietà](./../../../../modules/delivery-activation/datacollection/dc1.1/images/launch1.png)

In **Guida introduttiva**, il sistema di dimostrazione ha creato le proprietà dei tag per te: uno per il sito Web e uno per l&#39;app mobile. Trovarli cercando `--aepUserLdap--` nella casella **[!UICONTROL Cerca]**. Fare clic per aprire la proprietà **Web**.

![Casella di ricerca](./../../../../modules/delivery-activation/datacollection/dc1.1/images/property6.png)

Poi vedrai questo.

![Configurazione lancio](./images/rule1.png)

Nel menu a sinistra, vai a **Regole** e cerca la regola **Evento recinto geografico**. Fai clic sulla regola **Evento recinto geografico** per aprirla.

![Configurazione lancio](./images/rule2.png)

Vedrai quindi i dettagli di questa regola. Fare clic per aprire l&#39;azione **Adobe Experience Platform Web SDK - Invia evento**.

![Configurazione lancio](./images/rule3.png)

Quando questa azione viene attivata, vedrai che viene utilizzato un elemento dati specifico per definire la struttura dati XDM. È necessario aggiornare l&#39;elemento dati e definire l&#39;**ID evento** dell&#39;evento configurato in [Esercizio 3.2.1](./ex1.md).

![Configurazione lancio](./images/rule4.png)

Ora devi andare ad aggiornare l&#39;elemento dati **XDM - Evento recinto geografico**. A tale scopo, passare a **Elementi dati**. Cerca **XDM - Evento recinto geografico** e fai clic per aprire l&#39;elemento dati.

![Configurazione lancio](./images/rule5.png)

A questo punto viene visualizzato quanto segue:

![Configurazione lancio](./images/rule6.png)

Passare al campo `_experience.campaign.orchestration.eventID`. Rimuovi il valore corrente e incolla il tuo eventID lì.

Come promemoria, l&#39;ID evento si trova in Adobe Journey Optimizer in **Configurazioni > Eventi** e troverai l&#39;ID evento nel payload di esempio del tuo evento, che si presenta così: `"eventID": "209a2eecb641e20a517909e186a559ced155384a26429a557eb259e5a470bca7"`.

![ACOP](./images/payloadeventID.png)

Successivamente, devi definire la città in questo elemento dati. Vai a **placeContext > geo > city** e immetti una città scelta. Fare clic su **Salva** o **Salva nella libreria**.

![ACOP](./images/payloadeventIDgeo.png)

Infine, devi pubblicare le modifiche. Vai a **Flusso di pubblicazione** nel menu a sinistra e fai clic su **Uomo** per aprire la libreria.

![Configurazione lancio](./images/rule8.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi fai clic su **Salva e genera in sviluppo**.

![Configurazione lancio](./images/rule9.png)

## 3.2.5.2 Attiva il percorso

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

Apri il pannello Visualizzatore profilo e passa a Profilo cliente in tempo reale. Nel pannello Visualizzatore profili dovresti visualizzare tutti i dati personali, come gli identificatori e-mail e telefonici appena aggiunti.

![Demo](./images/pv2.png)

Nel pannello Visualizzatore profili, fai clic su **UTILITÀ** e seleziona **Chiamata diretta**.

>[!NOTE]
>
>Se nel pannello Visualizzatore profili non è disponibile l&#39;opzione per inviare un evento di chiamata diretta, è possibile inviarne manualmente uno aprendo la visualizzazione per sviluppatori del browser e passando a **Console**, quindi incollando e inviando il comando: `_satellite.track('geofenceevent')`.

![Demo](./images/pv3.png)

Immetti `geofenceevent` e fai clic su **Invia**.

![Demo](./images/pv4.png)

Un paio di secondi dopo, vedrai il messaggio di Adobe Journey Optimizer apparire nel canale Slack.

![Demo](./images/smsdemo4.png)

## Passaggi successivi

Torna a [Adobe Journey Optimizer: origini dati esterne e azioni personalizzate](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
