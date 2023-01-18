---
title: Bootcamp - Fusione fisica e digitale - Utilizza l’app mobile e attiva una voce beacon
description: Bootcamp - Fusione fisica e digitale - Utilizza l’app mobile e attiva una voce beacon
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 3.1 Utilizza l’app mobile e attiva una voce beacon

## Installare l’app mobile

Prima di installare l’app, devi attivare **Tracking** sul tuo dispositivo iOS. Per farlo, vai a **Impostazioni** > **Privacy e sicurezza** > **Tracking** e garantire che l&#39;opzione **Consenti alle app di richiedere il tracciamento**.

![DSN](./../uc3/images/app4.png)

Vai ad Apple App Store e cerca `aepmobile-bootcamp`. Fai clic su **Installa** o **Scarica**.

![DSN](./../uc3/images/app1.png)

Una volta installata l’app, fai clic su **Apri**.

![DSN](./../uc3/images/app2.png)

Fai clic su **OK**.

![DSN](./../uc3/images/app9.png)

Fai clic su **Consenti**.

![DSN](./../uc3/images/app3.png)

Fai clic su **Sono d&#39;accordo**.

![DSN](./../uc3/images/app7.png)

Fai clic su **Consenti durante l&#39;utilizzo dell&#39;app**.

![DSN](./../uc3/images/app8.png)

Fai clic su **Consenti**.

![DSN](./../uc3/images/app5.png)

Ora ti trovi nell’app, nella home page, pronta per il percorso dei clienti.

![DSN](./../uc3/images/app12.png)

## Flusso del percorso cliente

Prima di tutto, devi effettuare l&#39;accesso. Fai clic su **Accedi**.

![DSN](./images/app13.png)

Dopo aver creato il tuo account negli esercizi precedenti, lo hai visto sul sito web. Ora devi riutilizzare l’indirizzo e-mail dell’account creato nell’app per effettuare l’accesso.

![Demo](./images/pv1.png)

Inserisci l&#39;indirizzo e-mail utilizzato sul sito web qui e fai clic su **Login**.

![DSN](./images/app14.png)

Riceverai quindi una conferma dell’accesso e riceverai una notifica push.

![DSN](./images/app15.png)

Torna alla home page dell’app e vedrai apparire funzionalità aggiuntive.

![DSN](./images/app17.png)

Per prima cosa, vai a **Prodotti**. Fai clic su un prodotto, in questo esempio **Caffè da andare**.

![DSN](./images/app19.png)

Vedrete il **Caffè da andare** pagina di prodotto nell’app.

![DSN](./images/app20.png)

Ora simulerai un evento di ingresso beacon in una posizione di archiviazione offline. L&#39;obiettivo della simulazione è quello di personalizzare l&#39;esperienza del cliente sugli schermi all&#39;interno del negozio. Per visualizzare l’esperienza in-store, è stata creata una pagina che mostrerà dinamicamente le informazioni pertinenti per il cliente che è appena entrato nello store.

Prima di continuare, aprire questa pagina Web sul computer: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Vedrai questo:

![DSN](./images/screen1.png)

Poi, torna alla homepage. Fai clic sul pulsante **beacon** icona.

![DSN](./images/app23.png)

Vedrete questo. Per prima cosa, seleziona **Beacon schermo del campeggio di avvio** quindi fai clic sul pulsante **voce** pulsante . Questo ti consente di simulare una voce del beacon.

![DSN](./images/app21.png)

Ora, date un&#39;occhiata alla schermata in-store. L’ultimo prodotto visualizzato verrà visualizzato entro 5 secondi.

![DSN](./images/screen2.png)

Quindi, torna a **Prodotti**. Fai clic su un prodotto, in questo esempio **Copertura spiaggia Tan**.

![DSN](./images/app22.png)

Poi, torna alla homepage. Fai clic sul pulsante **beacon** icona.

![DSN](./images/app23.png)

Vedrete questo. Per prima cosa, seleziona **Beacon schermo del campeggio di avvio** quindi fai clic sul pulsante **voce** di nuovo. Questo ti consente di simulare una voce del beacon.

![DSN](./images/app21.png)

Ora, guarda di nuovo la schermata in-store. L’ultimo prodotto visualizzato verrà visualizzato entro 5 secondi.

![DSN](./images/screen3.png)

Diamo anche un&#39;occhiata al vostro Visualizzatore di profili sul sito web ora. Vedrai molti eventi aggiunti lì, solo per dimostrare che qualsiasi interazione con un cliente viene raccolta e memorizzata in Adobe Experience Platform.

![DSN](./images/screen4.png)

Negli esercizi successivi, configurerai e testerai il tuo percorso di ingresso beacon.

Passaggio successivo: [3.2 Creare un evento](./ex2.md)

[Torna al flusso utente 3](./uc3.md)

[Torna a tutti i moduli](../../overview.md)
