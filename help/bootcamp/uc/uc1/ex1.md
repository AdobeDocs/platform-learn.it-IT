---
title: Bootcamp - Profilo del cliente in tempo reale - Da sconosciuto a noto sul sito web
description: Bootcamp - Profilo del cliente in tempo reale - Da sconosciuto a noto sul sito web
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---

# 1.1 Da sconosciuto a noto sul sito web

## Contesto

Il percorso da sconosciuto a noto è uno degli argomenti più importanti tra i marchi di oggi, così come il percorso dei clienti dall&#39;acquisizione alla fidelizzazione.

Adobe Experience Platform gioca un ruolo enorme in questo percorso. La piattaforma è il cervello della comunicazione, **sistema di registrazione delle esperienze**.

Platform è un ambiente in cui la parola cliente è più ampia dei soli clienti noti. Un visitatore sconosciuto sul sito web è anche un cliente dal punto di vista di Platform e, di conseguenza, a Platform viene inviato anche tutto il comportamento di un visitatore sconosciuto. Grazie a questo approccio, quando il visitatore diventa un cliente noto, un marchio può visualizzare anche ciò che è successo prima di quel momento. Questo aiuta dal punto di vista dell’attribuzione e dell’ottimizzazione dell’esperienza.

## Flusso del percorso cliente

Vai a [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Fai clic su **Consenti tutto**.

![DSN](./images/web8.png)

Fai clic sull’icona del logo Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](./images/pv1.png)

Guarda il pannello Visualizzatore profili e il Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore principale per questo cliente attualmente sconosciuto.

![Demo](./images/pv2.png)

Puoi anche visualizzare tutti gli eventi di esperienza raccolti in base al comportamento del cliente. L’elenco è attualmente vuoto, ma questo verrà modificato presto.

![Demo](./images/pv3.png)

Vai a **Servizi applicativi** opzione del menu e fai clic sul prodotto **Real-Time CDP**.

![Demo](./images/pv4.png)

Viene visualizzata la pagina dei dettagli del prodotto. Un evento di esperienza di tipo **Visualizzazione prodotto** è stato inviato a Adobe Experience Platform utilizzando l’implementazione SDK per web rivista nel modulo 1. Apri il pannello Visualizzatore profili e dai un&#39;occhiata al tuo **Eventi esperienza**.

![Demo](./images/pv5.png)

Vai a **Servizi applicativi** opzione del menu e fai clic sul prodotto **Adobe Journey Optimizer**. Un altro evento esperienza è stato inviato a Adobe Experience Platform.

![Demo](./images/pv7.png)

Apri il pannello Visualizzatore profilo . Ora vedrai 2 Eventi esperienza di tipo **Visualizzazione prodotto**. Anche se il comportamento è anonimo, ogni clic viene tracciato e memorizzato in Adobe Experience Platform. Una volta che il cliente anonimo sarà noto, saremo in grado di unire automaticamente tutti i comportamenti anonimi al profilo noto.

![Demo](./images/pv8.png)

Ora analizziamo il tuo profilo cliente e quindi utilizziamo il tuo comportamento per personalizzare la tua esperienza cliente sul sito web.

Passaggio successivo: [1.2 Visualizzare il proprio profilo cliente in tempo reale - Interfaccia](./ex2.md)

[Torna al flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
