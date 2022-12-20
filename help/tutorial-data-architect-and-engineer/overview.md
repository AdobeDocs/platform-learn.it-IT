---
title: Guida introduttiva di Adobe Experience Platform per architetti di dati e data engineer
description: Guida introduttiva a Adobe Experience Platform per architetti di dati e data engineer.
breadcrumb-title: Panoramica
role: Data Architect, Data Engineer
kt: 4348
thumbnail: 4348-overview.jpg
recommendations: catalog, noDisplay
exl-id: fabbc591-840b-40dc-89af-305626a16338
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# Guida introduttiva di Adobe Experience Platform per architetti di dati e data engineer

<!--5min-->

_Guida introduttiva di Adobe Experience Platform per architetti di dati e data engineer_ è il punto di partenza perfetto per ottenere l&#39;Experience Platform.


<!--How do we address ETL-->

## Finalità di apprendimento

Gli architetti di dati e gli ingegneri di dati devono collaborare strettamente per una distribuzione di Experience Platform di successo. Questa esercitazione pratica illustra le attività chiave eseguite da _entrambi i ruoli_ quindi sai come iniziare a implementare Platform per la tua attività. Seguirai gli esercizi per conoscere la terminologia chiave, le funzioni, l’interfaccia e l’API di Experience Platform. Anche i clienti di applicazioni Adobe Experience Cloud come Real-time Customer Data Platform, Customer Journey Analytics e Journey Optimizer troveranno questi contenuti utili, in quanto i servizi Platform sono fondamentali per queste applicazioni.

![L’architettura di marketing Adobe Experience Cloud evidenzia i servizi Platform coperti da questa esercitazione: identità, profilo, segmentazione, acquisizione, query e governance](assets/marketecture.png)

Gli argomenti includono:

* Configurazione delle autorizzazioni utente
* Creazione di sandbox
* Configurazione di un progetto Developer Console e utilizzo dell’API Platform
* Gestione dei dati: creazione di schemi, set di dati, identità, criteri di unione e governance dei dati
* Acquisizione dati tramite modalità batch e streaming
* Acquisizione di dati web con Adobe Experience Platform Web SDK
* Creazione di profili cliente in tempo reale
* Utilizzo del servizio Query per convalidare i dati ed estrarre i dati
* Creazione di segmenti

## Scenario aziendale

Adobe Experience Platform è una piattaforma tecnica progettata per aiutarti a raggiungere gli obiettivi di marketing. I casi d&#39;uso aziendali dovrebbero guidare la progettazione e l&#39;implementazione della tecnologia. Questa esercitazione si concentra su un brand fittizio al dettaglio denominato Luma. Luma gestisce negozi di mattoni in diversi paesi e ha anche una presenza online con un sito web e app mobili. Investono in Adobe Experience Platform per combinare i dati di acquisto fedeltà, CRM, web e offline in profili cliente in tempo reale e attivare questi profili per portare il loro marketing al livello successivo. Gli obiettivi aziendali di Luma possono essere allineati o meno con gli obiettivi della tua azienda, ma dovresti essere in grado di mettere in relazione i passaggi pratici di questa esercitazione con gli obiettivi aziendali.

## Prerequisiti

* Hai completato il [Introduzione al corso Adobe Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-U-1-2020.1) ad Experience League e conoscono le funzionalità di Platform
* Puoi accedere a un account con provisioning di Adobe Experience Platform (o a un’applicazione basata su Platform come Real-Time CDP o Journey Optimizer) e alla raccolta dati (precedentemente Launch).
* Sei un amministratore di sistema di tale account o puoi averne uno [configurare le autorizzazioni utente](configure-permissions.md) per te.

## Utilizzo di questa esercitazione

Questa esercitazione combina le attività sia per i data engineer che per gli architetti di dati. Poiché si tratta di un’esercitazione di livello introduttivo, dovresti essere in grado di completare le attività per entrambi i ruoli. Poiché molte delle lezioni si basano su ciò che è stato implementato nelle lezioni precedenti, dovresti procedere nelle lezioni in ordine. Chiederò quali lezioni possono essere saltate.

Durante questa esercitazione, puoi creare vari elementi di Platform, cercando di attenermi ai nomi che ti consiglio il più possibile. Tuttavia, è possibile personalizzare alcuni nomi di elementi di alto livello nel caso in cui più persone nell’organizzazione utilizzino questa esercitazione contemporaneamente. Ad esempio, potrebbe essere utile denominare la sandbox Platform &quot;Luma Tutorial Platform - Ignatius J Reilly&quot; invece di semplicemente &quot;Luma Tutorial Platform&quot;.

Se ti trovi bloccato, prova prima a leggere di nuovo le istruzioni e poi utilizza il ![Segnala un problema](https://experienceleague.adobe.com/assets/img/feedback.svg) link sulla barra laterale di ogni pagina per contattarmi.

## Note tecniche

### Ambienti sandbox

Nell’esercitazione, creerai un ambiente sandbox e lo utilizzerai per completare gli esercizi. L&#39;ambiente sandbox ti consente di completare gli esercizi e l&#39;esperimento senza essere preoccupato di compromettere i tuoi dati di produzione.

### API

Platform è la prima API integrata. Sebbene esistano flussi di lavoro di interfaccia per tutti i principali flussi di lavoro di Platform e vengano utilizzati principalmente, l’esercitazione contiene alcuni esercizi orientati alle API. Ti guiderò attraverso la configurazione del progetto di base nella console Adobe Developer e ti fornirò [!DNL Postman] ambienti e raccolte per iniziare a utilizzare l’API Platform. Dopo aver completato l’esercitazione, potrebbe essere utile acquisire familiarità con l’API Platform e utilizzarla nella propria implementazione.

### Tecnologie di terze parti

Anche se utilizzerai più tecnologie in questa esercitazione, rimarrete quasi interamente nell’ecosistema di Adobe. Con la tua implementazione Platform, probabilmente integrerai Platform con specifiche tecnologie di terze parti. Per mantenere questa esercitazione rilevante per tutti i clienti, utilizzeremo un’implementazione più generica.

Passiamo ora alla prima lezione:[configurare le autorizzazioni](configure-permissions.md).
