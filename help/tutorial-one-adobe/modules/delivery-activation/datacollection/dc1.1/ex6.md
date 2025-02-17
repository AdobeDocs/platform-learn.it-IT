---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---

# 1.1.6 Implementare Adobe Target

## Aggiornare lo stream di dati per utilizzare Adobe Target

Se desideri inviare ad Adobe Target i dati raccolti da Web SDK e ottenere una risposta da Adobe Target con un’esperienza personalizzata per ogni cliente, segui la procedura riportata di seguito.

Vai a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e vai a **Datastreams**.

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`. Apri lo stream di dati specifico, denominato `--aepUserLdap-- - Demo System Datastream`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

Poi vedrai questo. Per abilitare Adobe Target, fare clic su **Aggiungi servizio**.

![Debugger AEP](./images/aa2.png)

Poi vedrai questo. Seleziona il servizio **Adobe Target**, dopo il quale puoi facoltativamente fornire ulteriori informazioni. Fai clic su **Salva**.

![Debugger AEP](./images/at1.png)

## Passaggi successivi

Vai a [1.1.7 Requisiti dello schema XDM in Adobe Experience Platform](./ex7.md){target="_blank"}

Torna a [Configurazione della raccolta dati di Adobe Experience Platform ed estensione tag Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
