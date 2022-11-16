---
title: Servizio query - Power BI/Tableau
description: Servizio query - Power BI/Tableau
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 11525d05-1c19-4d41-8f47-4feb3e8aed66
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 4.4 Generare un set di dati da una query

## Oggetto

Scopri come generare set di dati dai risultati delle query Connetti Microsoft Power BI Desktop/Tableau direttamente al servizio Query Creazione di un report in Microsoft Power BI Desktop/Tableau Desktop

## Contesto della lezione

Un&#39;interfaccia a riga di comando per la query dei dati è emozionante ma non è ben presente. In questa lezione, ti guideremo attraverso un flusso di lavoro consigliato per come utilizzare Microsoft Power BI Desktop/Tableau direttamente il servizio Query per creare rapporti visivi per le tue parti interessate.

## 4.4.1 Creare un set di dati da una query SQL

La complessità della query influisce sul tempo necessario per la restituzione dei risultati da parte del servizio query. E quando esegui query direttamente dalla riga di comando o da altre soluzioni come Microsoft Power BI/Tableau, il servizio Query è configurato con un timeout di 5 minuti (600 secondi). E in alcuni casi queste soluzioni saranno configurate con timeout più brevi. Per eseguire query più grandi e caricare in anticipo il tempo necessario per restituire i risultati, offriamo una funzione per generare un set di dati dai risultati della query. Questa funzione utilizza la funzione SQL standard nota come Crea tabella come selezione (CTAS). È disponibile nell’interfaccia utente di Platform dall’elenco query e può essere eseguito direttamente dalla riga di comando con PSQL.

Nel precedente hai sostituito **immetti il tuo nome** con il proprio ldap prima di eseguirlo in PSQL.

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

Passa all’interfaccia utente di Adobe Experience Platform - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

Cerca l’istruzione eseguita nell’interfaccia utente di Adobe Experience Platform Query immettendo ldap nel campo di ricerca:

Seleziona **Query**, vai a **Registro** e inserisci il tuo ldap nel campo di ricerca.

![search-query-for-ctas.png](./images/search-query-for-ctas.png)

Seleziona la query e fai clic su **Set di dati di output**.

![search-query-for-ctas.png](./images/search-query-for-ctasa.png)

Invio `--demoProfileLdap-- Callcenter Interaction Analysis` come nome e descrizione del set di dati e premi il **Esegui query** pulsante

![create-ctas-dataset.png](./images/create-ctas-dataset.png)

Di conseguenza, verrà visualizzata una nuova query con uno stato **Inviato**.

![ctas-query-submit.png](./images/ctas-query-submitted.png)

Al termine, verrà visualizzata una nuova voce per **Set di dati creato** (potrebbe essere necessario aggiornare la pagina).

![ctas-dataset-created.png](./images/ctas-dataset-created.png)

Non appena viene creato il set di dati (che può richiedere 5-10 minuti), puoi continuare l’esercizio.

Passaggio successivo - Opzione A: [4.5 Query Service e Power BI](./ex5.md)

Passaggio successivo - Opzione B: [4.6 Query Service e Tableau](./ex6.md)

[Torna al modulo 4](./query-service.md)

[Torna a tutti i moduli](../../overview.md)
