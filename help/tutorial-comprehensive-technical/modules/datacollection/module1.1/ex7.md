---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Requisiti dello schema XDM in Adobe Experience Platform
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e dell’estensione Web SDK - Requisiti dello schema XDM in Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 3fc4a1d6-4130-464e-98c0-5b9cac8051a0
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Requisiti dello schema XDM 1.1.7 in Adobe Experience Platform

Affinché il Web SDK possa acquisire i dati in Adobe Experience Platform, è necessario che un mixin XDM specifico faccia parte dello schema XDM in Adobe Experience Platform.

Vai a [https://experience.adobe.com/platform](https://experience.adobe.com/platform) e accedi.

![Debugger AEP](./images/exp1.png)

Dopo aver effettuato l&#39;accesso, seleziona la sandbox appropriata facendo clic sul testo **Production Prod** nella riga blu nella parte superiore dello schermo. Selezionare la sandbox `--aepSandboxName--`.

Dopo aver selezionato la sandbox, la schermata cambia e ora sei nella sandbox.

![Debugger AEP](./images/exp2.png)

Nel menu a sinistra, vai a **Schemi** e apri lo schema **Sistema demo - Schema evento per il sito Web (Global v1.1)**.

![Debugger AEP](./images/exp3.png)

In tale schema, vedrai che il gruppo di campi **AEP Web SDK ExperienceEvent** è stato aggiunto. Questo gruppo di campi aggiunge allo schema tutti i campi obbligatori minimi. Ogni schema Experience Event in Adobe Experience Platform che verrà utilizzato da Web SDK richiederà sempre che quel gruppo di campi faccia parte dello schema.

![Debugger AEP](./images/exp4.png)

Nel [modulo 1.2](./../module1.2/data-ingestion.md) verrà illustrato come aggiungere gruppi di campi agli schemi.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 1.1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../../overview.md)
