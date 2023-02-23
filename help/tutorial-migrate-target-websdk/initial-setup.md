---
title: Configurazione iniziale | Migrare Target da at.js 2.x all’SDK per web
description: Scopri e configura gli importanti elementi fondamentali necessari per l’implementazione dell’SDK per web di Platform
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 2%

---

# Eseguire la configurazione iniziale della raccolta dati

La migrazione da at.js a Platform Web SDK richiede una configurazione iniziale per abilitare l’acquisizione dei dati, le funzioni e le funzioni corrette di Platform Web SDK. I seguenti passaggi dal [Esercitazione sull’implementazione di Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it) devono essere completate prima che vengano apportate modifiche all’implementazione del sito web:

- [Configurare le autorizzazioni appropriate](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target="_blank"} in Adobe Admin Console per la raccolta dati
- [Configurare uno schema XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} per la trasmissione di dati strutturati a Edge Network
- [Configurare uno spazio dei nomi di identità](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} per la personalizzazione tra dispositivi e la funzionalità mbox3rdPartyId
- [Creare un datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} per abilitare l’inoltro di dati da Edge Network
- [Configurare il datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} per abilitare l’inoltro di dati ad Adobe Target

>[!CAUTION]
>
>Tieni presente che questi aspetti di progettazione devono essere coordinati tra Target, Analytics e le migrazioni di Audienci Manager.

Una volta completata la configurazione iniziale, la funzionalità di Target deve essere abilitata tramite Adobe Experience Platform Edge Network.

Quindi, scopri come [sostituisci la libreria at.js e configura un’implementazione SDK web di base per Platform](replace-library.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
