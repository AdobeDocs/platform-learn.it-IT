---
title: Servizio query - Esplora il set di dati con Power BI
description: Servizio query - Esplora il set di dati con Power BI
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 0f9e6719-056b-4858-8c86-04b3beaa950e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 4.5 Query Service e Power BI

Apri Microsoft Power BI Desktop.

![start-power-bi.png](./images/start-power-bi.png)

Fai clic su **Ottieni dati**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Cerca **poster** (1), seleziona **Postgres** (2) dall&#39;elenco e **Connetti** (3)

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Vai a Adobe Experience Platform, a **Query** e **Credenziali**.

![query-service-credentials.png](./images/query-service-credentials.png)

Da **Credenziali** in Adobe Experience Platform, copia la **Host** e incollalo nel **Server** e copia il **Database** e incollalo nel **Database** in PowerBI, quindi fare clic su OK (2).

>[!IMPORTANT]
>
>Assicurati di includere la porta **:80** alla fine del valore del server perché il servizio query non utilizza attualmente la porta PostgreSQL predefinita 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

Nella finestra di dialogo successiva, compila il nome utente e la password con il nome utente e la password che si trovano in **Credenziali** di query in Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

Nella finestra di dialogo Navigatore, inserisci il tuo **LDAP** nel campo di ricerca (1) per individuare i set di dati CTAS e selezionare la casella accanto a ciascuno (2). Quindi fare clic su Carica (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Assicurati che **Rapporto** (1) è selezionata.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Seleziona la mappa (1) e, una volta aggiunta all’area di reporting, ingrandisci la mappa (2).

![power-bi-select-map.png](./images/power-bi-select-map.png)

Ora è necessario definire le misure e le dimensioni, a tale scopo è necessario trascinare i campi dal **field** sezione sui segnaposto corrispondenti (situato sotto **visualizzazioni**) come indicato di seguito:

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Come misura utilizzeremo un conteggio di **customerId**. Trascina **briciolo** dal campo **field** nella sezione **Dimensione** segnaposto:

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

Infine, per fare un po&#39; **callTopic** analisi, trascina il **callTopic** sul campo **Filtri a livello di pagina** segnaposto (potrebbe essere necessario scorrere nel **visualizzazioni** sezione);

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

Seleziona/deseleziona **callTopics** per indagare:

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Ora avete finito questo esercizio.

Passaggio successivo: [API del servizio query 4.7](./ex7.md)

[Torna al modulo 4](./query-service.md)

[Torna a tutti i moduli](../../overview.md)
