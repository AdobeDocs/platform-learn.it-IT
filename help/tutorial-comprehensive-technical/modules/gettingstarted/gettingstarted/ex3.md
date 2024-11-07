---
title: 'Guida introduttiva: creare lo stream di dati'
description: 'Guida introduttiva: creare lo stream di dati'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---

# 0.3 Creare lo stream di dati

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/). Dopo l’esercizio precedente, ora disponi di due proprietà di Raccolta dati: una per il web e una per i dispositivi mobili.

![DSN](./images/launchprop.png)

Queste proprietà sono quasi pronte per essere utilizzate, ma prima di poter iniziare a raccogliere dati utilizzando queste proprietà è necessario impostare un flusso di dati. Otterrai ulteriori informazioni sul concetto di flusso di dati e sul suo significato nell’esercizio 1.2.

Per il momento, segui questi passaggi.

## 0.3.1 Creare lo stream di dati per il web

Fare clic su **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]**.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1a.png)

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Fare clic su **[!UICONTROL Nuovo flusso di dati]**.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1.png)

Per **[!UICONTROL Nome descrittivo]** e per la descrizione facoltativa, immettere `--aepUserLdap-- - Demo System Datastream`. Per Schema evento, selezionare **Sistema demo - Schema evento per sito Web (Global v1.1)**. Fai clic su **Salva**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig2.png)

Poi vedrai questo. Fare clic su **Aggiungi servizio**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig3.png)

Selezionare il servizio **[!UICONTROL Adobe Experience Platform]**, che esporrà campi aggiuntivi. Poi vedrai questo.

Per Set di dati evento, selezionare **Sistema demo - Set di dati evento per sito Web (Global v1.1)** e per Set di dati profilo, selezionare **Sistema demo - Set di dati profilo per sito Web (Global v1.1)**. Fai clic su **Salva**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig4.png)

Ora vedrai questo.

![Denomina la configurazione di Edge e salva](./images/edgeconfig5.png)

È tutto per ora. Nel [modulo 1.1](./../../../modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md) verranno fornite ulteriori informazioni su Web SDK e su come configurarne tutte le funzionalità.

Nel menu a sinistra, fai clic su **[!UICONTROL Tag]**.

Filtra i risultati della ricerca per visualizzare le due proprietà di raccolta dati. Aprire la proprietà per **Web** facendo clic su di essa.

![Denomina la configurazione di Edge e salva](./images/edgeconfig10a.png)

Poi vedrai questo. Fare clic su **Estensioni**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig11.png)

Nell&#39;estensione Adobe Experience Platform Web SDK fare clic su **Configura**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig12.png)

Poi vedrai questo. Per **Datastreams**, verrà visualizzato un valore fittizio impostato su 1. È ora necessario fare clic sul pulsante di scelta **Scegli dall&#39;elenco**. Nell’elenco a discesa, seleziona lo stream di dati creato in precedenza.

![Denomina la configurazione di Edge e salva](./images/edgeconfig13.png)

Assicurati di aver selezionato lo **stream di dati**. SUGGERIMENTO: è possibile filtrare facilmente i risultati nel menu a discesa digitando `--aepUserLdap--`.

![Denomina la configurazione di Edge e salva](./images/edgeconfig14.png)

Scorri verso il basso fino a visualizzare **Raccolta dati**. Verificare che la casella di controllo per **Abilita raccolta dati sui clic** non sia abilitata. Fai clic su **Salva** per salvare le modifiche.

![Denomina la configurazione di Edge e salva](./images/edgeconfig14a.png)

Vai a **Flusso di pubblicazione**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig15.png)

Fai clic su **...** per **Principale**, quindi su **Modifica**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig16.png)

Fare clic su **Aggiungi tutte le risorse modificate** e quindi su **Salva e genera per sviluppo**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig17.png)

Le modifiche sono ora in fase di pubblicazione e saranno pronte tra un paio di minuti.

## 0.3.2 Creare lo stream di dati per dispositivi mobili

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/).

Fare clic su **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]**.

![Fai clic sull&#39;icona dello stream di dati nell&#39;area di navigazione a sinistra](./images/edgeconfig1a.png)

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Fare clic su **[!UICONTROL Nuovo flusso di dati]**.

![Fai clic sull&#39;icona dello stream di dati nell&#39;area di navigazione a sinistra](./images/edgeconfig1.png)

Per **[!UICONTROL Nome descrittivo]** e per la descrizione facoltativa, immettere `--aepUserLdap-- - Demo System Datastream (Mobile)`. Per Schema eventi, selezionare **Sistema demo - Schema eventi per app mobile (Global v1.1)**. Fai clic su **Salva**.

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

Nell&#39;estensione **Adobe Experience Platform Edge Network**, fare clic su **Configura**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig12m.png)

Poi vedrai questo. Ora devi selezionare la sandbox e il flusso di dati corretti che hai appena configurato. La sandbox da utilizzare è `--aepSandboxName--` e lo stream di dati è denominato `--aepUserLdap-- - Demo System Datastream (Mobile)`.

Per il **dominio Edge Network**, utilizzare il dominio predefinito **edge.adobedc.net**.

Fai clic su **Salva** per salvare le modifiche.

![Denomina la configurazione di Edge e salva](./images/edgeconfig13m.png)

Vai a **Flusso di pubblicazione**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig15m.png)

Fai clic su **...** accanto a **Principale**, quindi su **Modifica**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig16m.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi su **Salva e genera per sviluppo**.

![Denomina la configurazione di Edge e salva](./images/edgeconfig17m.png)

Le modifiche sono ora in fase di pubblicazione e saranno pronte tra un paio di minuti.

Passaggio successivo: [0.4 Utilizzare il sito Web](./ex4.md)

[Torna al modulo 0](./getting-started.md)

[Torna a tutti i moduli](./../../../overview.md)