---
title: Configurazione della base dati relazionali
description: Configurazione della base dati relazionali
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: bf3bebfa3bd79829da5352e950aed3f4ef5bf6d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

---

# 3.8.1 Configurazione della base dati relazionali

Accedi a Adobe Journey Optimizer da [https://experience.adobe.com](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![AJO OC](./images/aechome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`.

![AJO OC](./images/ajohome.png)

## 3.8.1.1 configurazione schema basato su relazioni

Uno schema relazionale è la definizione formale del modello di dati basato su modello.

Specifica:

- Il set di tabelle
- Colonne in ogni tabella
- I vincoli
- Le relazioni tra le tabelle

L’organizzazione di schemi o tabelle in un modello di dati basato su modelli riguarda la strutturazione dei dati in più tabelle. Assicurati che ogni tabella memorizzi un tipo di entità/schemi.

Quando si acquisiscono i dati in per l’utilizzo con le campagne orchestrate di Adobe Journey Optimizer, sono disponibili le seguenti origini:

- Amazon S3
- Google Cloud Storage
- SFTP
- Snowflake
- Google BigQuery
- Data Landing Zone
- Azure Databricks
- Caricamento file locale

Il primo passaggio di questo esercizio è la configurazione degli schemi XDM relazionali. Nel menu a sinistra, scorri verso il basso fino a **Gestione dati** e seleziona **Schemi**. Fare clic su **+ Crea schema**.

![AJO OC](./images/ajoocdata1.png)

Selezionare **Relazionale**.

![AJO OC](./images/ajoocdata2.png)

Selezionare **Carica file DDL**, quindi fare clic su **Scegli file**.

![AJO OC](./images/ajoocdata3.png)

Ora che gli schemi XDM relazionali sono configurati e i dati vengono acquisiti, puoi iniziare a utilizzarli per creare la campagna orchestrata nell’esercizio successivo.

## Acquisizione dati 3.8.1.2


## Passaggi successivi

Vai a [Crea la tua campagna orchestrata](./ex2.md){target="_blank"}

Torna a [Adobe Journey Optimizer: Campagne](./ajocampaigns.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
