---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 475e9a34-c80e-41e4-9660-61c79f26922d
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

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

Passaggio successivo: [requisiti dello schema XDM 1.1.7 in Adobe Experience Platform](./ex7.md)

[Torna al modulo 1.1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../../overview.md)
