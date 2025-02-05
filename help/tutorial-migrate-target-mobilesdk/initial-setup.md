---
title: Configurazione iniziale - Migrazione da Adobe Target a Adobe Journey Optimizer - Estensione Decisioning Mobile
description: Scopri e imposta gli importanti elementi fondamentali necessari per l’implementazione di Platform Web SDK
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 5%

---

# Eseguire l’impostazione iniziale della raccolta dati

La migrazione da Target SDK a Optimize SDK richiede una configurazione iniziale per abilitare l’acquisizione dati, le funzioni e le caratteristiche corrette di Optimize SDK. Prima di apportare qualsiasi modifica all’implementazione del sito web, è necessario completare i seguenti passaggi:

- [Configurare le autorizzazioni appropriate](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} in Adobe Admin Console per la raccolta dati
- [Configura uno schema XDM](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} per il passaggio di dati strutturati all&#39;Edge Network
- [Configura lo schema](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema) per ricevere i dati di Adobe Target
- [Configura uno spazio dei nomi delle identità](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} per la personalizzazione tra dispositivi e la funzionalità mbox3rdPartyId
- [Crea un flusso di dati](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} per abilitare l&#39;inoltro di dati da Edge Network
- [Configura lo stream di dati](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} per abilitare l&#39;inoltro di dati ad Adobe Target
- [Configura la proprietà tag](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension) per l&#39;estensione Decisioning

>[!BEGINTABS]

>[!TAB Estensione Target]

Estensioni di tag installate quando si utilizza l’estensione Target:

1. Mobile Core
1. Profilo
1. Adobe Target
1. Adobe Analytics (facoltativo, necessario se si utilizza Adobe Analytics come origine per la generazione di rapporti per le attività di Adobe Target)

![Estensioni tag installate quando si utilizza l&#39;estensione Target](assets/tag-extensions-target.png)


>[!TAB Estensione Decisioning]

Estensioni di tag installate quando si utilizza l’estensione Decisioning:

1. Mobile Core
1. Profilo
1. Consenso
1. Identità
1. Adobe Experience Platform Edge Network
1. Adobe Journey Optimizer - Decisioning
1. AEP Assurance (facoltativo, necessario per il debug)

![Estensioni tag installate quando si utilizza l&#39;estensione Decisioning](assets/tag-extensions-decisioning.png)


>[!ENDTABS]

Successivamente, scopri come [sostituire la libreria at.js e configurare un&#39;implementazione di base di Platform Web SDK](replace-library.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
