---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Implementare Adobe Target
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6 Implementare Adobe Target

## 1.6. Aggiorna il tuo Datastream per utilizzare Adobe Target

Se desideri inviare ad Adobe Target i dati raccolti dall’SDK per web e ottenere una risposta da Adobe Target con un’esperienza personalizzata per ogni cliente, segui questi passaggi.

Vai a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) e vai a **Datastreams**.

Nell’angolo in alto a destra dello schermo, seleziona il nome della sandbox, che deve essere `--aepSandboxId--`. Apri il tuo datastream specifico, denominato `--demoProfileLdap-- - Demo System Datastream`.

![Fai clic sull’icona Configurazione bordo nella barra di navigazione a sinistra](./images/edgeconfig1b.png)

Vedrete questo. Per abilitare Adobe Target, fai clic su **+Aggiungi servizio**.

![Debugger AEP](./images/aa2.png)

Vedrete questo. Selezionare il servizio **Adobe Target**, dopo di che puoi facoltativamente fornire ulteriori informazioni. In questo momento, non è necessario salvarlo, quindi fai clic su **Annulla**.

![Debugger AEP](./images/at1.png)

Passaggio successivo: [Requisiti dello schema XDM 1.7 in Adobe Experience Platform](./ex7.md)

[Torna al modulo 1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../overview.md)
