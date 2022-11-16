---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Requisiti dello schema XDM in Adobe Experience Platform
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Requisiti dello schema XDM in Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 8e17129c-633d-45bd-aa70-78cc3d3a2108
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Requisiti dello schema XDM 1.7 in Adobe Experience Platform

Per garantire che l’SDK web e alloy.js siano in grado di acquisire dati in Adobe Experience Platform, è necessario che un determinato mixin XDM faccia parte dello schema XDM in Adobe Experience Platform.

Vai a [https://experience.adobe.com/platform](https://experience.adobe.com/platform) e accedi.

![Debugger AEP](./images/exp1.png)

Dopo aver effettuato l’accesso, seleziona la sandbox appropriata facendo clic sul testo **Produzione Prod** nella linea blu sopra lo schermo. Selezionare la sandbox `--aepSandboxId--`.

Dopo aver selezionato la sandbox, vedrete la modifica dello schermo e ora siete nella sandbox.

![Debugger AEP](./images/exp2.png)

Nel menu a sinistra, vai a **Schemi** e aprire **Sistema demo - Schema evento per sito web (Global v1.1)** Schema.

![Debugger AEP](./images/exp3.png)

In questo schema, verrà visualizzato il gruppo di campi **Mixin ExperienceEvent SDK per web AEP** è stato aggiunto. Questo gruppo di campi aggiunge tutti i campi minimi richiesti allo schema. Ogni schema evento esperienza in Adobe Experience Platform che verrà utilizzato dall’SDK per web richiederà sempre che il gruppo di campi faccia parte dello schema.

![Debugger AEP](./images/exp4.png)

In [Modulo 2](./../module2/data-ingestion.md) verrà illustrato come aggiungere gruppi di campi agli schemi.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../overview.md)
