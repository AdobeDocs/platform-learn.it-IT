---
title: Query Service - Prerequisiti
description: Query Service - Prerequisiti
kt: 5342
doc-type: tutorial
exl-id: e9e4d478-cb8d-42a9-87a3-319e5a8b8522
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# 2.1.1 Prerequisiti

## Installare l&#39;utilità della riga di comando PSQL

Seguire le istruzioni descritte nella documentazione di Adobe Experience Platform per installare il client psql:
[Guida all&#39;installazione di PSQL](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=it)

Dopo aver installato PSQL, potrebbe essere necessario aggiornare **PATH** eseguendo il comando seguente in una finestra del terminale:

Per macOS (sostituire XX nel comando seguente con il numero di versione di PSQL installato):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Installare Power BI

Solo per utenti Windows

[Installa Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=it)

Assicurarsi di installare la versione esatta di **npgsql** come indicato nel documento, altrimenti non sarà possibile connettere Power BI a Adobe Experience Platform Query Service.

## Installare Tableau

Per utenti di Windows o Mac

[Installa Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=it) come da documentazione.

Tableau offre automaticamente un periodo di prova di 14 giorni.

Se desideri utilizzare Tableau oltre questi 14 giorni, ti servirà una chiave di licenza.

## Passaggi successivi

Vai a [2.1.2 Guida introduttiva](./ex2.md){target="_blank"}

Torna a [Servizio query](./query-service.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
