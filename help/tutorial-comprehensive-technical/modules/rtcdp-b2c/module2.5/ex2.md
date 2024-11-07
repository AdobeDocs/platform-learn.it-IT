---
title: 'Raccolta dati di Adobe Experience Platform e inoltro lato server in tempo reale: aggiorna lo stream di dati per rendere disponibili i dati per la proprietà Server di raccolta dati di Adobe Experience Platform'
description: Aggiorna lo stream di dati per rendere i dati disponibili per la proprietà del server di raccolta dati di Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---

# 2.5.2 Aggiorna lo stream di dati per rendere i dati disponibili per la proprietà Adobe Experience Platform Data Collection Server

## 2.5.2.1 Aggiornare lo stream di dati

Nell&#39;esercizio [0.2](./../../gettingstarted/gettingstarted/ex2.md) hai creato **[!UICONTROL Datastream]** personalizzato. È stato quindi utilizzato il nome `--demoProfileLdap-- - Demo System Datastream`.

In questo esercizio, devi configurare **[!UICONTROL Datastream]** in modo che funzioni con **[!DNL Data Collection Server property]**.

Per eseguire questa operazione, vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/). Poi vedrai questo. Nel menu a sinistra, fai clic su **[!UICONTROL Datastreams]**.

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxId--`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Cerca il **[!UICONTROL flusso di dati]**, denominato `--demoProfileLdap-- - Demo System Datastream`. Fai clic sul **[!UICONTROL Datastream]** per aprirlo.

![WebSDK](./images/websdk0.png)

Poi vedrai questo. Fare clic su **[!UICONTROL + Aggiungi servizio]**.

![WebSDK](./images/websdk3.png)

Selezionare il servizio **Inoltro eventi**. Verranno visualizzate 2 impostazioni aggiuntive. Selezionare la proprietà Inoltro eventi creata nell&#39;esercizio precedente e denominata `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Quindi seleziona **Sviluppo** in **Ambiente**. Fai clic su **Salva**.

![WebSDK](./images/websdk4.png)

Lo stream di dati è stato aggiornato ed è pronto per l’utilizzo.

![WebSDK](./images/websdk8a.png)

Lo stream di dati è ora pronto per funzionare con **[!DNL Event Forwarding property]**.

Passaggio successivo: [2.5.3 Crea e configura un webhook personalizzato](./ex3.md)

[Torna al modulo 2.5](./aep-data-collection-ssf.md)

[Torna a tutti i moduli](./../../../overview.md)
