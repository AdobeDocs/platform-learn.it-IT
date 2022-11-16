---
title: Servizio query - Utilizzo del servizio query
description: Servizio query - Utilizzo del servizio query
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dbf19991-cb09-43cf-887c-52996dfd2986
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 4.2 Utilizzo del servizio Query

## Oggetto

- Trovare ed esplorare i set di dati
- Scopri come risolvere gli oggetti e gli attributi dei modelli di dati Experience nelle query

## Contesto

In questo documento viene illustrato come utilizzare PSQL per recuperare informazioni sui set di dati disponibili, come scrivere query per Experience Data Model (XDM) e scrivere le prime semplici query di reporting utilizzando i set di dati Query Service e Citi Signal.

## 4.2.1 Query di base

In questo documento vengono fornite informazioni sui metodi per recuperare informazioni sui set di dati disponibili e su come recuperare correttamente i dati con una query da un set di dati XDM.

Tutti i set di dati esplorati tramite Adobe Experience Platform all’inizio di 1 sono disponibili anche per l’accesso tramite un’interfaccia SQL come tabelle. Per elencare le tabelle è possibile utilizzare **mostra tabelle;** comando.

Esegui **mostra tabelle;** nel tuo **Interfaccia della riga di comando PSQL**. (non dimenticare di terminare il comando con un punto e virgola).

Copia il comando **mostra tabelle;** e incollalo al prompt:

![prompt dei comandi-show-tables.png](./images/command-prompt-show-tables.png)

Vedrai il seguente risultato:

```text
aepenablementfy21:all=> show tables;
                            name                            |        dataSetId         |                            dataSet                             | description | resolved 
------------------------------------------------------------+--------------------------+----------------------------------------------------------------+-------------+----------
 demo_system_event_dataset_for_call_center_global_v1_1      | 5fd1a9dea30603194baeea43 | Demo System - Event Dataset for Call Center (Global v1.1)      |             | false
 demo_system_event_dataset_for_mobile_app_global_v1_1       | 5fd1a9de250e4f194bec84cd | Demo System - Event Dataset for Mobile App (Global v1.1)       |             | false
 demo_system_event_dataset_for_voice_assistants_global_v1_1 | 5fd1a9de49ee76194b85f73c | Demo System - Event Dataset for Voice Assistants (Global v1.1) |             | false
 demo_system_event_dataset_for_website_global_v1_1          | 5fd1a9dee3224d194cdfe786 | Demo System - Event Dataset for Website (Global v1.1)          |             | false
 demo_system_profile_dataset_for_loyalty_global_v1_1        | 5fd1a9de250e4f194bec84cc | Demo System - Profile Dataset for Loyalty (Global v1.1)        |             | false
 demo_system_profile_dataset_for_ml_predictions_global_v1_1 | 5fd1a9de241f58194b0cb117 | Demo System - Profile Dataset for ML Predictions (Global v1.1) |             | false
 demo_system_profile_dataset_for_mobile_app_global_v1_1     | 5fd1a9deddf353194a2e00b7 | Demo System - Profile Dataset for Mobile App (Global v1.1)     |             | false
 demo_system_profile_dataset_for_website_global_v1_1        | 5fd1a9de42a61c194dd7b810 | Demo System - Profile Dataset for Website (Global v1.1)        |             | false
 journey_step_events                                        | 5fd1a7f30268c5194bbb7e5e | Journey Step Events                                            |             | false
```

Premere i due punti nella barra spaziatrice per visualizzare la pagina successiva del set di risultati oppure immettere `q` per ripristinare il prompt dei comandi.

Ogni set di dati in Platform ha la tabella corrispondente del servizio query. Puoi trovare la tabella di un set di dati tramite l’interfaccia utente Datasets :

![ui-dataset-Tablename.png](./images/ui-dataset-tablename.png)

La `demo_system_event_dataset_for_website_global_v1_1` la tabella Query Service corrispondente alla `Demo System - Event Schema for Website (Global v1.1)` set di dati.

Per richiedere alcune informazioni sulla posizione di visualizzazione di un prodotto, selezioneremo la **geo** informazioni.

Copia l’istruzione sottostante e incollala al prompt nel **Interfaccia della riga di comando PSQL** e premi invio:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Nel risultato della query, noterai che le colonne in Experience Data Model (XDM) possono essere tipi complessi e non solo tipi scalari. Nella query precedente si desidera identificare le geolocalità in cui un **commerce.productViews** si è verificato. Per identificare un **commerce.productViews** dobbiamo navigare nel modello XDM utilizzando **.** (punto) notazione.

```text
aepenablementfy21:all=> select placecontext.geo
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
                  geo                   
----------------------------------------
 ("(57.4694803,-3.1269422)",Tullich,GB)
(1 row)
```

Notare che il risultato è un oggetto piatto anziché un singolo valore? La **segnaposto.geo** l&#39;oggetto contiene quattro attributi: schema, paese e città. E quando un oggetto viene dichiarato come colonna, restituisce l’intero oggetto come stringa. Lo schema XDM può essere più complesso di quello che si conosce, ma è molto potente ed è stato progettato per supportare molte soluzioni, canali e casi di utilizzo.

Per selezionare le singole proprietà di un oggetto, utilizzare la **.** (punto) notazione.

Copia l’istruzione sottostante e incollala al prompt nel **Interfaccia della riga di comando PSQL**:

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

Il risultato della query di cui sopra dovrebbe essere simile al seguente.
Il risultato è ora un set di valori semplici:

```text
aepenablementfy21:all=> select placecontext.geo._schema.longitude
aepenablementfy21:all->       ,placecontext.geo._schema.latitude
aepenablementfy21:all->       ,placecontext.geo.city
aepenablementfy21:all->       ,placecontext.geo.countryCode
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  |  latitude  |  city   | countrycode 
------------+------------+---------+-------------
 -3.1269422 | 57.4694803 | Tullich | GB
(1 row)
```

Non ti preoccupare, c&#39;è un modo semplice per ottenere il percorso verso una proprietà specifica. Nella parte seguente imparerai come.

Dovrai modificare una query, quindi apriamo prima un editor.

Su Windows

Fai clic sul pulsante **ricerca** nella barra degli strumenti di windows, digitare **blocco note** in **ricerca** fai clic sul campo **blocco note** risultato:

![windows-start-blocco note.png](./images/windows-start-notepad.png)

Su Mac

Installa [Parentesi](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) o utilizzare un altro Editor di testo, se non è installato e seguire le istruzioni. Dopo l&#39;installazione, cerca **Parentesi** tramite la ricerca sotto i riflettori di Mac e aprilo.

Copiare la seguente istruzione nel blocco note o tra parentesi:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Torna all’interfaccia utente di Adobe Experience Platform (deve essere aperta nel browser) o passa a [https://platform.adobe.com](https://platform.adobe.com).

Seleziona **Schemi**, inserisci `Demo System - Event Schema for Website (Global v1.1)` in **ricerca** campo e seleziona `Demo System - Event Schema for Website (Global v1.1) Schema` dall&#39;elenco.

![browseschema.png](./images/browse-schema.png)

Esplora il modello XDM per **Sistema demo - Schema evento per sito web (Global v1.1)** facendo clic su un oggetto. Espandi la struttura ad albero per **segnaposto**, **geo** e **schema**. Quando si seleziona l&#39;attributo effettivo **longitudine**, viene visualizzato il percorso completo nella casella rossa evidenziata. Per copiare il percorso dell&#39;attributo, fai clic sull&#39;icona del percorso di copia.

![expl-schema-for-path.png](./images/explore-schema-for-path.png)

Passa al blocco note/staffe e rimuovi **your_attribute_path_here** dalla prima riga. Posiziona il cursore dopo **select** sulla prima riga e incollare (CTRL+V).

Copiare l’istruzione modificata dal blocco note/parentesi e incollarla al prompt in **Interfaccia della riga di comando PSQL** e premi invio.

Il risultato dovrebbe essere simile al seguente:

```text
aepenablementfy21:all=> select placeContext.geo._schema.longitude
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  
------------
 -3.1269422
```

Passaggio successivo: [4.3 Query, query, query... e analisi di abbandono](./ex3.md)

[Torna al modulo 4](./query-service.md)

[Torna a tutti i moduli](../../overview.md)
