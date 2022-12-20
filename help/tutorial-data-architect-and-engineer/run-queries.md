---
title: Eseguire query
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Eseguire query
description: Questa lezione illustra come impostare, scrivere ed eseguire query per convalidare i dati acquisiti.
role: Data Architect, Data Engineer
feature: Queries
kt: 4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 3%

---

# Eseguire query

<!-- 15 min-->
In questa lezione verrà illustrato come impostare, scrivere ed eseguire query per convalidare i dati acquisiti.

Adobe Experience Platform Query Service consente di comprendere meglio i dati grazie all’utilizzo di SQL standard per eseguire query sui dati in Platform. Utilizzando Query Service, puoi unire qualsiasi set di dati nel Data Lake e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, nell’apprendimento automatico o per l’inserimento nel Profilo cliente in tempo reale.

**Architetti dei dati** e **Ingegneri dati** dovrà utilizzare il servizio di query al di fuori di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sul servizio Query:
>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Autorizzazioni necessarie

In [Configurare le autorizzazioni](configure-permissions.md) per completare la lezione, è necessario impostare tutti i controlli di accesso necessari.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Query semplici

Cominciamo con alcune semplici domande:

1. Nell’interfaccia utente di Platform, passa a **Query** nella navigazione a sinistra
1. Seleziona la **Crea query** pulsante in alto a destra per aprire una casella di testo per eseguire ed eseguire query
1. Inserisci la seguente query nell’editor e premi Maiusc+Invio o Maiusc+Invio per eseguire la query.

   ```
   SHOW TABLES
   ```

1. Viene visualizzato l’elenco delle tabelle disponibili

   ![MOSTRA query TABLE](assets/queries-showTables.png)


1. Ora prova questa query, sostituendo `_techmarketingdemos` con il tuo namespace tenant, che, se ricordi, è visibile negli schemi.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![SELEZIONARE i dati dal set di dati fedeltà](assets/queries-loyaltySelect.png)

1. In caso di errore, nella sezione **[!UICONTROL Console]** scheda , come illustrato di seguito
   ![Errore nella query](assets/queries-error.png)

1. Con la query riuscita, **[!UICONTROL Nome]** it `Luma Gold Level Customers`
1. Seleziona il pulsante **[!UICONTROL Salva]**
   ![Salvataggio della query](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## Esercizi aggiuntivi

Ulteriori esercitazioni del servizio query verranno aggiunte all’esercitazione in una data successiva.
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## Risorse aggiuntive

* [Documentazione del servizio query](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=it)
* [Riferimento API del servizio query](https://www.adobe.io/experience-platform-apis/references/query-service/)

E ora per la lezione finale, [creazione di segmenti](build-segments.md)!
