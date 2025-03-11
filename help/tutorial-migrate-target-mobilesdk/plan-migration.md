---
title: 'Pianificare la migrazione: migrazione dell’implementazione Adobe Target nell’app mobile a Adobe Journey Optimizer - Estensione Decisioning'
description: Scopri le differenze principali tra at.js e Platform Web SDK e come pianificare le attività di migrazione.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Pianificare la migrazione

Il livello di impegno per la migrazione dall’estensione Target all’estensione Decisioning dipende dalla complessità dell’implementazione corrente e delle funzioni di Target utilizzate.

Indipendentemente dalla semplicità o dalla complessità dell’implementazione, è importante comprendere appieno lo stato corrente prima di eseguire la migrazione. Questa guida ti aiuta a suddividere i componenti dell’implementazione corrente e a sviluppare un piano gestibile per migrare ogni elemento.

Il processo di migrazione prevede i seguenti passaggi chiave:

1. Valuta l’implementazione corrente e determina un approccio alla migrazione
1. Configurare i componenti iniziali per la connessione a Adobe Experience Platform Edge Network
1. Aggiorna l’implementazione fondamentale per sostituire l’estensione Target con l’estensione Decisioning
1. Migliora l’implementazione Ottimizza SDK per casi d’uso specifici. Questo può comportare il passaggio di parametri aggiuntivi, l’utilizzo di token di risposta e altro ancora.
1. Aggiornare oggetti nell’interfaccia di Target, ad esempio script di profilo, attività e definizioni di pubblico
1. Convalida l’implementazione finale prima di effettuare il passaggio nell’app di produzione

>[!INFO]
>
>Nell’ecosistema di Adobe Experience Platform Mobile SDK, le estensioni vengono implementate dagli SDK importati nelle applicazioni che possono avere nomi diversi:
>
> * **Target SDK** implementa l&#39;estensione **Adobe Target**
> * **Ottimizza SDK** implementa l&#39;estensione **Adobe Journey Optimizer - Decisioning**


Rivedi quindi il confronto dettagliato [tra l&#39;estensione Target e l&#39;estensione Decisioning](detailed-comparison.md) per comprendere meglio le differenze tecniche e identificare le aree che richiedono un&#39;attenzione aggiuntiva.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
