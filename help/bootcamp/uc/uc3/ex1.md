---
title: Bootcamp - Blending physical and digital - Utilizza l’app mobile e attiva una voce beacon
description: Bootcamp - Blending physical and digital - Utilizza l’app mobile e attiva una voce beacon
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Mobile SDK
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 3.1 Usare l&#39;app mobile e attivare una voce beacon

## Installare l’app mobile

Prima di installare l’app, è necessario abilitare **Tracciamento** sul dispositivo iOS. Per farlo, vai a **Impostazioni** > **Privacy e sicurezza** > **Tracciamento** e assicurarsi che l&#39;opzione **Consenti alle app di richiedere il tracciamento**.

![DSN](./../uc3/images/app4.png)

Vai a Apple App Store e cerca `aepmobile-bootcamp`. Clic **Installa** o **Scarica**.

![DSN](./../uc3/images/app1.png)

Una volta installata l’app, fai clic su **Apri**.

![DSN](./../uc3/images/app2.png)

Fai clic su **OK**.

![DSN](./../uc3/images/app9.png)

Clic **Consenti**.

![DSN](./../uc3/images/app3.png)

Clic **Accetto**.

![DSN](./../uc3/images/app7.png)

Clic **Consenti durante l&#39;utilizzo dell&#39;app**.

![DSN](./../uc3/images/app8.png)

Clic **Consenti**.

![DSN](./../uc3/images/app5.png)

Ora sei nell’app, nella home page, pronto per passare attraverso il percorso di clienti.

![DSN](./../uc3/images/app12.png)

## Flusso di percorso cliente

Prima di tutto, devi effettuare l’accesso. Fai clic su **Accedi**.

![DSN](./images/app13.png)

Dopo aver creato l’account negli esercizi precedenti, l’hai visto sul sito web. Per accedere, ora devi riutilizzare l’indirizzo e-mail dell’account creato nell’app.

![Demo](./images/pv1.png)

Inserisci qui l’indirizzo e-mail utilizzato sul sito web e fai clic su **Login**.

![DSN](./images/app14.png)

Riceverai una conferma di accesso e una notifica push.

![DSN](./images/app15.png)

Torna alla home page dell’app per visualizzare funzionalità aggiuntive.

![DSN](./images/app17.png)

Per prima cosa, vai a **Prodotti**. Fai clic su qualsiasi prodotto, in questo esempio **Caffè a disposizione**.

![DSN](./images/app19.png)

Vedrai il **Caffè a disposizione** nell’app.

![DSN](./images/app20.png)

Ora simuli un evento di ingresso beacon in un percorso di archivio offline. L&#39;obiettivo di questa simulazione è quello di personalizzare l&#39;esperienza del cliente sugli schermi all&#39;interno del negozio. Per visualizzare l’esperienza nel negozio, è stata creata una pagina che mostra in modo dinamico le informazioni rilevanti per il cliente che è appena entrato nel negozio.

Prima di continuare, aprire la pagina Web nel computer: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

A questo punto viene visualizzato quanto segue:

![DSN](./images/screen1.png)

Quindi, torna alla home page. Fai clic su **beacon** icona.

![DSN](./images/app23.png)

Poi vedrai questo. Seleziona innanzitutto **Beacon schermo bootcamp** e quindi fare clic su **voce** pulsante. Questo consente di simulare una voce beacon.

![DSN](./images/app21.png)

Dai un&#39;occhiata allo schermo del negozio. Vedrai l’ultimo prodotto visualizzato lì entro 5 secondi.

![DSN](./images/screen2.png)

Quindi, torna a **Prodotti**. Fai clic su qualsiasi prodotto, in questo esempio **Coperta da spiaggia Tan**.

![DSN](./images/app22.png)

Quindi, torna alla home page. Fai clic su **beacon** icona.

![DSN](./images/app23.png)

Poi vedrai questo. Seleziona innanzitutto **Beacon schermo bootcamp** e quindi fare clic su **voce** pulsante di nuovo. Questo consente di simulare una voce beacon.

![DSN](./images/app21.png)

Dai un&#39;occhiata allo schermo del negozio. Vedrai l’ultimo prodotto visualizzato lì entro 5 secondi.

![DSN](./images/screen3.png)

Diamo anche un’occhiata al tuo Visualizzatore profili sul sito web ora. Vedrai molti eventi aggiunti lì, solo per mostrare che ogni interazione con un cliente viene raccolta e memorizzata in Adobe Experience Platform.

![DSN](./images/screen4.png)

Negli esercizi successivi, configurerai e verificherai il tuo percorso di ingresso beacon.

Passaggio successivo: [3.2 Creare l’evento](./ex2.md)

[Torna a Flusso utente 3](./uc3.md)

[Torna a tutti i moduli](../../overview.md)
