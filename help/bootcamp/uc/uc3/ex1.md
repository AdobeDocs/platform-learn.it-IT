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
source-wordcount: '526'
ht-degree: 0%

---

# 3.1 Usare l&#39;app mobile e attivare una voce beacon

## Installare l’app mobile

Prima di installare l&#39;app, devi abilitare **il tracciamento** sul tuo dispositivo iOS. Per farlo, vai a **Impostazioni** > **Privacy e sicurezza** > **Tracciamento** e assicurati che l&#39;opzione **Consenti alle app di richiedere di tenere traccia**.

![DSN](./../uc3/images/app4.png)

Vai all&#39;App Store di Apple e cerca `aepmobile-bootcamp`. Fai clic su **Installa** o **Scarica**.

![DSN](./../uc3/images/app1.png)

Una volta installata l&#39;app, fai clic su **Apri**.

![DSN](./../uc3/images/app2.png)

Fai clic su **OK**.

![DSN](./../uc3/images/app9.png)

Fare clic su **Consenti**.

![DSN](./../uc3/images/app3.png)

Fai clic su **Accetto**.

![DSN](./../uc3/images/app7.png)

Fare Clic Su **Consenti Durante L&#39;Utilizzo Dell&#39;App**.

![DSN](./../uc3/images/app8.png)

Fare clic su **Consenti**.

![DSN](./../uc3/images/app5.png)

Ora sei nell’app, nella home page, pronto per passare attraverso il percorso di clienti.

![DSN](./../uc3/images/app12.png)

## Flusso di percorso cliente

Prima di tutto, devi effettuare l’accesso. Fai clic su **Accesso**.

![DSN](./images/app13.png)

Dopo aver creato l’account negli esercizi precedenti, l’hai visto sul sito web. Per accedere, ora devi riutilizzare l’indirizzo e-mail dell’account creato nell’app.

![Demo](./images/pv1.png)

Immetti qui l&#39;indirizzo e-mail utilizzato nel sito Web e fai clic su **Accedi**.

![DSN](./images/app14.png)

Riceverai una conferma di accesso e una notifica push.

![DSN](./images/app15.png)

Torna alla home page dell’app per visualizzare funzionalità aggiuntive.

![DSN](./images/app17.png)

Vai a **Prodotti**. Fai clic su un prodotto, in questo esempio **Caffè da aprire**.

![DSN](./images/app19.png)

Nell&#39;app verrà visualizzata la pagina del prodotto **Coffee to go**.

![DSN](./images/app20.png)

Ora simuli un evento di ingresso beacon in un percorso di archivio offline. L&#39;obiettivo di questa simulazione è quello di personalizzare l&#39;esperienza del cliente sugli schermi all&#39;interno del negozio. Per visualizzare l’esperienza nel negozio, è stata creata una pagina che mostra in modo dinamico le informazioni rilevanti per il cliente che è appena entrato nel negozio.

Prima di continuare, apri questa pagina Web nel computer: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

A questo punto viene visualizzato quanto segue:

![DSN](./images/screen1.png)

Quindi, torna alla home page. Fai clic sull&#39;icona **beacon**.

![DSN](./images/app23.png)

Poi vedrai questo. Selezionare innanzitutto **Bootcamp Screen Beacon** e quindi fare clic sul pulsante **entry**. Questo consente di simulare una voce beacon.

![DSN](./images/app21.png)

Dai un&#39;occhiata allo schermo del negozio. Vedrai l’ultimo prodotto visualizzato lì entro 5 secondi.

![DSN](./images/screen2.png)

Quindi, torna a **Prodotti**. Fare clic su qualsiasi prodotto, in questo esempio **Tan coperta spiaggia**.

![DSN](./images/app22.png)

Quindi, torna alla home page. Fai clic sull&#39;icona **beacon**.

![DSN](./images/app23.png)

Poi vedrai questo. Selezionare **Bootcamp Screen Beacon**, quindi fare di nuovo clic sul pulsante **entry**. Questo consente di simulare una voce beacon.

![DSN](./images/app21.png)

Dai un&#39;occhiata allo schermo del negozio. Vedrai l’ultimo prodotto visualizzato lì entro 5 secondi.

![DSN](./images/screen3.png)

Diamo anche un’occhiata al tuo Visualizzatore profili sul sito web ora. Vedrai molti eventi aggiunti lì, solo per mostrare che ogni interazione con un cliente viene raccolta e memorizzata in Adobe Experience Platform.

![DSN](./images/screen4.png)

Negli esercizi successivi, configurerai e verificherai il tuo percorso di ingresso beacon.

Passaggio successivo: [3.2 Crea l&#39;evento](./ex2.md)

[Torna a Flusso utente 3](./uc3.md)

[Torna a tutti i moduli](../../overview.md)
