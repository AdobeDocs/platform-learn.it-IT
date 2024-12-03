---
title: Servizio query - Power BI/Tableau
description: Servizio query - Power BI/Tableau
kt: 5342
doc-type: tutorial
exl-id: c4e4f5f9-3962-4c8f-978d-059f764eee1c
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 5.1.5 Generare un set di dati da una query

## Finalità

Scopri come generare set di dati dai risultati delle query
Connettere Microsoft Power BI Desktop/Tableau direttamente a Query Service
Creazione di un report in Microsoft Power BI Desktop/Tableau Desktop

## Contesto lezione

L&#39;interfaccia della riga di comando per l&#39;esecuzione di query sui dati è molto interessante, ma non è disponibile. In questa lezione, ti guideremo attraverso un flusso di lavoro consigliato su come utilizzare Microsoft Power BI Desktop/Tableau direttamente da Query Service per creare rapporti visivi per le parti interessate.

## Creare un set di dati da una query SQL

La complessità della query influirà sul tempo necessario affinché il servizio query restituisca i risultati. E quando si esegue una query direttamente dalla riga di comando o da altre soluzioni come Microsoft Power BI/Tableau, Query Service è configurato con un timeout di 5 minuti (600 secondi). E in alcuni casi queste soluzioni saranno configurate con timeout più brevi. Per eseguire query più grandi e caricare in anteprima il tempo necessario per restituire i risultati, è disponibile una funzione che consente di generare un set di dati dai risultati della query. Questa funzione utilizza la funzione SQL standard nota come Create Table As Select (CTAS). È disponibile nell’interfaccia utente di Platform dall’elenco delle query e può essere eseguito direttamente dalla riga di comando con PSQL.

In precedenza hai sostituito **immetti il tuo nome** con il tuo ldap prima di eseguirlo in PSQL.

```sql
select /* enter your name */
       e.--aepTenantId--.identification.core.ecid as ecid,
       e.placeContext.geo.city as city,
       e.placeContext.geo._schema.latitude latitude,
       e.placeContext.geo._schema.longitude longitude,
       e.placeContext.geo.countryCode as countrycode,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling as callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic as callTopic,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled as contractCancelled,
       l.--aepTenantId--.loyaltyDetails.level as loyaltystatus,
       l.--aepTenantId--.loyaltyDetails.points as loyaltypoints,
       l.--aepTenantId--.identification.core.loyaltyId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_loyalty_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

Passa all&#39;interfaccia utente di Adobe Experience Platform - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

Per cercare l’istruzione eseguita nell’interfaccia utente di Adobe Experience Platform Query, immetti il ldap nel campo di ricerca:

Seleziona **Query**, passa a **Registro** e immetti il tuo ldap nel campo di ricerca.

![search-query-for-ctas.png](./images/search-query-for-ctas.png)

Seleziona la query e fai clic su **Set di dati di output**.

![search-query-for-ctas.png](./images/search-query-for-ctasa.png)

Immetti `--aepUserLdap-- Callcenter Interaction Analysis` come nome e descrizione per il set di dati e premi il pulsante **Esegui query**

![create-ctas-dataset.png](./images/create-ctas-dataset.png)

Verrà quindi visualizzata una nuova query con stato **Inviata**.

![ctas-query-mitted.png](./images/ctas-query-submitted.png)

Al termine, verrà visualizzata una nuova voce per **Set di dati creato** (potrebbe essere necessario aggiornare la pagina).

![ctas-dataset-created.png](./images/ctas-dataset-created.png)

Non appena viene creato il set di dati (operazione che può richiedere 5-10 minuti), puoi continuare l’esercizio.

Passaggio successivo - Opzione A: [5.1.6 Query Service e Power BI](./ex6.md)

Passaggio successivo - Opzione B: [5.1.7 Query Service e Tableau](./ex7.md)

[Torna al modulo 5.1](./query-service.md)

[Torna a tutti i moduli](../../../overview.md)
