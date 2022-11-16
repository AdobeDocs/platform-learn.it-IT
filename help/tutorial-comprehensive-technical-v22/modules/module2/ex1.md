---
title: Foundation - Acquisizione dati - Da sconosciuti a noti sul sito web
description: Foundation - Acquisizione dati - Da sconosciuti a noti sul sito web
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 683c7dd9-af69-456e-ab75-2a694588e3b3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# 2.1 - Da sconosciuto a noto sul sito web

## Contesto

Il percorso da sconosciuto a noto è uno degli argomenti più importanti tra i marchi di oggi, così come il percorso dei clienti dall&#39;acquisizione alla fidelizzazione.

Adobe Experience Platform gioca un ruolo enorme in questo percorso. La piattaforma è il cervello per la comunicazione, il sistema di esperienza di record.

Platform è un ambiente in cui la parola **cliente** è più ampio del solo **noto** Clienti. Questo è un aspetto molto importante da menzionare quando si parla ai marchi: un visitatore sconosciuto sul sito web è anche un cliente dal punto di vista di Platform e, di conseguenza, a Platform viene inviato anche tutto il comportamento di un visitatore sconosciuto. Grazie a questo approccio, quando il cliente diventa un cliente noto, un marchio può visualizzare anche ciò che è successo prima di quel momento. Questo aiuta dal punto di vista dell’attribuzione e dell’ottimizzazione dell’esperienza.

## Cosa farai?

Ora i dati vengono inseriti in Adobe Experience Platform e collegati a identificatori come ECID e indirizzi e-mail. L&#39;obiettivo è quello di comprendere il contesto di business di ciò che stai per fare dal punto di vista della configurazione. Nell’esercizio successivo, inizierai a configurare tutto il necessario per rendere possibile l’inserimento di tutti i dati nel tuo ambiente sandbox.

### Flusso del Percorso cliente

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

![Demo](./images/pv1.png)

Guarda il pannello Visualizzatore profili e il Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore principale per questo cliente attualmente sconosciuto.

![Demo](./images/pv2.png)

Puoi anche visualizzare tutti gli eventi di esperienza raccolti in base al comportamento del cliente. L’elenco è attualmente vuoto, ma questo verrà modificato presto.

![Demo](../module2/images/pv3.png)

Vai a **Uomini** categoria di prodotti. Quindi, fai clic sul prodotto **Giacca vento Montana**.

![Demo](../module2/images/pv4.png)

Viene visualizzata la pagina dei dettagli del prodotto. Un evento di esperienza di tipo **Visualizzazione prodotto** è stato inviato a Adobe Experience Platform utilizzando l’implementazione SDK per web rivista nel modulo 1.

![Demo](../module2/images/pv5.png)

Apri il pannello Visualizzatore fornitori e dai un&#39;occhiata al tuo **Eventi esperienza**.

![Demo](../module2/images/pv6.png)

Torna alla pagina **Donne** e fare clic su un altro prodotto. Un altro evento esperienza è stato inviato a Adobe Experience Platform.

![Demo](../module2/images/pv7.png)

Apri il pannello Visualizzatore profilo . Ora vedrai 2 Eventi esperienza di tipo **Visualizzazione prodotto**. Anche se il comportamento è anonimo, siamo in grado di monitorare ogni clic e archiviarlo in Adobe Experience Platform. Una volta che il cliente anonimo sarà noto, saremo in grado di unire automaticamente tutti i comportamenti anonimi al profilo noto.

![Demo](../module2/images/pv8.png)

Vai alla pagina Registrazione/Accesso . Fai clic su **CREARE UN ACCOUNT**.

![Demo](../module2/images/pv9.png)

Inserisci i tuoi dati e fai clic su **Registro** dopo di che verrai reindirizzato alla pagina precedente.

![Demo](../module2/images/pv10.png)

Apri il pannello Visualizzatore profili e vai a Profilo cliente in tempo reale. Nel pannello Visualizzatore profilo dovrebbero essere visualizzati tutti i dati personali, come le e-mail e gli identificatori telefonici appena aggiunti.

![Demo](../module2/images/pv11.png)

Nel pannello Visualizzatore profilo, vai a Eventi esperienza. I 2 prodotti visualizzati in precedenza sono disponibili nel pannello Visualizzatore profilo. Entrambi questi eventi sono ora collegati anche al tuo profilo &quot;noto&quot;.

![Demo](../module2/images/pv12.png)

Ora hai acquisito i dati in Adobe Experience Platform e li hai collegati a identificatori come ECID e indirizzi e-mail. L&#39;obiettivo è capire il contesto commerciale di ciò che stai per fare. Nell’esercizio successivo, inizierai a configurare tutto il necessario per rendere possibile l’inserimento di tutti i dati.

Passaggio successivo: [2.2 Configurare gli schemi e impostare gli identificatori](./ex2.md)

[Torna al modulo 2](./data-ingestion.md)

[Torna a tutti i moduli](../../overview.md)
