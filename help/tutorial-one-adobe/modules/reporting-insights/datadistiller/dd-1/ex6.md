---
title: 'Query Service: esplora il set di dati con Power BI'
description: 'Query Service: esplora il set di dati con Power BI'
kt: 5342
doc-type: tutorial
exl-id: f1125d91-2fe6-456c-9d4a-802e3f288fc0
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 2.1.6 Query Service e Power BI

Aprire Microsoft Power BI Desktop.

![start-power-bi.png](./images/startpowerbi.png)

Fare clic su **Ottieni dati**.

![power-bi-get-data.png](./images/powerbigetdata.png)

Cerca **postgres** (1), seleziona **Postgres** (2) dall&#39;elenco e **Connect** (3).

![power-bi-connect-progress.png](./images/powerbiconnectprogress.png)

Vai a Adobe Experience Platform, **Query** e **Credenziali**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Dalla pagina **Credenziali** in Adobe Experience Platform, copiare l&#39;**Host** e incollarlo nel campo **Server**, copiare il **Database** e incollarlo nel campo **Database** in PowerBI, quindi fare clic su OK (2).

>[!IMPORTANT]
>
>Assicurarsi di includere la porta **:80** alla fine del valore Server perché il servizio query non utilizza attualmente la porta PostgreSQL predefinita di 5432.

![power-bi-connect-server.png](./images/powerbiconnectserver.png)

Nella finestra di dialogo successiva compila il nome utente e la password con il nome utente e la password trovati nelle **credenziali** delle query in Adobe Experience Platform.

![query-service-credentials.png](./images/queryservicecredentials.png)

Nella finestra di dialogo Navigator, inserisci **LDAP** nel campo di ricerca (1) per individuare i set di dati CTAS e seleziona la casella accanto a ciascuno (2). Quindi fare clic su Carica (3).

![power-bi-load-churn-data.png](./images/powerbiloadchurndata.png)

Assicurarsi che la scheda **Report** (1) sia selezionata.

![power-bi-report-tab.png](./images/powerbireporttab.png)

Seleziona la mappa (1) e, dopo che è stata aggiunta all’area di lavoro per i rapporti, ingrandisci la mappa (2).

![power-bi-select-map.png](./images/powerbiselectmap.png)

Ora è necessario definire le misure e le dimensioni. A tale scopo, trascina i campi dalla sezione **fields** ai segnaposto corrispondenti (che si trovano in **visualizations**) come indicato di seguito:

![power-bi-drag-lat-lon.png](./images/powerbidraglatlon.png)

Come misura utilizzeremo un conteggio di **customerId**. Trascina il campo **crmid** dalla sezione **fields** nel segnaposto **Size**:

![power-bi-drag-crmid.png](./images/powerbidragcrmid.png)

Infine, per eseguire alcune analisi di **callTopic**, trascina il campo **callTopic** sul segnaposto **Filtri a livello di pagina** (potrebbe essere necessario scorrere la sezione **visualizzazioni**);

![power-bi-drag-calltopic.png](./images/powerbidragcalltopic.png)

Seleziona/deseleziona **argomentiChiamata** per analizzare:

![power-bi-report-select-calltopic.png](./images/powerbireportselectcalltopic.png)

Hai terminato questo esercizio.

## Passaggi successivi

Vai a [2.1.8 API servizio query](./ex8.md){target="_blank"}

Torna a [Servizio query](./query-service.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
