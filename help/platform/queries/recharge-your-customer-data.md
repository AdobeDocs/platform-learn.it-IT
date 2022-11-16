---
title: Ricarica i dati dei clienti per offrire esperienze elettrizzanti
description: Scopri come mitigare l’impatto di dati di bassa qualità, ridurre il tempo a valore e moltiplicare il ROI utilizzando gli stessi dati per diversi casi d’uso.
role: Data Engineer, Data Architect, Developer
feature: Queries
kt: 10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# Ricarica i dati dei clienti per offrire esperienze elettrizzanti

I dati Omnichannel sono un ingrediente fondamentale per abilitare i profili cliente utilizzabili dagli esperti di marketing per orchestrare l’attivazione e misurare i percorsi di clienti risultanti. Tuttavia, le aziende devono affrontare problemi nella gestione della qualità, della scala e della varietà di questi dati. Richiedono soluzioni semplificate per mitigare l&#39;impatto di dati di bassa qualità, ridurre il tempo a valore e moltiplicare il ROI utilizzando gli stessi dati per molti casi d&#39;uso.

Questo video esplora:

* Funzionalità di preparazione dei dati Adobe Experience Platform che puoi sfruttare
* Aumento del ROI da Adobe Real-Time CDP, Adobe Journey Optimizer e Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Esempio SQL

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

Per ulteriori informazioni, visita il [Documentazione del servizio query](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=it).

>[!NOTE]
>
>Questo video è un estratto della sessione Adobe Summit 2020 *[Ricarica dei dati Omnichannel per l&#39;elettrificazione delle esperienze](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
