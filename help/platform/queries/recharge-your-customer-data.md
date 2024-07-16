---
title: Ricarica i dati dei tuoi clienti per offrire esperienze elettrizzanti
description: Scopri come mitigare l’impatto di dati di bassa qualità, ridurre il time-to-value e moltiplicare il ROI utilizzando gli stessi dati per molti casi d’uso.
feature: Queries
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Ricarica i dati dei tuoi clienti per offrire esperienze elettrizzanti

I dati omni-channel sono un componente fondamentale per abilitare i profili dei clienti actionable utilizzati dagli esperti di marketing per orchestrare l’attivazione e misurare i percorsi dei clienti risultanti. Tuttavia, le organizzazioni devono affrontare problemi nella gestione della qualità, della scala e della varietà di questi dati. Richiedono soluzioni semplificate per mitigare l’impatto di dati di bassa qualità, ridurre il time-to-value e moltiplicare il ROI utilizzando gli stessi dati per molti casi d’uso.
Per ulteriori informazioni, visitare la [documentazione di Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=it).

Questo video illustra:

* Funzionalità di preparazione dei dati di Adobe Experience Platform che puoi sfruttare
* Aumento del ROI da Adobe Real-Time CDP, Adobe Journey Optimizer e Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/342533?learn=on)

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

>[!NOTE]
>
>Questo video è un estratto della sessione Adobe Summit 2020 *[Ricarica dei dati omnichannel per elettrificare le esperienze](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
