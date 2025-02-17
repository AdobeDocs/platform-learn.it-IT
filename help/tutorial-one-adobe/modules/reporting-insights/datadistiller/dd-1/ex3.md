---
title: 'Query Service: utilizzo di Query Service'
description: 'Query Service: utilizzo di Query Service'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: ce04fa00-0247-4693-ba60-efc1746b9fec
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 2.1.3 Utilizzo di Query Service

## Finalità

- Trovare ed esplorare i set di dati
- Scopri come gestire oggetti e attributi di Experience Data Models nelle query

## Contesto

Questo video illustra come utilizzare PSQL per recuperare informazioni sui set di dati disponibili, come scrivere query per Experience Data Model (XDM) e come scrivere le prime semplici query di reporting utilizzando i set di dati Query Service e Citi Signal.

## Query di base

In questo corso scoprirai i metodi per recuperare informazioni sui set di dati disponibili e come recuperare correttamente i dati con una query da un set di dati XDM.

Tutti i set di dati esplorati tramite Adobe Experience Platform all’inizio del 1 sono disponibili per l’accesso tramite un’interfaccia SQL come tabelle. Per elencare tali tabelle è possibile utilizzare il comando **show tables;**.

Eseguire `show tables;` nell&#39;interfaccia della riga di comando **PSQL**. (non dimenticare di terminare il comando con un punto e virgola).

Copiare il comando `show tables;` e incollarlo al prompt:

![prompt dei comandi-show-tables.png](./images/commandpromptshowtables.png)

Vedrai il seguente risultato:

```text
tech-insiders:all=> show tables;
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset                  :
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset   
```

Premere due punti sulla barra spaziatrice per visualizzare la pagina successiva del set di risultati oppure immettere `q` per tornare al prompt dei comandi.

Ogni set di dati in AEP ha la corrispondente tabella di Query Service. Puoi trovare la tabella di un set di dati tramite l’interfaccia utente Set di dati:

![ui-dataset-tablename.png](./images/uidatasettablename.png)

La tabella `demo_system_event_dataset_for_website_global_v1_1` è la tabella di Query Service che corrisponde al set di dati `Demo System - Event Schema for Website (Global v1.1)`.

Per eseguire una query su alcune informazioni sulla posizione in cui è stato visualizzato un prodotto, verranno selezionate le informazioni **geo**.

Copiare la query seguente e incollarla al prompt nell&#39;interfaccia della riga di comando **PSQL** e premere Invio:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Nei risultati della query, noterai che le colonne nel Experience Data Model (XDM) possono essere tipi complessi e non solo scalari. Nella query precedente vogliamo identificare le posizioni geografiche in cui si è verificato un **commerce.productViews**. Per identificare un **commerce.productViews** è necessario navigare nel modello XDM utilizzando **.Notazione** (punto).

```text
tech-insiders:all=> select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
                 geo                  
--------------------------------------
 ("(51.59119,-1.407848)",Charlton,GB)
(1 row)
```

Il risultato è un oggetto piatto anziché un singolo valore? L&#39;oggetto **placecontext.geo** contiene quattro attributi: schema, paese e città. Quando un oggetto viene dichiarato come colonna, restituisce l’intero oggetto come stringa. Lo schema XDM può essere più complesso di quello che conosci, ma è molto potente ed è stato progettato per supportare molte soluzioni, canali e casi d’uso.

Per selezionare le singole proprietà di un oggetto, utilizzare **.Notazione** (punto).

Copia l&#39;istruzione seguente e incollala al prompt nell&#39;interfaccia della riga di comando **PSQL**:

```sql
select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Il risultato della query di cui sopra deve essere simile al seguente.
Il risultato è ora un insieme di valori semplici:

```text
tech-insiders:all=> select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude | latitude |   city   | countrycode 
-----------+----------+----------+-------------
 -1.407848 | 51.59119 | Charlton | GB
(1 row)
```

Non preoccuparti, c&#39;è un modo semplice per ottenere il percorso verso una proprietà specifica. Nella parte seguente verrà illustrato come.

Sarà necessario modificare una query, quindi apriamo prima un editor.

In Windows: utilizzare **Blocco note**

Su Mac: installa l’app Editor di testo desiderata e aprila.

Copia l’istruzione seguente nell’editor di testo:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Torna all&#39;interfaccia utente di Adobe Experience Platform (dovrebbe essere aperta nel browser) o passa a [Adobe Experience Platform](https://experience.adobe.com/platform).

Seleziona **Schemi**, immetti `Demo System - Event Schema for Website` nel campo **cerca** e fai clic per aprire lo schema `Demo System - Event Schema for Website (Global v1.1) Schema`.

![browse-schema.png](./images/browseschema.png)

Esplora il modello XDM per **Demo System - Event Schema for Website (Global v1.1)**, facendo clic su un oggetto. Espandere la struttura per **placecontext**, **geo** e **schema**. Quando selezioni l&#39;attributo effettivo **longitude**, visualizzerai il percorso completo nella casella rossa evidenziata. Per copiare il percorso dell&#39;attributo, fare clic sull&#39;icona Copia percorso.

![esplora-schema-per-percorso.png](./images/exploreschemaforpath.png)

Passa al blocco note/parentesi quadre e rimuovi **il percorso_attributo_qui** dalla prima riga. Posiziona il cursore dopo **select** sulla prima riga e incolla (CTRL-V).

![esplora-schema-per-percorso.png](./images/exploreschemaforpath1.png)

Copiare l&#39;istruzione modificata e incollarla al prompt nell&#39;interfaccia della riga di comando **PSQL** e premere Invio.

Il risultato dovrebbe essere simile al seguente:

```text
tech-insiders:all=> select placeContext.geo._schema.longitude
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude 
-----------
 -1.407848
(1 row)
```

## Passaggi successivi

Vai a [2.1.4 Query, query, query e analisi dell&#39;abbandono](./ex4.md){target="_blank"}

Torna a [Servizio query](./query-service.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
