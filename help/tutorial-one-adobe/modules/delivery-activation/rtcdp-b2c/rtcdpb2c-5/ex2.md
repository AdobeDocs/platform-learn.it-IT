---
title: 'Raccolta dati di Adobe Experience Platform e inoltro lato server in tempo reale: aggiorna lo stream di dati per rendere disponibili i dati per la proprietà Server di raccolta dati di Adobe Experience Platform'
description: Aggiorna lo stream di dati per rendere i dati disponibili per la proprietà del server di raccolta dati di Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: f4bb0673-d553-4027-8bfd-53d2608efaf5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# 2.5.2 Aggiorna lo stream di dati per rendere i dati disponibili per la proprietà Adobe Experience Platform Data Collection Server

## Aggiornare lo stream di dati

In [Guida introduttiva](./../../../getting-started/gettingstarted/ex2.md), hai creato il tuo **[!UICONTROL Datastream]**. È stato quindi utilizzato il nome `--aepUserLdap-- - Demo System Datastream`.

In questo esercizio, devi configurare **[!UICONTROL Datastream]** in modo che funzioni con la proprietà **Data Collection Server**.

Per eseguire questa operazione, vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/). Poi vedrai questo. Nel menu a sinistra, fai clic su **[!UICONTROL Datastreams]**.

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Cerca il **[!UICONTROL flusso di dati]**, denominato `--aepUserLdap-- - Demo System Datastream`. Fai clic sul **[!UICONTROL Datastream]** per aprirlo.

![WebSDK](./images/websdk0.png)

Poi vedrai questo. Fare clic su **[!UICONTROL + Aggiungi servizio]**.

![WebSDK](./images/websdk3.png)

Selezionare il servizio **Inoltro eventi**. Verranno visualizzate 2 impostazioni aggiuntive. Selezionare la proprietà Inoltro eventi creata nell&#39;esercizio precedente e denominata `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Quindi seleziona **Sviluppo** in **Ambiente**. Fai clic su **Salva**.

![WebSDK](./images/websdk4.png)

Lo stream di dati è stato aggiornato ed è pronto per l’utilizzo.

![WebSDK](./images/websdk8a.png)

Lo stream di dati è ora pronto per funzionare con **[!DNL Event Forwarding property]**.

## Passaggi successivi

Vai a [2.5.3 Crea e configura un webhook personalizzato](./ex3.md){target="_blank"}

Torna a [Connessioni Real-Time CDP: Inoltro eventi](./aep-data-collection-ssf.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
