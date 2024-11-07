---
title: Aggiorna l’ID configurazione e verifica il Percorso
description: Aggiorna l’ID configurazione e verifica il Percorso
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 3.1.3 Aggiorna la proprietà Data Collection e verifica il percorso

## 3.1.3.1 Aggiornare la proprietà Data Collection

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/launch/) e seleziona **Tag**.

Questa è la pagina Proprietà raccolta dati di Adobe Experience Platform che hai visto prima.

![Pagina delle proprietà](./../../../modules/datacollection/module1.1/images/launch1.png)

Nel modulo 0, Demo System ha creato due proprietà client per te: una per il sito web e una per l’app mobile. Trovarli cercando `--aepUserLdap--` nella casella **[!UICONTROL Cerca]**. Fare clic per aprire la proprietà **Web**.

![Casella di ricerca](./../../../modules/datacollection/module1.1/images/property6.png)

Poi vedrai questo.

![Configurazione lancio](./images/rule1.png)

Nel menu a sinistra, vai a **Regole** e cerca la regola **Registra profilo**. Fare clic sulla regola **Registra profilo** per aprirla.

![Configurazione lancio](./images/rule2.png)

Vedrai quindi i dettagli di questa regola. Fare clic per aprire l&#39;azione **Invia &quot;Evento registrazione&quot; ad AEP - Attiva JO**.

![Configurazione lancio](./images/rule3.png)

Quando questa azione viene attivata, vedrai che viene utilizzato un elemento dati specifico per definire la struttura dati XDM. È necessario aggiornare l&#39;elemento dati e definire l&#39;**ID evento** dell&#39;evento configurato in [Esercizio 7.1](./ex1.md).

![Configurazione lancio](./images/rule4.png)

Ora devi andare ad aggiornare l&#39;elemento dati **XDM - Evento registrazione**. A tale scopo, passare a **Elementi dati**. Cerca **XDM - Registration Event** e fai clic per aprire l&#39;elemento dati.

![Configurazione lancio](./images/rule5.png)

A questo punto viene visualizzato quanto segue:

![Configurazione lancio](./images/rule6.png)

Passare al campo `_experience.campaign.orchestration.eventID`. Rimuovi il valore corrente e incolla il tuo eventID lì.

Come promemoria, l&#39;ID evento si trova in Adobe Journey Optimizer in **Configurazioni > Eventi** e troverai l&#39;ID evento nel payload di esempio del tuo evento, che si presenta così: `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

Dopo aver incollato l’ID evento, lo schermo dovrebbe essere simile al seguente. Fare clic su **Salva** o **Salva nella libreria**.

![Configurazione lancio](./images/rule7.png)

Infine, devi pubblicare le modifiche. Vai a **Flusso di pubblicazione** nel menu a sinistra.

![Configurazione lancio](./images/rule8.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi fai clic su **Salva e genera in sviluppo**.

![Configurazione lancio](./images/rule9.png)

La libreria verrà quindi aggiornata e dopo 1-2 minuti puoi procedere e verificare la configurazione.

## 3.1.3.2 Test del Percorso

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Nella pagina **Screens** fare clic su **Esegui**.

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

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

1 minuto dopo aver creato l’account, riceverai l’e-mail di creazione dell’account da Adobe Journey Optimizer.

![Configurazione lancio](./images/email.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 3.1](./journey-orchestration-create-account.md)

[Torna a tutti i moduli](../../../overview.md)
