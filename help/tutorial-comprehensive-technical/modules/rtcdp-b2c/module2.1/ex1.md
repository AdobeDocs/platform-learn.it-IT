---
title: Foundation - Real-time Customer Profile - Da sconosciuto a noto sul sito web
description: Foundation - Real-time Customer Profile - Da sconosciuto a noto sul sito web
kt: 5342
doc-type: tutorial
exl-id: ddbf97c2-8105-42b6-b9bf-209b1df6a3b5
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 2%

---

# 2.1.1 Da sconosciuto a noto sul sito web

## Contesto

Il percorso da sconosciuto a noto è uno degli argomenti più importanti tra i brand di oggi, così come il percorso del cliente dall&#39;acquisizione alla conservazione.

Adobe Experience Platform gioca un ruolo fondamentale in questo percorso. Platform è il cervello della comunicazione, il &quot;sistema di esperienza di registrazione&quot;.

Platform è un ambiente in cui la parola cliente è più ampia rispetto ai soli clienti noti. Un visitatore sconosciuto sul sito web è anche un cliente dal punto di vista di Platform e, come tale, anche tutto il comportamento di un visitatore sconosciuto viene inviato a Platform. Grazie a questo approccio, quando il visitatore diventa un cliente noto, un brand può visualizzare anche quello che è successo prima di quel momento. Questo è utile dal punto di vista dell’attribuzione e dell’ottimizzazione dell’esperienza.

## Flusso di percorso cliente

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni esercizio, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Fai clic sull’icona del logo di Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](../../datacollection/module1.2/images/pv1.png)

Dai un&#39;occhiata al pannello Visualizzatore profili e al Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore primario per questo cliente attualmente sconosciuto.

![Demo](../../datacollection/module1.2/images/pv2.png)

Puoi anche visualizzare tutti gli eventi esperienza che sono stati raccolti in base al comportamento del cliente. L’elenco è attualmente vuoto, ma cambierà presto.

![Demo](../../datacollection/module1.2/images/pv3.png)

Vai alla categoria di prodotto **Telefoni e dispositivi**. Fare clic sul prodotto **iPhone 15 Pro**.

![Demo](../../datacollection/module1.2/images/pv4.png)

Viene visualizzata la pagina dei dettagli del prodotto. Un evento esperienza di tipo **Visualizzazione prodotto** è stato ora inviato a Adobe Experience Platform utilizzando l&#39;implementazione Web SDK esaminata nel modulo 1.

![Demo](../../datacollection/module1.2/images/pv5.png)

Apri il pannello Provider Viewer e osserva i tuoi **eventi esperienza**.

![Demo](../../datacollection/module1.2/images/pv6.png)

Torna alla pagina della categoria **Telefoni e dispositivi** e fai clic su un altro prodotto. Un altro evento esperienza è stato inviato a Adobe Experience Platform. Apri il pannello Visualizzatore profili. Verranno visualizzati 2 eventi esperienza di tipo **Visualizzazione prodotto**. Anche se il comportamento è anonimo, con il consenso adeguato sul posto, puoi tenere traccia di ogni clic e memorizzarlo in Adobe Experience Platform. Una volta che il cliente anonimo verrà a conoscenza, saremo in grado di unire automaticamente tutti i comportamenti anonimi al profilo know.

![Demo](../../datacollection/module1.2/images/pv7.png)

Vai alla pagina di registrazione/accesso. Fai clic su **Accedi**.

![Demo](../../datacollection/module1.2/images/pv8.png)

Fai clic su **Crea un account**.

![Demo](../../datacollection/module1.2/images/pv9.png)

Compila i tuoi dettagli e fai clic su **Registra** dopo di che sarai reindirizzato alla pagina precedente.

![Demo](../../datacollection/module1.2/images/pv10.png)

Apri il pannello Visualizzatore profilo e passa a Profilo cliente in tempo reale. Nel pannello Visualizzatore profili dovresti visualizzare tutti i dati personali, come gli identificatori e-mail e telefonici appena aggiunti.

![Demo](../../datacollection/module1.2/images/pv11.png)

Nel pannello Visualizzatore profili, vai a Eventi esperienza. Nel pannello Visualizzatore profili vengono visualizzati i 2 prodotti precedenti. Entrambi gli eventi sono ora connessi anche al tuo profilo &quot;noto&quot;.

![Demo](../../datacollection/module1.2/images/pv12.png)

Ora che hai acquisito i dati in Adobe Experience Platform, li hai collegati a identificatori come ECID e indirizzi e-mail. L&#39;obiettivo è quello di capire il contesto di business di ciò che si sta per fare. Nel prossimo esercizio, inizierai a configurare tutto il necessario per rendere possibile l’acquisizione dei dati.

### Navigare nell’app mobile

Dopo essere diventato un cliente noto, è ora di iniziare a utilizzare l’app mobile. Apri l’app mobile sul tuo iPhone, quindi accedi all’app.

Se l&#39;app non è più installata o se non ricordi come installarla, consulta questa pagina: [Usa l&#39;app mobile](../../gettingstarted/gettingstarted/ex5.md)

Dopo aver installato l’app secondo le istruzioni, viene visualizzata la pagina di destinazione dell’app con il brand Citignal caricato. Fai clic sull’icona dell’account nella parte in alto a sinistra della schermata.

![Demo](./images/app_hp1.png)

Nella schermata Login, accedi con l’indirizzo e-mail utilizzato sul sito web desktop. Fai clic su **Accesso**.

![Demo](./images/app_acc.png)

Vai alla schermata iniziale dell’app e fai clic su per aprire qualsiasi prodotto.

![Demo](./images/app_hp.png)

Viene visualizzata la pagina dei dettagli del prodotto.

![Demo](./images/app_galaxy.png)

Vai alla schermata iniziale dell’app e scorri verso sinistra per visualizzare il pannello Visualizzatore profili. Vedrai quindi il prodotto appena visualizzato nella sezione **Eventi esperienza**, insieme a tutte le visualizzazioni prodotto della sessione del sito Web precedente.

>[!NOTE]
>
>Potrebbero essere necessari un paio di minuti prima di visualizzare la visualizzazione consolidata nell’app e sul sito web.

![Demo](./images/app_after_galaxy.png)

Tornare al computer desktop e aggiornare la home page, dopodiché verrà visualizzato anche il prodotto.

>[!NOTE]
>
>Potrebbero essere necessari un paio di minuti prima di visualizzare la visualizzazione consolidata nell’app e sul sito web.

![Demo](./images/web_x_aftermobile.png)

Ora che hai acquisito i dati in Adobe Experience Platform, li hai collegati a identificatori come ECID e indirizzi e-mail. L&#39;obiettivo di questo esercizio era quello di comprendere il contesto aziendale di ciò che si stava per fare. Ora hai creato in modo efficace un profilo cliente multi-dispositivo in tempo reale. Nel prossimo esercizio, procederai con la visualizzazione del tuo profilo in Adobe Experience Platform.

Passaggio successivo: [2.1.2 Visualizza il tuo profilo cliente in tempo reale - Interfaccia utente](./ex2.md)

[Torna al modulo 2.1](./real-time-customer-profile.md)

[Torna a tutti i moduli](../../../overview.md)
