---
title: Configurazione iniziale - Migrazione di Target da at.js 2.x a Web SDK
description: Scopri e imposta gli importanti elementi fondamentali necessari per l’implementazione di Platform Web SDK
exl-id: dbf9683b-1cfc-474a-9c38-432cad4d1533
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Eseguire l’impostazione iniziale della raccolta dati

La migrazione da at.js a Platform Web SDK richiede una configurazione iniziale per abilitare l’acquisizione dati, le funzioni e le caratteristiche corrette di Platform Web SDK. Prima di apportare qualsiasi modifica all&#39;implementazione del sito Web, è necessario completare i passaggi seguenti dell&#39;esercitazione sull&#39;implementazione di [Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it):

- [Configurare le autorizzazioni appropriate](https://experienceleague.adobe.com/it/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} in Adobe Admin Console per la raccolta dati
- [Configura uno schema XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html?lang=it){target="_blank"} per il passaggio di dati strutturati all&#39;Edge Network
- [Configura uno spazio dei nomi delle identità](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html?lang=it){target="_blank"} per la personalizzazione tra dispositivi e la funzionalità mbox3rdPartyId
- [Crea un flusso di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html?lang=it){target="_blank"} per abilitare l&#39;inoltro di dati da Edge Network
- [Configura lo stream di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=it#configure-the-datastream){target="_blank"} per abilitare l&#39;inoltro di dati ad Adobe Target

>[!CAUTION]
>
>Ricorda che questi aspetti di progettazione devono essere coordinati tra le migrazioni di Target, Analytics e Audience Manager.

Una volta completata la configurazione iniziale, la funzionalità di Target deve essere abilitata utilizzando l’Edge Network di Adobe Experience Platform.

Successivamente, scopri come [sostituire la libreria at.js e configurare un&#39;implementazione di base di Platform Web SDK](replace-library.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti con la migrazione di Target da at.js a Web SDK. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
