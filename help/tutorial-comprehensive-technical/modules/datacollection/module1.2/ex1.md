---
title: Foundation - Acquisizione dei dati - Da sconosciuto a noto sul sito web
description: Foundation - Acquisizione dei dati - Da sconosciuto a noto sul sito web
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 1%

---

# 1.2.1 - Da sconosciuto a noto sul sito web

## Contesto

Il percorso da sconosciuto a noto è uno degli argomenti più importanti tra i brand di oggi, così come il percorso del cliente dall&#39;acquisizione alla conservazione.

Adobe Experience Platform gioca un ruolo fondamentale in questo percorso. Platform è il cervello della comunicazione, il sistema di esperienza di registrazione.

Platform è un ambiente in cui la parola **cliente** è più ampia rispetto ai soli **clienti noti**. Questo è un aspetto molto importante da menzionare quando si parla con i marchi: un visitatore sconosciuto sul sito web è anche un cliente dal punto di vista di Platform e, come tale, anche tutto il comportamento come visitatore sconosciuto viene inviato a Platform. Grazie a questo approccio, quando il cliente diventa un cliente noto, un marchio può visualizzare anche ciò che è successo prima di quel momento. Questo è utile dal punto di vista dell’attribuzione e dell’ottimizzazione dell’esperienza.

## Cosa farai?

Ora acquisirai i dati in Adobe Experience Platform e i dati verranno collegati a identificatori come ECID e indirizzi e-mail. L&#39;obiettivo è comprendere il contesto di business di ciò che si sta per fare dal punto di vista della configurazione. Nel prossimo esercizio, inizierai a configurare tutto il necessario per rendere possibile l’acquisizione dei dati nel tuo ambiente sandbox.

### Flusso di Percorso cliente

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](./../../gettingstarted/gettingstarted/images/web8.png)

Nella pagina **Screens** fare clic su **Esegui**.

![DSN](../module1.1/images/web2.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](./../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](./../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.


Seleziona il tipo di account e completa la procedura di accesso.


Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni dimostrazione, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.


Fai clic sull’icona del logo di Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](./images/pv1.png)

Dai un&#39;occhiata al pannello Visualizzatore profili e al Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore primario per questo cliente attualmente sconosciuto.

![Demo](./images/pv2.png)

Puoi anche visualizzare tutti gli eventi esperienza che sono stati raccolti in base al comportamento del cliente. L’elenco è attualmente vuoto, ma cambierà presto.

![Demo](../module1.2/images/pv3.png)

Vai alla categoria di prodotto **Men**. Quindi, fai clic sul prodotto **Giacca a vento Montana**.

![Demo](../module1.2/images/pv4.png)

Viene visualizzata la pagina dei dettagli del prodotto. Un evento esperienza di tipo **Visualizzazione prodotto** è stato ora inviato a Adobe Experience Platform utilizzando l&#39;implementazione Web SDK esaminata nel modulo 1.

![Demo](../module1.2/images/pv5.png)

Apri il pannello Provider Viewer e osserva i tuoi **eventi esperienza**.

![Demo](../module1.2/images/pv6.png)

Torna alla pagina della categoria **Donne** e fai clic su un altro prodotto. Un altro evento esperienza è stato inviato a Adobe Experience Platform.

![Demo](../module1.2/images/pv7.png)

Apri il pannello Visualizzatore profili. Verranno visualizzati 2 eventi esperienza di tipo **Visualizzazione prodotto**. Anche se il comportamento è anonimo, siamo in grado di tenere traccia di ogni clic e memorizzarlo in Adobe Experience Platform. Una volta che il cliente anonimo verrà a conoscenza, saremo in grado di unire automaticamente tutti i comportamenti anonimi al profilo know.

![Demo](../module1.2/images/pv8.png)

Vai alla pagina di registrazione/accesso. Fare clic su **CREA UN ACCOUNT**.

![Demo](../module1.2/images/pv9.png)

Compila i tuoi dettagli e fai clic su **Registra** dopo di che sarai reindirizzato alla pagina precedente.

![Demo](../module1.2/images/pv10.png)

Apri il pannello Visualizzatore profilo e passa a Profilo cliente in tempo reale. Nel pannello Visualizzatore profili dovresti visualizzare tutti i dati personali, come gli identificatori e-mail e telefonici appena aggiunti.

![Demo](../module1.2/images/pv11.png)

Nel pannello Visualizzatore profili, vai a Eventi esperienza. Nel pannello Visualizzatore profili vengono visualizzati i 2 prodotti precedenti. Entrambi gli eventi sono ora connessi anche al tuo profilo &quot;noto&quot;.

![Demo](../module1.2/images/pv12.png)

Ora che hai acquisito i dati in Adobe Experience Platform, li hai collegati a identificatori come ECID e indirizzi e-mail. L&#39;obiettivo è quello di capire il contesto di business di ciò che si sta per fare. Nel prossimo esercizio, inizierai a configurare tutto il necessario per rendere possibile l’acquisizione dei dati.

Passaggio successivo: [1.2.2 Configurare schemi e impostare identificatori](./ex2.md)

[Torna al modulo 1.2](./data-ingestion.md)

[Torna a tutti i moduli](../../../overview.md)
