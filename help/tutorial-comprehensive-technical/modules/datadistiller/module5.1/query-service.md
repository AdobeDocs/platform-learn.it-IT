---
title: Query Service
description: Query Service
kt: 5342
doc-type: tutorial
exl-id: 6eb65de3-d0e8-49d4-a702-5c9d6a1952b7
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 5.1 Servizio query

In questo modulo, riceverai un’anteprima pratica di Adobe Experience Platform Query Service. Query Service consente di eseguire query omnicanale su tutti i dati dell’applicazione Adobe Experience Cloud, unendo e analizzando i dati in Adobe Campaign, Analytics, Audience Manager, Target e Advertising Cloud e altri dati dei clienti caricati/inseriti in Adobe Experience Platform.

Query Service è uno strumento senza server. Supporta le query SQL e la connettività da più applicazioni client tramite la compatibilità PostgreSQL.
Utilizzeremo i dati che sono stati inseriti in Platform utilizzando i dati di interazione web, le interazioni con i call center in combinazione con i dati sulla fedeltà dei clienti caricati in Platform.

## Finalità di apprendimento

- Acquisisci familiarità con l’interfaccia utente di Adobe Experience Platform
- Connessione a Query Service ed esecuzione delle query SQL
- Esplorare i set di dati in Adobe Experience Platform
- Connettere Tableau o Power BI a Adobe Experience Platform Query Service per creare visualizzazioni e rapporti

## Prerequisiti

- È preferibile acquisire una certa familiarità con SQL, ma non è necessario
- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Set di dati (set di dati utilizzati durante il laboratorio, precaricati per te)
- PostgreSQL
- Tableau o Microsoft Power BI Desktop
- **Scarica queste risorse**:
   - [JSON - Dati di esempio: interazioni con il sito web](./../../../assets/json/ee.json)
   - [JSON - Dati di esempio: interazioni con il call center](./../../../assets/json/callcenter.json)
   - [JSON - Dati di esempio: fedeltà](./../../../assets/json/loyalty.json)

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l&#39;estensione Chrome come indicato in [Installare l&#39;estensione Chrome per la documentazione di Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Esercizi

[5.1.1 Prerequisiti](./ex1.md)

Per eseguire le query in questo esercizio di abilitazione, è necessario installare PSQL. A seconda del sistema operativo in uso, è necessario installare Microsoft Power BI o Tableau. Gli utenti possono scegliere tra Power BI o Tableau. Gli utenti di Mac devono installare Tableau.

[5.1.2 Guida introduttiva](./ex2.md)

In questo esercizio verrà esplorata l&#39;interfaccia utente di Adobe Experience Platform Query Service, verranno fornite informazioni sui set di dati, verranno individuate le query e infine verrà impostata una connessione da PSQL.

[5.1.3 Utilizzo di Query Service](./ex3.md)

In questo esercizio imparerai a conoscere la sintassi di base di Query Service e potrai identificare gli attributi dello schema XDM nella query.

[5.1.4 Query, query, query... e analisi dell’abbandono](./ex4.md)

In questo esercizio eseguirete delle query e apprenderete le funzioni definite dall&#39;Adobe durante l&#39;analisi dell&#39;abbandono. Al termine di questo processo, scriverai una query per preparare un set di dati da utilizzare in Microsoft Power BI.

[5.1.5 Generare un set di dati da una query](./ex5.md)

In questo esercizio genererai un set di dati da una query eseguita in precedenza e utilizzerai questo set di dati negli esercizi successivi.

[5.1.6 Servizio query e Power BI](./ex6.md)

In questo esercizio, collegherai Power BI a Adobe Experience Platform e Query Service per eseguire l’analisi dell’interazione del callcenter.

[5.1.7 Query Service e Tableau](./ex7.md)

In questo esercizio collegherai Tableau a Adobe Experience Platform e Query Service per eseguire l’analisi dell’interazione del callcenter.

[5.1.8 API Query Service](./ex8.md)

In questo esercizio utilizzerai l’API Query Service per gestire i modelli di query e le pianificazioni delle query.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all&#39;apprendimento di tutto ciò che c&#39;è da sapere su Adobe Experience Platform e sulle sue applicazioni. Se hai domande, vuoi condividere feedback generali su suggerimenti in merito a contenuti futuri, contatta direttamente Tech Insiders, inviando un&#39;e-mail a **techinsiders@adobe.com**.

[Torna a tutti i moduli](../../../overview.md)
