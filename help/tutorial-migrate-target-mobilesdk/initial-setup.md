---
title: Configurazione iniziale - Migrazione da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning Mobile
description: Scopri e imposta gli importanti elementi fondamentali necessari per l’implementazione di Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 6%

---

# Eseguire l’impostazione iniziale della raccolta dati

La migrazione da Target SDK a Optimize SDK richiede una configurazione iniziale per abilitare l’acquisizione dati, le funzioni e le caratteristiche corrette di Optimize SDK. Prima di apportare qualsiasi modifica all’implementazione del sito web, è necessario completare i seguenti passaggi:

- [Configurare le autorizzazioni appropriate](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} in Adobe Admin Console per la raccolta dati
- [Configura uno schema XDM](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} per il passaggio di dati strutturati ad Edge Network
- [Configura lo schema](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} per ricevere i dati di Adobe Target
- [Configura uno spazio dei nomi delle identità](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} per la personalizzazione tra dispositivi e la funzionalità mbox3rdPartyId
- [Crea uno stream di dati](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} per abilitare l&#39;inoltro di dati da Edge Network
- [Configura lo stream di dati](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} per abilitare l&#39;inoltro di dati ad Adobe Target
- [Configura la proprietà tag](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} per l&#39;estensione Decisioning

## Configurazione dell&#39;estensione

>[!BEGINTABS]

>[!TAB Estensione Decisioning]

Estensioni di tag installate quando si utilizza l’estensione Decisioning:

1. Adobe Journey Optimizer - Decisioning
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Profilo
1. Consenso
1. Identità
1. AEP Assurance (facoltativo, necessario per il debug)

![Estensioni tag installate quando si utilizza l&#39;estensione Decisioning](assets/tag-extensions-decisioning.png)

>[!TAB Estensione Target]

Estensioni di tag installate quando si utilizza l’estensione Target:

1. Adobe Target
1. Mobile Core
1. Profilo
1. Adobe Analytics (facoltativo, necessario se si utilizza Adobe Analytics come origine per la generazione di rapporti per le attività di Adobe Target)

![Estensioni tag installate quando si utilizza l&#39;estensione Target](assets/tag-extensions-target.png)

>[!ENDTABS]

## Configurazione dello stream di dati

L&#39;estensione Target dispone di [impostazioni configurabili](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) che con l&#39;estensione Decision sono [configurate nello stream di dati](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup).

| Estensione Target | Estensione Decisioning | Note |
| --- | --- | --- | 
| Codice client | n/d | Impostato automaticamente dal bordo utilizzando i dettagli dell’organizzazione IMS |
| ID ambiente | ID ambiente di destinazione | Configurato nello stream di dati |
| Target Workspace, proprietà | Token proprietà | Configurato nello stream di dati |
| Timeout | Non configurabile | Il timeout con l’estensione Decisioning è di 10 secondi |
| Dominio server | Dominio Edge Network | Impostato nell’estensione Adobe Experience Platform Edge Network |

Quindi, scopri come [sostituire SDK](replace-sdk.md) di Target.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
