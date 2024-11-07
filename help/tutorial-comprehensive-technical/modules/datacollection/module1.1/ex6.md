---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 1.1.6 Implementare Adobe Target

## 1.1.6.1 Aggiornare lo stream di dati per utilizzare Adobe Target

Se desideri inviare ad Adobe Target i dati raccolti da Web SDK e ottenere una risposta da Adobe Target con un’esperienza personalizzata per ogni cliente, segui la procedura riportata di seguito.

Vai a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e vai a **Datastreams**.

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxId--`. Apri lo stream di dati specifico, denominato `--demoProfileLdap-- - Demo System Datastream`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Poi vedrai questo. Per abilitare Adobe Target, fare clic su **+Aggiungi servizio**.

![Debugger AEP](./images/aa2.png)

Poi vedrai questo. Seleziona il servizio **Adobe Target**, dopo il quale puoi facoltativamente fornire ulteriori informazioni. Al momento non è necessario salvarlo, quindi fai clic su **Annulla**.

![Debugger AEP](./images/at1.png)

Passaggio successivo: [requisiti dello schema XDM 1.1.7 in Adobe Experience Platform](./ex7.md)

[Torna al modulo 1.1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../../overview.md)
