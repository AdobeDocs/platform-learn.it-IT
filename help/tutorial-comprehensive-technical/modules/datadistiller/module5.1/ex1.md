---
title: Query Service - Prerequisiti
description: Query Service - Prerequisiti
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 5.1.1 Prerequisiti

## Installare l&#39;utilità della riga di comando PSQL

Seguire le istruzioni descritte nella documentazione di Adobe Experience Platform per installare il client psql:
[Guida all&#39;installazione di PSQL](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html)

Dopo aver installato PSQL, potrebbe essere necessario aggiornare **PATH** eseguendo il comando seguente in una finestra del terminale:

Per macOS (sostituire XX nel comando seguente con il numero di versione di PSQL installato):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Installa Power BI

Solo per utenti Windows

[Installa Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html)

Assicurarsi di installare la versione esatta di **npgsql** come indicato nel documento, altrimenti non sarà possibile connettere Power BI a Adobe Experience Platform Query Service.

## Installare Tableau

Per utenti di Windows o Mac

[Installa Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html) come da documentazione.

Tableau offre automaticamente un periodo di prova di 14 giorni.

Se desideri utilizzare Tableau oltre questi 14 giorni, ti servirà una chiave di licenza.

Passaggio successivo: [5.1.2 Guida introduttiva](./ex2.md)

[Torna al modulo 5.1](./query-service.md)

[Torna a tutti i moduli](../../../overview.md)
