---
title: Guida introduttiva di Adobe Experience Platform per architetti di dati e data engineer
description: Guida introduttiva di Adobe Experience Platform per architetti di dati e data engineer.
breadcrumb-title: Panoramica
role: Data Architect, Data Engineer
jira: KT-4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: 63987fb652a653283a05a5f35f7ce670127ae905
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Guida introduttiva di Adobe Experience Platform per architetti di dati e data engineer

<!--5min-->

_Guida introduttiva di Adobe Experience Platform per architetti di dati e ingegneri di dati_ è il punto di partenza ideale per iniziare a utilizzare Experience Platform.


<!--How do we address ETL-->

## Finalità di apprendimento

Gli architetti di dati e i data engineer devono collaborare strettamente per una corretta distribuzione degli Experienci Platform. Questa esercitazione pratica illustra le attività chiave eseguite da _entrambi i ruoli_ per consentirti di iniziare a implementare Platform per la tua attività. Sarai guidato attraverso esercizi che ti presenteranno la terminologia chiave, le funzioni, l’interfaccia e le API di Experience Platform. Anche i clienti di applicazioni Adobe Experience Cloud come Real-time Customer Data Platform, Customer Journey Analytics e Journey Optimizer troveranno utili tali contenuti, in quanto i servizi Platform sono fondamentali per tali applicazioni.

![Adobe Experience Cloud marketecture che evidenzia i servizi Platform descritti in questo tutorial: identità, profilo, segmentazione, acquisizione, query e governance](assets/marketecture.png)

Gli argomenti includono:

* Configurazione delle autorizzazioni utente
* Creazione di sandbox
* Configurazione di un progetto Developer Console e utilizzo dell’API della piattaforma
* Gestione dei dati, inclusa la creazione di schemi, set di dati, identità, criteri di unione e governance dei dati
* Acquisizione dei dati utilizzando le modalità batch e streaming
* Acquisizione di dati web con Adobe Experience Platform Web SDK
* Creazione di profili cliente in tempo reale
* Utilizzo di Query Service per convalidare i dati ed estrarli
* Creazione di segmenti

## Scenario di business

Adobe Experience Platform è una piattaforma tecnica progettata per aiutarti a raggiungere gli obiettivi di marketing. I casi d&#39;uso aziendali dovrebbero guidare la progettazione e l&#39;implementazione della tecnologia. Questa esercitazione si concentra su un marchio al dettaglio fittizio denominato Luma. Luma gestisce negozi tradizionali in più paesi e ha anche una presenza online con un sito web e app mobili. Stanno investendo in Adobe Experience Platform per combinare i dati di fidelizzazione, gestione delle relazioni con i clienti, dati di acquisto Web e offline in profili cliente in tempo reale e attivare questi profili per portare il loro marketing a un livello successivo. Gli obiettivi aziendali di Luma possono essere allineati o meno con gli obiettivi della tua azienda, ma dovresti essere in grado di correlare i passaggi pratici di questa esercitazione ai tuoi obiettivi aziendali.

## Prerequisiti

* Hai guardato la [Introduzione alla playlist di Adobe Experience Platform](https://experienceleague.adobe.com/it/playlists/experience-platform-introduction) su Experience League e conosci le funzionalità di Platform
* Hai accesso a un account fornito con Adobe Experience Platform (o un’applicazione basata su Platform come Real-Time CDP o Journey Optimizer) e Data Collection (precedentemente Launch).
* L&#39;utente è un amministratore di sistema dell&#39;account oppure può disporre di un [autorizzazione utente](configure-permissions.md).

## Utilizzo di questa esercitazione

Questa esercitazione combina attività per data engineer e architetti di dati. Trattandosi di un tutorial di livello introduttivo, dovresti essere in grado di completare le attività per entrambi i ruoli. Poiché molte delle lezioni si basano su quanto implementato nelle lezioni precedenti, dovresti procedere attraverso le lezioni in ordine. Vi dirò quali lezioni possono essere saltate.

Mentre crei vari elementi di Platform durante questa esercitazione, cerca di attenersi il più possibile ai nomi che ti consiglio. Tuttavia, esistono alcuni nomi di elementi di alto livello che è possibile personalizzare nel caso in cui più persone dell’organizzazione partecipino contemporaneamente a questa esercitazione. Ad esempio, potrebbe essere utile denominare la sandbox Platform &quot;Luma Tutorial Platform - Ignatius J Reilly&quot; invece di &quot;Luma Tutorial Platform&quot;.

Se ti blocchi, prova a leggere di nuovo le istruzioni, quindi utilizza il collegamento ![Segnala un problema](https://experienceleague.adobe.com/assets/img/feedback.svg?lang=it) nella barra laterale di ogni pagina per contattarmi.

## Note tecniche

### Ambienti sandbox

Nell’esercitazione, creerai un ambiente sandbox e lo utilizzerai per completare gli esercizi. L’ambiente sandbox ti consente di completare in tutta sicurezza gli esercizi e l’esperimento senza preoccuparti di compromettere i dati di produzione.

### API

La piattaforma è stata creata prima in base alle API. Anche se i flussi di lavoro di interfaccia esistono per tutti i principali flussi di lavoro di Platform e verranno utilizzati principalmente, l’esercitazione contiene alcuni esercizi orientati all’API. Ti guiderò attraverso la configurazione del progetto di base in Adobe Developer Console e ti fornirò [!DNL Postman] ambienti e raccolte per iniziare con l&#39;API di Platform. Dopo aver completato l’esercitazione, potrebbe essere utile avere familiarità con l’API di Platform e utilizzarla nella propria distribuzione.

### Tecnologie di terze parti

Anche se in questa esercitazione utilizzerai più tecnologie, rimarrai quasi interamente all’interno dell’ecosistema Adobe. Nella tua implementazione di Platform, probabilmente integrerai Platform con specifiche tecnologie di terze parti. Per mantenere questa esercitazione rilevante per tutti i clienti, utilizzeremo un’implementazione più generica.

## Aggiornamenti tutorial

* Giugno 2023: aggiornato per includere il nuovo flusso di lavoro delle autorizzazioni e per utilizzare le credenziali API server-to-server di OAuth


Passiamo ora alla prima lezione: [configurare le autorizzazioni](configure-permissions.md).
