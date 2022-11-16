---
title: Guida introduttiva - Creare il Datastream
description: Guida introduttiva - Creare il Datastream
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: c967b01e-9a0b-4a74-b536-706db0cb237f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 1%

---

# 0.3 Creare il Datastream

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Dopo l’esercizio precedente, ora disponi di due proprietà di raccolta dati: uno per il web e uno per il mobile.

![DSN](./images/launchprop.png)

Queste proprietà sono quasi pronte per essere utilizzate, ma prima di poter iniziare a raccogliere dati utilizzando queste proprietà devi impostare un datastream. Otterrai maggiori informazioni sul concetto di ciò che un datastream è e cosa significa nell&#39;esercizio 1.2.

Per il momento, segui questi passaggi.

## 0.3.1 Creare il Datastream per Web

Fai clic su **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]**.

![Fai clic sull’icona Configurazione bordo nella barra di navigazione a sinistra](./images/edgeconfig1a.png)

Nell’angolo in alto a destra dello schermo, seleziona il nome della sandbox, che deve essere `--aepSandboxId--`.

![Fai clic sull’icona Configurazione bordo nella barra di navigazione a sinistra](./images/edgeconfig1b.png)

Fai clic su **[!UICONTROL Nuovo Datastream]**.

![Fai clic sull’icona Configurazione bordo nella barra di navigazione a sinistra](./images/edgeconfig1.png)

Per **[!UICONTROL Nome descrittivo]** e per la descrizione facoltativa, immetti `--demoProfileLdap-- - Demo System Datastream`. Per Schema evento, seleziona **Sistema demo - Schema evento per sito web (Global v1.1)**. Fai clic su **Salva**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig2.png)

Vedrete questo. Fai clic su **Aggiungi servizio**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig3.png)

Selezionare il servizio **[!UICONTROL Adobe Experience Platform]**, che esporrà campi aggiuntivi. Vedrete questo.

Per Set di dati evento, seleziona **Sistema di demo - Set di dati evento per il sito web (Global v1.1)** e per il set di dati profilo, seleziona **Sistema di demo - Set di dati di profilo per il sito web (Global v1.1)**. Fai clic su **Salva**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig4.png)

Ora vedrete questo.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig5.png)

È tutto per ora. In [Modulo 1](./../module1/data-ingestion-launch-web-sdk.md) ulteriori informazioni su SDK per web e su come configurare tutte le sue funzionalità.

Nel menu a sinistra, fai clic su **[!UICONTROL Tag]**.

Filtra i risultati della ricerca per visualizzare le tue due proprietà di raccolta dati. Apri la proprietà per **Web** facendo clic su di essa.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig10a.png)

Vedrete questo. Fai clic su **Estensioni**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig11.png)

Nell’estensione Adobe Experience Platform Web SDK, fai clic su **Configura**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig12.png)

Vedrete questo. Per **Datastreams**, al momento vedrai un valore fittizio impostato su 1. Ora devi fare clic sul pulsante **Scegli dall’elenco** pulsante di scelta. Nell’elenco a discesa , seleziona il Datastream creato in precedenza.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig13.png)

Assicurati di aver selezionato il **Datastream**. SUGGERIMENTO: Puoi filtrare facilmente i risultati nel menu a discesa digitando il tuo `--demoProfileLdap--`.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig14.png)

Scorri verso il basso fino a visualizzare **Raccolta dati**. Assicurati che la casella di controllo per **Abilita raccolta dati clic** non è abilitato. Fai clic su **Salva** per salvare le modifiche.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig14a.png)

Vai a **Flusso di pubblicazione**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig15.png)

Fai clic sul pulsante **...** per **Principale**, quindi fai clic su **Modifica**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig16.png)

Fai clic su **Aggiungi tutte le risorse modificate** quindi fai clic su **Salva e genera per sviluppo**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig17.png)

Le modifiche sono in fase di pubblicazione e saranno pronte tra un paio di minuti.

## 0.3.2 Creare il Datastream per Mobile

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Fai clic su **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]**.

![Fai clic sull’icona Datastream nella navigazione a sinistra](./images/edgeconfig1a.png)

Nell’angolo in alto a destra dello schermo, seleziona il nome della sandbox, che deve essere `--aepSandboxId--`.

![Fai clic sull’icona Configurazione bordo nella barra di navigazione a sinistra](./images/edgeconfig1b.png)

Fai clic su **[!UICONTROL Nuovo Datastream]**.

![Fai clic sull’icona Datastream nella navigazione a sinistra](./images/edgeconfig1.png)

Per **[!UICONTROL Nome descrittivo]** e per la descrizione facoltativa, immetti `--demoProfileLdap-- - Demo System Datastream (Mobile)`. Per Schema evento, seleziona **Sistema demo - Schema evento per app mobile (versione globale 1.1)**. Fai clic su **Salva**.

Fai clic su **[!UICONTROL Salva]**.

![Assegna un nome al Datastream e salva](./images/edgeconfig2m.png)

Vedrete questo. Fai clic su **Aggiungi servizio**.

![Assegna un nome al Datastream e salva](./images/edgeconfig3m.png)

Selezionare il servizio **[!UICONTROL Adobe Experience Platform]**, che esporrà campi aggiuntivi. Vedrete questo.

Per Set di dati evento, seleziona **Sistema di demo - Set di dati evento per app mobile (Global v1.1)** e per il set di dati profilo, seleziona **Sistema di demo - Set di dati di profilo per app mobile (Global v1.1)**. Fai clic su **Salva**.

![Assegna un nome alla configurazione del Datastream e salva](./images/edgeconfig4m.png)

Vedrete questo.

![Assegna un nome alla configurazione del Datastream e salva](./images/edgeconfig5m.png)

Il Datastream è ora pronto per essere utilizzato nella proprietà del client di raccolta dati di Adobe Experience Platform per Mobile.

Vai a **Tag** e filtrare i risultati della ricerca per visualizzare le due proprietà di raccolta dati. Apri la proprietà per **Mobile** facendo clic su di essa.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig10am.png)

Vedrete questo. Fai clic su **Estensioni**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig11m.png)

Sulla **Adobe Experience Platform Edge Network** estensione, fai clic su **Configura**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig12m.png)

Vedrete questo. Ora devi selezionare la sandbox e il datastream corretti che hai appena configurato. La sandbox da utilizzare è `--aepSandboxId--` e il datastream è chiamato `--demoProfileLdap-- - Demo System Datastream (Mobile)`.

Per **Dominio di rete Edge**, utilizza il dominio predefinito **edge.adobedc.net**.

Fai clic su **Salva** per salvare le modifiche.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig13m.png)

Vai a **Flusso di pubblicazione**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig15m.png)

Fai clic sul pulsante **...** accanto a **Principale**, quindi fai clic su **Modifica**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig16m.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi fai clic su **Salva e genera per sviluppo**.

![Assegna un nome alla configurazione Edge e salva](./images/edgeconfig17m.png)

Le modifiche sono in fase di pubblicazione e saranno pronte tra un paio di minuti.

Passaggio successivo: [0.4 Utilizzare il sito web](./ex4.md)

[Torna al modulo 0](./getting-started.md)

[Torna a tutti i moduli](./../../overview.md)