---
title: Raccolta dati Adobe Experience Platform e inoltro lato server in tempo reale - Aggiorna il tuo Datastream per rendere i dati disponibili per la proprietà Adobe Experience Platform Data Collection Server
description: Aggiornare il Datastream per rendere i dati disponibili per la proprietà Adobe Experience Platform Data Collection Server
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 0c42350c-c38a-410e-bdab-41aff6024f81
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 14.2 Aggiornare il Datastream per rendere i dati disponibili per la proprietà Adobe Experience Platform Data Collection Server

## 14.2.1 Aggiorna il tuo Datastream

In [Esercizio 0.2](./../../modules/module0/ex2.md), hai creato il tuo **[!UICONTROL Datastream]**. Hai quindi utilizzato il nome `--demoProfileLdap-- - Demo System Datastream`.

In questo esercizio, devi configurare che **[!UICONTROL Datastream]** per lavorare con **[!DNL Data Collection Server property]**.

Per farlo, vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Vedrete questo. Nel menu a sinistra, fai clic su **[!UICONTROL Datastreams]**.

Nell’angolo in alto a destra dello schermo, seleziona il nome della sandbox, che deve essere `--aepSandboxId--`.

![Fai clic sull’icona Configurazione bordo nella barra di navigazione a sinistra](./images/edgeconfig1b.png)

Cerca il tuo **[!UICONTROL Datastream]**, denominato `--demoProfileLdap-- - Demo System Datastream`. Fai clic su **[!UICONTROL Datastream]** per aprirlo.

![WebSDK](./images/websdk0.png)

Vedrete questo. Fai clic su **[!UICONTROL + Aggiungi servizio]**.

![WebSDK](./images/websdk3.png)

Selezionare il servizio **Inoltro eventi**. Verranno visualizzate 2 impostazioni aggiuntive. Selezionare la proprietà Event Forwarding, creata nell&#39;esercizio precedente e denominata `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Quindi seleziona **Sviluppo** sotto **Ambiente**. Fai clic su **Salva**.

![WebSDK](./images/websdk4.png)

Il datastream è stato aggiornato ed è pronto per l’uso.

![WebSDK](./images/websdk8a.png)

Il tuo datastream è ora pronto per lavorare con il tuo **[!DNL Event Forwarding property]**.

Passaggio successivo: [14.3 Creare e configurare un webhook personalizzato](./ex3.md)

[Torna al modulo 14](./aep-data-collection-ssf.md)

[Torna a tutti i moduli](./../../overview.md)
