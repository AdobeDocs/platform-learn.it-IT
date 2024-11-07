---
title: 'Query Service: esplora il set di dati con Power BI'
description: 'Query Service: esplora il set di dati con Power BI'
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 5.1.5 Servizio query e Power BI

Aprire Microsoft Power BI Desktop.

![start-power-bi.png](./images/start-power-bi.png)

Fare clic su **Ottieni dati**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Cerca **postgres** (1), seleziona **Postgres** (2) dall&#39;elenco e **Connect** (3).

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Vai a Adobe Experience Platform, **Query** e **Credenziali**.

![query-service-credentials.png](./images/query-service-credentials.png)

Dalla pagina **Credenziali** in Adobe Experience Platform, copiare l&#39;**Host** e incollarlo nel campo **Server**, copiare il **Database** e incollarlo nel campo **Database** in PowerBI, quindi fare clic su OK (2).

>[!IMPORTANT]
>
>Assicurarsi di includere la porta **:80** alla fine del valore Server perché il servizio query non utilizza attualmente la porta PostgreSQL predefinita di 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

Nella finestra di dialogo successiva compila il nome utente e la password con il nome utente e la password trovati nelle **credenziali** delle query in Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

Nella finestra di dialogo Navigator, inserisci **LDAP** nel campo di ricerca (1) per individuare i set di dati CTAS e seleziona la casella accanto a ciascuno (2). Quindi fare clic su Carica (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Assicurarsi che la scheda **Report** (1) sia selezionata.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Seleziona la mappa (1) e, dopo che è stata aggiunta all’area di lavoro per i rapporti, ingrandisci la mappa (2).

![power-bi-select-map.png](./images/power-bi-select-map.png)

Ora è necessario definire le misure e le dimensioni. A tale scopo, trascina i campi dalla sezione **fields** ai segnaposto corrispondenti (che si trovano in **visualizations**) come indicato di seguito:

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Come misura utilizzeremo un conteggio di **customerId**. Trascina il campo **crmid** dalla sezione **fields** nel segnaposto **Size**:

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

Infine, per eseguire alcune analisi di **callTopic**, trascina il campo **callTopic** sul segnaposto **Filtri a livello di pagina** (potrebbe essere necessario scorrere la sezione **visualizzazioni**);

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

Seleziona/deseleziona **argomentiChiamata** per analizzare:

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Hai terminato questo esercizio.

Passaggio successivo: [5.1.7 API servizio query](./ex7.md)

[Torna al modulo 5.1](./query-service.md)

[Torna a tutti i moduli](../../../overview.md)
