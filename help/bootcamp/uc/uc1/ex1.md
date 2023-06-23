---
title: Bootcamp - Real-time Customer Profile - Da sconosciuto a noto sul sito web
description: Bootcamp - Real-time Customer Profile - Da sconosciuto a noto sul sito web
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---

# 1.1 Da sconosciuto a noto sul sito web

## Contesto

Il percorso da sconosciuto a noto è uno degli argomenti più importanti tra i brand di oggi, così come il percorso del cliente dall&#39;acquisizione alla conservazione.

Adobe Experience Platform gioca un ruolo fondamentale in questo percorso. Platform è il cervello per la comunicazione, **sistema di registrazione esperienza**.

Platform è un ambiente in cui la parola cliente è più ampia rispetto ai soli clienti noti. Un visitatore sconosciuto sul sito web è anche un cliente dal punto di vista di Platform e, come tale, anche tutto il comportamento di un visitatore sconosciuto viene inviato a Platform. Grazie a questo approccio, quando il visitatore diventa un cliente noto, un brand può visualizzare anche quello che è successo prima di quel momento. Questo è utile dal punto di vista dell’attribuzione e dell’ottimizzazione dell’esperienza.

## Flusso di percorso cliente

Vai a [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clic **Consenti tutto**.

![DSN](./images/web8.png)

Fai clic sull’icona del logo di Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](./images/pv1.png)

Dai un’occhiata al pannello Visualizzatore profili e al Profilo cliente in tempo reale con **ID EXPERIENCE CLOUD** come identificatore principale per questo cliente attualmente sconosciuto.

![Demo](./images/pv2.png)

Puoi anche visualizzare tutti gli eventi esperienza che sono stati raccolti in base al comportamento del cliente. L’elenco è attualmente vuoto, ma cambierà presto.

![Demo](./images/pv3.png)

Vai a **Servizi dell&#39;applicazione** e fai clic sul prodotto **Real-Time CDP**.

![Demo](./images/pv4.png)

Viene visualizzata la pagina dei dettagli del prodotto. Un evento esperienza di tipo **Visualizzazione prodotto** ora è stato inviato a Adobe Experience Platform utilizzando l’implementazione Web SDK esaminata nel Modulo 1. Apri il pannello Visualizzatore profili e osserva **Eventi esperienza**.

![Demo](./images/pv5.png)

Vai a **Servizi dell&#39;applicazione** e fai clic sul prodotto **Adobe Journey Optimizer**. Un altro evento esperienza è stato inviato a Adobe Experience Platform.

![Demo](./images/pv7.png)

Apri il pannello Visualizzatore profili. Ora vedrai 2 eventi esperienza di tipo **Visualizzazione prodotto**. Anche se il comportamento è anonimo, ogni clic viene tracciato e memorizzato in Adobe Experience Platform. Una volta che il cliente anonimo verrà a conoscenza, saremo in grado di unire automaticamente tutti i comportamenti anonimi al profilo know.

![Demo](./images/pv8.png)

Ora analizziamo il tuo profilo cliente e utilizziamo il tuo comportamento per personalizzare la tua esperienza cliente sul sito web.

Passaggio successivo: [1.2 Visualizzare il proprio profilo cliente in tempo reale - Interfaccia utente](./ex2.md)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
