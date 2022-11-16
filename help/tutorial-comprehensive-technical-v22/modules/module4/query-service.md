---
title: Servizio query
description: Servizio query
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 74943e52-8a7e-4db7-9407-7deeab008fa7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---

# 4. Servizio query

**Autori: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

In questo modulo, otterrai un’anteprima pratica di Adobe Experience Platform Query Service. Query Service consente di eseguire query omnicanale in tutti i dati dell’applicazione Adobe Experience Cloud, unendo e analizzando i dati in Adobe Campaign, Analytics, Audience Manager, Target e Advertising Cloud e altri dati cliente caricati/inseriti in Adobe Experience Platform.

Query Service è uno strumento senza server. Supporta le query SQL e la connettività da più applicazioni client tramite la sua compatibilità PostgreSQL.
Useremo i dati che sono stati inseriti nella piattaforma utilizzando i dati di interazione web, le interazioni con i call center in combinazione con i dati di fedeltà cliente caricati nella piattaforma.

## Finalità di apprendimento

- Acquisisci familiarità con l’interfaccia utente di Adobe Experience Platform
- Connettiti a Query Service ed esegui le query SQL
- Esplorare i set di dati in Adobe Experience Platform
- Collegare Tableau o Power BI al servizio query Adobe Experience Platform per creare visualizzazioni e rapporti

## Prerequisiti

- Una certa familiarità con SQL è preferita, ma non obbligatoria
- Accesso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Set di dati (set di dati utilizzato durante il laboratorio, precaricato)
- PostgreSQL
- Tableau o Microsoft Power BI Desktop
- **Scarica queste risorse**:
   - [JSON - Dati di esempio: Interazioni sito web](./../../assets/json/ee.json)
   - [JSON - Dati di esempio: Interazioni con il call center](./../../assets/json/callcenter.json)
   - [JSON - Dati di esempio: Fedeltà](./../../assets/json/loyalty.json)

>[!IMPORTANT]
>
>Questa esercitazione è stata creata per facilitare un particolare formato del workshop. Utilizza sistemi e account specifici a cui potresti non avere accesso. Anche senza accesso, pensiamo che si possa ancora imparare molto leggendo attraverso questo contenuto molto dettagliato. Se partecipi a uno dei workshop e hai bisogno delle tue credenziali di accesso, contatta il tuo rappresentante di Adobe che ti fornirà le informazioni richieste.

## Panoramica dell’architettura

Scopri l’architettura riportata di seguito, che evidenzia i componenti che verranno discussi e utilizzati in questo modulo.

![Panoramica dell’architettura](../../assets/images/architecturem7.png)

## Sandbox da utilizzare

Per questo modulo, utilizza questa sandbox: `--module7sandbox--`.

>[!NOTE]
>
>Non dimenticare di installare, configurare e utilizzare l’estensione Chrome come riferimento in [0.1 - Installare l’estensione Chrome per la documentazione di Experience League](../module0/ex1.md)

## Esercizi

[Prerequisiti per 4.0](./ex0.md)

Sarà necessario installare PSQL per eseguire le query in questo esercizio di abilitazione. A seconda del sistema operativo, sarà necessario installare Microsoft Power BI o Tableau. Gli utenti Windows possono scegliere tra Power BI o Tableau. Gli utenti di Mac dovrebbero installare Tableau.

[4.1 Guida introduttiva](./ex1.md)

In questo esercizio esplorerai l’interfaccia utente di Adobe Experience Platform Query Service, saprai di più sui set di dati, troverai le query e infine imposterai una connessione da PSQL.

[4.2 Utilizzo del servizio Query](./ex2.md)

In questo esercizio imparerai la sintassi di base del servizio query e potrai identificare gli attributi dello schema XDM nella query.

[4.3 Query, query, query... e analisi di abbandono](./ex3.md)

In questo esercizio si esegue una query, si apprenderà delle funzioni definite dall&#39;Adobe mentre si esegue un&#39;analisi di abbandono. Alla fine di questo, scriverai una query per preparare un set di dati da utilizzare in Microsoft Power BI.

[4.4 Generare un set di dati da una query](./ex4.md)

In questo esercizio genererai un set di dati da una query eseguita nel precedente e utilizzerai questo set di dati negli esercizi successivi.

[4.5 Query Service e Power BI](./ex5.md)

In questo esercizio, connetterai Power BI a Adobe Experience Platform e Query Service per eseguire l’analisi dell’interazione con Callcenter.

[4.6 Query Service e Tableau](./ex6.md)

In questo esercizio, connetterai Tableau a Adobe Experience Platform e Query Service per eseguire l’analisi dell’interazione con Callcenter.

[API del servizio query 4.7](./ex7.md)

In questo esercizio utilizzerai l’API del servizio query per gestire i modelli di query e le pianificazioni delle query.

[Riepilogo e vantaggi](./summary.md)

Riepilogo di questo modulo e panoramica dei vantaggi.

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;imparare tutto quello che c&#39;è da sapere su Adobe Experience Platform. Se hai domande, vuoi condividere feedback generali su suggerimenti su contenuti futuri, contatta direttamente Wouter Van Geluwe, inviando un&#39;e-mail a **vangeluw@adobe.com**.

[Torna a tutti i moduli](../../overview.md)
