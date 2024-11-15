---
title: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Attiva il tuo Percorso di clienti orchestrato
description: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Attiva il tuo Percorso di clienti orchestrato
kt: 5342
doc-type: tutorial
exl-id: 068c8be4-2e9e-4d38-9c0e-f769ac927b57
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---

# 3.2.5 Attivare il percorso

In questo esercizio, verificherai e attiverai il percorso configurato in questo modulo.

## 3.2.5.1 Aggiornare la configurazione dell’evento recinto geografico

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/launch/) e seleziona **Tag**.

Questa è la pagina Proprietà raccolta dati di Adobe Experience Platform che hai visto prima.

![Pagina delle proprietà](./../../../modules/datacollection/module1.1/images/launch1.png)

Nel modulo 0, Demo System ha creato due proprietà client per te: una per il sito web e una per l’app mobile. Trovarli cercando `--aepUserLdap--` nella casella **[!UICONTROL Cerca]**. Fare clic per aprire la proprietà **Web**.

![Casella di ricerca](./../../../modules/datacollection/module1.1/images/property6.png)

Poi vedrai questo.

![Configurazione lancio](./images/rule1.png)

Nel menu a sinistra, vai a **Regole** e cerca la regola **Evento recinto geografico**. Fai clic sulla regola **Evento recinto geografico** per aprirla.

![Configurazione lancio](./images/rule2.png)

Vedrai quindi i dettagli di questa regola. Fai clic per aprire l&#39;azione **Invia &quot;evento recinto geografico&quot; ad AEP - attiva JO**.

![Configurazione lancio](./images/rule3.png)

Quando questa azione viene attivata, vedrai che viene utilizzato un elemento dati specifico per definire la struttura dati XDM. È necessario aggiornare l&#39;elemento dati e definire l&#39;**ID evento** dell&#39;evento configurato in [Esercizio 8.1](./ex1.md).

![Configurazione lancio](./images/rule4.png)

Ora devi andare ad aggiornare l&#39;elemento dati **XDM - Evento recinto geografico**. A tale scopo, passare a **Elementi dati**. Cerca **XDM - Evento recinto geografico** e fai clic per aprire l&#39;elemento dati.

![Configurazione lancio](./images/rule5.png)

A questo punto viene visualizzato quanto segue:

![Configurazione lancio](./images/rule6.png)

Passare al campo `_experience.campaign.orchestration.eventID`. Rimuovi il valore corrente e incolla il tuo eventID lì.

Come promemoria, l&#39;ID evento si trova in Adobe Journey Optimizer in **Configurazioni > Eventi** e troverai l&#39;ID evento nel payload di esempio del tuo evento, che si presenta così: `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

Successivamente, devi definire la città in questo elemento dati. Vai a **placeContext > geo > city** e immetti una città scelta. Fare clic su **Salva** o **Salva nella libreria**.

![ACOP](./images/payloadeventIDgeo.png)

Infine, devi pubblicare le modifiche. Vai a **Flusso di pubblicazione** nel menu a sinistra.

![Configurazione lancio](./images/rule8.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi fai clic su **Salva e genera in sviluppo**.

![Configurazione lancio](./images/rule9.png)

## 3.2.5.2 Attivare il percorso

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

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

Nel pannello Visualizzatore profili, fai clic su **UTILITÀ**. Immetti `geofenceevent` e fai clic su **Invia**.

![Demo](./images/smsdemo1.png)

Un paio di secondi dopo, riceverai un SMS da Adobe Journey Optimizer.

![Demo](./images/smsdemo4.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Torna a tutti i moduli](../../../overview.md)
