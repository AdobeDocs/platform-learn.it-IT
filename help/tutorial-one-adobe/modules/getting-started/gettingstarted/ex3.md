---
title: 'Guida introduttiva: creare lo stream di dati'
description: 'Guida introduttiva: creare lo stream di dati'
kt: 5342
doc-type: tutorial
exl-id: d36057b4-64c6-4389-9612-d3c9cf013117
source-git-commit: cc8efbdbcf90607f5a9bc98a2e787b61b4cd66d9
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---

# Creare lo stream di dati

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/){target="_blank"}.

![DSN](./images/launchprop.png)

Prima di continuare, accertati di aver selezionato l’ambiente corretto utilizzando il selettore di ambiente nell’angolo in alto a destra dello schermo. L&#39;ambiente corretto da utilizzare è denominato `--aepImsOrgName--`.

>[!NOTE]
>
> La schermata seguente mostra un’organizzazione specifica selezionata. Durante l’esercitazione, è molto probabile che il nome dell’organizzazione sia diverso. Quando ti sei iscritto a questo tutorial, ti sono stati forniti i dettagli dell’ambiente da utilizzare, segui queste istruzioni.


![DSN](./images/org.png)

Nel menu a sinistra, fai clic su **[!UICONTROL Tag]**. Dopo l’esercizio precedente, ora disponi di 3 proprietà di raccolta dati: una per il web, una per i dispositivi mobili e una per l’app CX.

![DSN](./images/launchprop1.png)

Queste proprietà sono quasi pronte per essere utilizzate, ma prima di poter iniziare a raccogliere dati utilizzando queste proprietà è necessario impostare un flusso di dati. In un esercizio successivo nel modulo di raccolta dei dati troverai ulteriori informazioni sul concetto di flusso di dati e sul suo significato.

Per il momento, segui questi passaggi.

## Creare lo stream di dati per il web

Fare clic su **[!UICONTROL Datastreams]**.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1a.png)

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`.

>[!NOTE]
>
> La schermata seguente mostra una sandbox specifica selezionata. Durante l’esercitazione, è molto probabile che il nome della sandbox sia diverso. Quando ti sei iscritto a questo tutorial, ti sono stati forniti i dettagli dell’ambiente da utilizzare, segui queste istruzioni.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Fare clic su **[!UICONTROL Nuovo flusso di dati]**.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1.png)

Per **Name** e per la descrizione facoltativa, immettere `--aepUserLdap-- - One Adobe Datastream`. Per **Schema mappatura**, selezionare **Sistema demo - Schema evento per sito Web (Global v1.1)**. Fai clic su **Salva**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig2.png)

Poi vedrai questo. Fare clic su **Aggiungi servizio**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig3.png)

Selezionare il servizio **[!UICONTROL Adobe Experience Platform]**, che esporrà campi aggiuntivi. Poi vedrai questo.

Per Set di dati evento, selezionare **Sistema demo - Set di dati evento per sito Web (Global v1.1)** e per Set di dati profilo, selezionare **Sistema demo - Set di dati profilo per sito Web (Global v1.1)**. Fai clic su **Salva**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig4.png)

Ora vedrai questo.

![Denomina la configurazione di Edge e salva](./images/edgeconfig5.png)

Nel menu a sinistra, fai clic su **[!UICONTROL Tag]**.

Filtra i risultati della ricerca per visualizzare le proprietà di raccolta dati. Aprire la proprietà per **Web** facendo clic su di essa.

![Denomina la configurazione di Edge e salva](./images/edgeconfig10a.png)

Poi vedrai questo. Fare clic su **Estensioni**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig11.png)

Fare clic sull&#39;estensione Adobe Experience Platform Web SDK e quindi su **Configura**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig12.png)

Poi vedrai questo. Dai un&#39;occhiata al menu **Flussi di dati** e assicurati che sia selezionata la sandbox corretta, che in questo caso dovrebbe essere `--aepSandboxName--`.

![Denomina la configurazione di Edge e salva](./images/edgeconfig12a.png)

Apri il menu a discesa **Datastreams** e seleziona lo stream di dati creato in precedenza.

![Denomina la configurazione di Edge e salva](./images/edgeconfig13.png)

Assicurati di aver selezionato lo **stream di dati** in tutti e tre i diversi ambienti. Quindi fare clic su **Salva**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig14.png)

Vai a **Flusso di pubblicazione**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig15.png)

Fai clic su **...** per **Principale**, quindi su **Modifica**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig16.png)

Fare clic su **Aggiungi tutte le risorse modificate** e quindi su **Salva e genera per sviluppo**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig17.png)

Le modifiche sono in fase di pubblicazione e saranno pronte tra qualche minuto, dopodiché verrà visualizzato il punto verde accanto a **Principale**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig17a.png)

## Creare lo stream di dati per dispositivi mobili

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/){target="_blank"}.

Fare clic su **[!UICONTROL Datastreams]**.

![Fai clic sull&#39;icona dello stream di dati nell&#39;area di navigazione a sinistra](./images/edgeconfig1a.png)

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`.

>[!NOTE]
>
> La schermata seguente mostra una sandbox specifica selezionata. Durante l’esercitazione, è molto probabile che il nome della sandbox sia diverso. Quando ti sei iscritto a questo tutorial, ti sono stati forniti i dettagli dell’ambiente da utilizzare, segui queste istruzioni.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Fare clic su **[!UICONTROL Nuovo flusso di dati]**.

![Fai clic sull&#39;icona dello stream di dati nell&#39;area di navigazione a sinistra](./images/edgeconfig1.png)

Per **[!UICONTROL Nome descrittivo]** e per la descrizione facoltativa, immettere `--aepUserLdap-- - One Adobe Datastream (Mobile)`. Per **Schema mappatura**, selezionare **Sistema demo - Schema evento per app mobile (Global v1.1)**. Fai clic su **Salva**.

Fai clic su **[!UICONTROL Salva]**.

![Denomina lo stream di dati e salva](./images/edgeconfig2m.png)

Poi vedrai questo. Fare clic su **Aggiungi servizio**.

![Denomina lo stream di dati e salva](./images/edgeconfig3m.png)

Selezionare il servizio **[!UICONTROL Adobe Experience Platform]**, che esporrà campi aggiuntivi. Poi vedrai questo.

Per Set di dati evento, selezionare **Sistema demo - Set di dati evento per app mobile (Global v1.1)** e per Set di dati profilo, selezionare **Sistema demo - Set di dati profilo per app mobile (Global v1.1)**. Fai clic su **Salva**.

![Denomina la configurazione dello stream di dati e salva](./images/edgeconfig4m.png)

Poi vedrai questo.

![Denomina la configurazione dello stream di dati e salva](./images/edgeconfig5m.png)

Lo stream di dati è ora pronto per essere utilizzato nella proprietà Client di raccolta dati di Adobe Experience Platform per dispositivi mobili.

Vai a **Tag** e filtra i risultati della ricerca per visualizzare le due proprietà di raccolta dati. Apri la proprietà per **Mobile** facendo clic su di essa.

![Denomina la configurazione di Edge e salva](./images/edgeconfig10am.png)

Poi vedrai questo. Fare clic su **Estensioni**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig11m.png)

Fare clic sull&#39;estensione **Adobe Experience Platform Edge Network** e quindi su **Configura**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig12m.png)

Poi vedrai questo. Ora devi selezionare la sandbox e il flusso di dati corretti che hai appena configurato. La sandbox da utilizzare è `--aepSandboxName--` e lo stream di dati è denominato `--aepUserLdap-- - One Adobe Datastream (Mobile)`.

Per il **dominio Edge Network**, utilizzare il dominio predefinito.

Fai clic su **Salva** per salvare le modifiche.

![Denomina la configurazione di Edge e salva](./images/edgeconfig13m.png)

Vai a **Flusso di pubblicazione**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig15m.png)

Fai clic su **...** accanto a **Principale**, quindi su **Modifica**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig16m.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi su **Salva e genera per sviluppo**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig17m.png)

Le modifiche sono in fase di pubblicazione e saranno pronte tra qualche minuto, dopodiché verrà visualizzato il punto verde accanto a **Principale**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig17ma.png)

## Passaggi successivi

Vai a [Utilizza il sito Web](./ex4.md){target="_blank"}

Torna a [Guida introduttiva](./getting-started.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}