---
title: Testare l’implementazione
description: Testare l’implementazione
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# Testare l’implementazione

Ora che hai configurato la pagina web e implementato la libreria di tag Adobe Experience Platform, è necessario testarne l’implementazione.

Apri la pagina del prodotto nel browser. Per farlo, fai clic su _File_ allora _Apri file..._ nel browser o puoi ospitare la pagina su un server web e immettere l’URL appropriato.

Dopo il caricamento della pagina, dovresti vedere qualcosa di simile a questo:

![Pagina Web](../../assets/implementation-strategy/webpage.png)

Non è carino, ma farà il suo lavoro.

## Inspect: eventi di visualizzazione della pagina e del prodotto

Apri gli strumenti per sviluppatori nel browser e fai clic sul pannello di rete. Aggiorna la pagina.

A questo punto, dovresti vedere quattro richieste:

1. product.html - La tua pagina web.
2. launch-###########-development.js - Libreria Launch.
3. interact: l’evento di visualizzazione della pagina che viene inviato al server.
4. interact: l’evento di visualizzazione del prodotto che viene inviato al server.

Puoi controllare i payload di ogni richiesta. Per il primo `interact` richiesta, dovresti essere in grado di visualizzare il payload inviato con un `eventType` di `web.webpagedetails.pageViews`.

![Ispezione della richiesta di visualizzazione pagina](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

Per il secondo `interact` richiesta, dovresti essere in grado di visualizzare il payload inviato con un `eventType` di `commerce.productViews`.

![Ispezione della richiesta di visualizzazione prodotto](../../assets/implementation-strategy/webpage-product-view-inspection.png)

Puoi consultare il resto dei dati inviati, incluse le informazioni sul prodotto.

## Inspect apre il carrello e aggiungi al carrello eventi

Ora fai clic su _Aggiungi al carrello_ pulsante.

Dovresti trovare due richieste aggiuntive, la prima con un `eventType` di `commerce.productListOpens` (per aprire un nuovo carrello) e il secondo con un `eventType` di `commerce.productListAdds` (per aggiungere il prodotto al carrello).

## Inspect: evento di clic per il collegamento scarica app

A seconda del browser, se si fa clic su un collegamento che consente di uscire dalla pagina corrente, il pannello di rete potrebbe scomparire. Poiché desideri esaminare la richiesta di rete per l’evento clic collegamento che si verifica immediatamente prima di uscire dalla pagina, devi configurare il browser per preservare i registri di rete tra le pagine. Ciò viene effettuato controllando un _Mantieni registro_ nel pannello di rete (Chrome, Safari, Edge) o facendo clic sull’icona di un ingranaggio e selezionando una _Salvataggio permanente dei registri_ nel menu visualizzato (Firefox).

Ora fai clic su _Scaricare l’app_ collegamento.

Dovresti vederne un altro `interact` nel pannello di rete. Se analizzi la richiesta, dovresti trovare un `eventType` di `web.webinteraction.linkClicks` nonché dettagli sul collegamento su cui è stato fatto clic.

## Verifica che i dati arrivino nel set di dati di Adobe Experience Platform

Ora che le richieste vengono inviate, puoi anche verificare se i dati arrivano in modo sicuro nel set di dati Adobe Experience Platform creato. Per iniziare, accedi al [!UICONTROL Set di dati] in Adobe Experience Platform.

Seleziona il set di dati creato in precedenza.

Potrebbe essere necessario attendere alcuni minuti, ma presto dovrebbero comparire indicazioni sull’elaborazione e l’inserimento dei dati nel set di dati. Dovresti anche verificare se l’elaborazione è riuscita o meno. Se fallisce, potrai vedere perché è fallito. In genere si verificano errori perché i dati che stai inviando non corrispondono allo schema e dovrai modificare di conseguenza i dati o lo schema.

![Acquisizione del set di dati](../../assets/implementation-strategy/dataset-ingestion.png)

## Utilizza l’estensione Adobe Experience Platform Debugger

Per maggiori informazioni sul comportamento dell’implementazione sia sul browser che sui server Adobe, vedi l’estensione del browser Adobe Experience Platform Debugger.

[Estensione di Adobe Experience Platform Debugger per Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Estensione di Adobe Experience Platform Debugger per Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/)
