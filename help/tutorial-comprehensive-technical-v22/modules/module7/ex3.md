---
title: 'Modulo 7: aggiorna l’ID di configurazione e verifica il Percorso'
description: Aggiorna l'ID configurazione e verifica il Percorso
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: d3ceb676-d7f5-4f52-85a4-deaa5ef24034
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 1%

---

# 7.3 Aggiorna la proprietà Data Collection e verifica il percorso

## 7.3.1 Aggiorna la proprietà Data Collection

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/launch/) e seleziona **Tag**.

Questa è la pagina Proprietà raccolta dati di Adobe Experience Platform che hai visto prima.

![Pagina Proprietà](../module1/images/launch1.png)

Nel modulo 0, Demo System ha creato due proprietà Client: uno per il sito web e uno per l’app mobile. Trovarli cercando `--demoProfileLdap--` in **[!UICONTROL Ricerca]** scatola. Fai clic per aprire **Web** proprietà.

![Casella di ricerca](../module1/images/property6.png)

Vedrete questo.

![Configurazione di Launch](./images/rule1.png)

Nel menu a sinistra, vai a **Regole** e cerca la regola **Registra profilo**. Fai clic sulla regola **Registra profilo** per aprirlo.

![Configurazione di Launch](./images/rule2.png)

Verranno quindi visualizzati i dettagli di questa regola. Fai clic per aprire l’azione **Invia &quot;Evento di registrazione&quot; ad AEP - trigger JO**.

![Configurazione di Launch](./images/rule3.png)

Vedrai quindi che quando questa azione viene attivata, viene utilizzato un elemento dati specifico per definire la struttura dati XDM. È necessario aggiornare tale elemento dati e definire le **ID evento** dell&#39;evento configurato in [Esercizio 7.1](./ex1.md).

![Configurazione di Launch](./images/rule4.png)

Ora devi aggiornare l’elemento dati **XDM - Evento di registrazione**. Per farlo, vai a **Elementi dati**. Cerca **XDM - Evento di registrazione** e fai clic su per aprire l&#39;elemento dati.

![Configurazione di Launch](./images/rule5.png)

Vedrai questo:

![Configurazione di Launch](./images/rule6.png)

Passa al campo . `_experience.campaign.orchestration.eventID`. Rimuovi il valore corrente e incolla qui il tuo eventID.

Per promemoria, l’ID evento si trova in Adobe Journey Optimizer in **Configurazioni > Eventi** e troverai l’ID evento nel payload di esempio del tuo even, che si presenta così: `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

Dopo aver incollato l&#39;ID evento, la schermata dovrebbe essere simile a questa. Quindi, fai clic su **Salva** o **Salva nella libreria**.

![Configurazione di Launch](./images/rule7.png)

Infine, devi pubblicare le modifiche. Vai a **Flusso di pubblicazione** nel menu a sinistra.

![Configurazione di Launch](./images/rule8.png)

Fai clic su **Aggiungi tutte le risorse modificate** quindi fai clic su **Salva e genera in sviluppo**.

![Configurazione di Launch](./images/rule9.png)

La libreria verrà quindi aggiornata e dopo 1-2 minuti potrai procedere e verificare la configurazione.

## 7.3.2 Testare il Percorso

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, vedrai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](../module0/images/web8.png)

Sulla **Schermi** pagina, fai clic su **Esegui**.

![DSN](../module1/images/web2.png)

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

Fai clic sull’icona del logo Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](../module2/images/pv1.png)

Guarda il pannello Visualizzatore profili e il Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore principale per questo cliente attualmente sconosciuto.

![Demo](../module2/images/pv2.png)

Vai alla pagina Registrazione/Accesso . Fai clic su **CREARE UN ACCOUNT**.

![Demo](../module2/images/pv9.png)

Inserisci i tuoi dati e fai clic su **Registro** dopo di che verrai reindirizzato alla pagina precedente.

![Demo](../module2/images/pv10.png)

Apri il pannello Visualizzatore profili e vai a Profilo cliente in tempo reale. Nel pannello Visualizzatore profilo dovrebbero essere visualizzati tutti i dati personali, come le e-mail e gli identificatori telefonici appena aggiunti.

![Demo](../module2/images/pv11.png)

1 minuto dopo aver creato il tuo account, riceverai l’e-mail di creazione del tuo account da Adobe Journey Optimizer.

![Configurazione di Launch](./images/email.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 7](./journey-orchestration-create-account.md)

[Torna a tutti i moduli](../../overview.md)
