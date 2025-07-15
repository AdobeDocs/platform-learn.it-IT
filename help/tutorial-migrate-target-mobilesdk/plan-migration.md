---
title: 'Pianificare la migrazione: esegui la migrazione dell’implementazione Adobe Target nell’app mobile all’estensione Offer Decisioning e Target'
description: Scopri le differenze principali tra at.js e Platform Web SDK e come pianificare le attività di migrazione.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Pianificare la migrazione

Il livello di impegno per la migrazione dall’estensione Target all’estensione Offer Decisioning e Target dipende dalla complessità dell’implementazione corrente e delle funzioni di Target utilizzate.

Indipendentemente dalla semplicità o dalla complessità dell’implementazione, è importante comprendere appieno lo stato corrente prima di eseguire la migrazione. Questa guida ti aiuta a suddividere i componenti dell’implementazione corrente e a sviluppare un piano gestibile per migrare ogni elemento.

Il processo di migrazione prevede i seguenti passaggi chiave:

1. Valuta l’implementazione corrente e determina un approccio alla migrazione
1. Configurare i componenti iniziali per la connessione a Adobe Experience Platform Edge Network
1. Aggiornare l’implementazione di base per sostituire l’estensione Target con l’estensione Offer Decisioning e Target
1. Migliora l’implementazione Ottimizza SDK per casi d’uso specifici. Questo può comportare il passaggio di parametri aggiuntivi, l’utilizzo di token di risposta e altro ancora.
1. Aggiornare oggetti nell’interfaccia di Target, ad esempio script di profilo, attività e definizioni di pubblico
1. Convalida l’implementazione finale prima di effettuare il passaggio nell’app di produzione

>[!INFO]
>
>Nell’ecosistema di Adobe Experience Platform Mobile SDK, le estensioni vengono implementate dagli SDK importati nelle applicazioni che possono avere nomi diversi:
>
> * **Target SDK** implementa l&#39;estensione **Adobe Target**
> * **Ottimizza SDK** implementa l&#39;estensione **Offer Decisioning e Target**


Quindi, controlla il [confronto dettagliato tra l&#39;estensione Target e l&#39;estensione Offer Decisioning e Target](detailed-comparison.md) per comprendere meglio le differenze tecniche e identificare le aree che richiedono un&#39;attenzione aggiuntiva.

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target per dispositivi mobili dall’estensione Target all’estensione Offer Decisioning e Target. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
