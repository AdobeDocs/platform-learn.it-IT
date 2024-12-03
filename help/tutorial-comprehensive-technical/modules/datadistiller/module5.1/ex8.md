---
title: Servizio query - API servizio query
description: Servizio query - API servizio query
kt: 5342
doc-type: tutorial
source-git-commit: 87089d6c9e1096f12193c73ef63d64a498dbc8dd
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 2%

---

# 5.1.8 API Query Service

## Finalità

- Utilizza l’API Query Service per gestire modelli di query e pianificazioni delle query

## Contesto

In questo esercizio eseguirai chiamate API per gestire modelli di query e pianificazioni di query utilizzando una raccolta Postman. Potrai definire modelli di query, eseguire query regolari e query CTAS. Una query **CTAS** (crea tabella come query di selezione) memorizza il set di risultati in un set di dati esplicito. Mentre le query regolari vengono memorizzate in un set di dati implicito (o generato dal sistema), che in genere viene esportato in formato di file parquet.

## Documentazione

- [Guida di Adobe Experience Platform Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html)
- [API servizio query](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## API servizio query

L’API Query Service consente di gestire le query non interattive rispetto al data lake di Adobe Experience Platform.

Non interattivo significa che una richiesta di esecuzione di una query non darà luogo a una risposta immediata. La query verrà elaborata e il relativo set di risultati verrà memorizzato in un set di dati implicito o esplicito (CTAS: create table as select).

## Query di esempio

Come query di esempio si utilizzerà la prima query elencata in [4.3 - Query, query, query... e churn analysis](./ex3.md):

Quante visualizzazioni di prodotto abbiamo su base giornaliera?

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

## Query

Apri Postman sul computer. Come parte del modulo 3, hai creato un ambiente Postman e importato una raccolta Postman. Seguire le istruzioni nell&#39;esercizio [2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md) nel caso in cui non sia stato ancora eseguito.

Come parte della raccolta Postman importata, verrà visualizzata una cartella **3. Servizio query**. Se non vedi questa cartella, scarica di nuovo la [raccolta Postman](./../../../assets/postman/postman_profile.zip) e importa di nuovo la raccolta in Postman come indicato nell&#39;esercizio [2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md).

![QS](./images/pm3.png)

>[!NOTE]
>
>Al momento, solo la cartella **1. Le query** contengono richieste. Altre richieste verranno aggiunte in una fase livello.

Apri tale cartella e scopri le chiamate API di Query Service per eseguire, monitorare e scaricare il set di risultati della query.

Una chiamata POST a [/query/query] con il seguente payload attiverà l&#39;esecuzione della query;

### Crea query

Fai clic sulla richiesta denominata **1.1 QS - Crea query** e passa a **Intestazioni**. A questo punto viene visualizzato quanto segue:

![Segmentazione](./images/s1_call.png)

Concentriamoci su questo campo intestazione:

| Chiave | Valore |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>È necessario specificare il nome della sandbox di Adobe Experience Platform in uso. Il campo intestazione **x-sandbox-name** deve essere `--module7sandbox--`.

Vai alla sezione **Body** di questa richiesta. Nel **Corpo** di questa richiesta, visualizzerai quanto segue:

![Segmentazione](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

Attenzione: aggiornare la variabile **name** nella richiesta seguente sostituendo **ldap** con il **ldap** specifico.

Dopo aver aggiunto il tuo **ldap** specifico, il corpo dovrebbe essere simile al seguente:

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>La chiave **dbName** nel corpo JSON precedente fa riferimento alla sandbox utilizzata nell&#39;istanza di Adobe Experience Platform. Se utilizzi la sandbox di PROD, il dbName deve essere **prod:all**, se utilizzi un&#39;altra sandbox come, ad esempio, **module7**, il dbName deve essere uguale a **module7:all**.

Fai clic sul pulsante blu **Invia** per creare il segmento e visualizzarne i risultati.

![Segmentazione](./images/s1_bodydtl_results.png)

In caso di esito positivo, la richiesta POST restituirà la seguente risposta:

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 0,
    "updated": "2021-01-20T13:23:13.951Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

Il **stato** corrente della query è **INVIATO**. Una volta eseguito, lo stato diventerà **COMPLETATO**.

Puoi anche cercare le query inviate tramite l&#39;interfaccia utente di Adobe Experience Platform, aprire [Adobe Experience Platform](https://experience.adobe.com/#/@experienceplatform/platform/home), passare a **Query**, **Registro** e selezionare la query:

![Segmentazione](./images/s1_bodydtl_results_qs.png)

### Ottieni query

Fai clic sulla richiesta denominata **1.2 QS - Ottieni query** e passa a **Intestazioni**. A questo punto viene visualizzato quanto segue:

![Segmentazione](./images/s2_call.png)

Concentriamoci su questo campo intestazione:

| Chiave | Valore |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>È necessario specificare il nome della sandbox di Adobe Experience Platform in uso. Il campo intestazione **x-sandbox-name** deve essere `--module7sandbox--`.

Vai a **Parametri**. A questo punto viene visualizzato quanto segue:

![Segmentazione](./images/s2_call_p.png)

Il parametro **orderby** consente di specificare un ordinamento basato sulla proprietà **created**. Osserva il segno **&#39;-&#39;** prima di creato, il che significa che l&#39;ordine in cui viene restituito l&#39;elenco delle query utilizzerà la data di creazione nell&#39;ordine **decrescente**. La query deve trovarsi all&#39;inizio dell&#39;elenco.

Fai clic sul pulsante blu **Invia** per creare il segmento e visualizzarne i risultati.

![Segmentazione](./images/s2_bodydtl_results.png)

In caso di esito positivo, la richiesta restituirà una risposta simile a quella riportata di seguito. Il **stato** della risposta può essere **INVIATO**, **IN_CORSO** o **COMPLETATO**. Potrebbero essere necessari alcuni minuti prima che la query abbia uno stato **SUCCESS**. Puoi ripetere l&#39;invio di questa richiesta diverse volte, finché non visualizzi lo stato **SUCCESS**.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "module7:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
            "state": "SUCCESS",
            "rowCount": 1,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "elapsedTime": 217481,
            "updated": "2021-01-20T13:26:51.432Z",
            "client": "API",
            "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
            "created": "2021-01-20T13:23:13.951Z",
            "_links": {
                "self": {
                    "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "60080ace62c49a19490c5870",
                        "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
                    }
                ]
            }
        }
     ]
    },
    "version": 1
}
```

Quando lo stato è **SUCCESS**, continuare con la richiesta successiva.

### Ottieni stato query

Fai clic sulla richiesta denominata **1.3 QS - Ottieni stato query** e passa a **Intestazioni**. A questo punto viene visualizzato quanto segue:

![Segmentazione](./images/s3_call.png)

Concentriamoci su questo campo intestazione:

| Chiave | Valore |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>È necessario specificare il nome della sandbox di Adobe Experience Platform in uso. Il campo intestazione **x-sandbox-name** deve essere `--module7sandbox--`.

Fai clic sul pulsante blu **Invia** per creare il segmento e visualizzarne i risultati.

![Segmentazione](./images/s3_bodydtl_results.png)

In caso di esito positivo, la richiesta restituirà una risposta simile a quella riportata di seguito.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUCCESS",
    "rowCount": 1,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 217481,
    "updated": "2021-01-20T13:26:51.432Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "referenced_datasets": [
            {
                "id": "60080ace62c49a19490c5870",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
            }
        ]
    }
}
```

Quando una query raggiunge lo stato **SUCCESS**, la risposta indica anche il numero di righe recuperate dalla query tramite la proprietà **rowCount**. Nel nostro esempio, la query restituisce 10 righe. Vediamo nella sezione successiva come è possibile recuperare le 10 righe.

### Recupera risultati query

La risposta **SUCCESS** precedente include una proprietà **referenced_datasets** che punta al set di dati implicito in cui è memorizzato il risultato della query. Per accedere al risultato, utilizziamo la relativa proprietà **href** o **id**.

Fai clic sulla richiesta denominata **1.4 QS - Ottieni risultato query** e passa a **Intestazioni**. A questo punto viene visualizzato quanto segue:

![Segmentazione](./images/s4_call.png)

Concentriamoci su questo campo intestazione:

| Chiave | Valore |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>È necessario specificare il nome della sandbox di Adobe Experience Platform in uso. Il campo intestazione **x-sandbox-name** deve essere `--module7sandbox--`.

Fai clic sul pulsante blu **Invia** per creare il segmento e visualizzarne i risultati.

![Segmentazione](./images/s4_bodydtl_results.png)

La risposta di questa richiesta punterà ai file del set di dati:

```json
{
    "60080ace62c49a19490c5870": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:enabled"
            ],
            "adobe/siphon/buffered-promotion-recency": [
                "live"
            ],
            "adobe/siphon/use-buffered-promotion": [
                "true"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "aep/siphon/expire-snapshot-timestamp": [
                "1611141272703"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "iceberg"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2021-01-20 10:49:51"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "62cd9f38-8529-4b05-8d9f-388529db0540",
        "lastBatchId": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "version": "1.0.6",
        "created": 1611139790698,
        "updated": 1611149266031,
        "createdClient": "750e24ee855b4ac18ccc4f4817f96ee1",
        "createdUser": "3A260B485E909A170A495E76@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "viewId": "60080ace62c49a19490c5871",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/60080ace62c49a19490c5870/views/60080ace62c49a19490c5871/files",
        "schemaMetadata": {
            "delta": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

>[!NOTE]
>
>Presto verranno aggiunti altri esercizi per aiutarti a interagire con l’API di Query Service.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 5.1](./query-service.md)

[Torna a tutti i moduli](../../../overview.md)
