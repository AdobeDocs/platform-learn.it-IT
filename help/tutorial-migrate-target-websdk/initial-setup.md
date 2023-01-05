---
title: Configurazione iniziale | Migrare Target da at.js 2.x all’SDK per web
description: Scopri e configura gli importanti elementi fondamentali necessari per l’implementazione dell’SDK per web di Platform
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# Eseguire la configurazione iniziale della raccolta dati

La migrazione da at.js a Platform Web SDK richiede una configurazione iniziale per abilitare l’acquisizione dei dati, le funzioni e le funzioni corrette di Platform Web SDK. I seguenti passaggi dal [Esercitazione sull’implementazione di Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it) devono essere completate prima che vengano apportate modifiche all’implementazione del sito web:

- [Configurare le autorizzazioni appropriate](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target=&quot;_blank&quot;} in Adobe Admin Console for Data Collection
- [Configurare uno schema XDM](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target=&quot;_blank&quot;} per la trasmissione di dati strutturati alla rete Edge
- [Configurare uno spazio dei nomi di identità](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target=&quot;_blank&quot;} per la personalizzazione tra dispositivi e la funzionalità mbox3rdPartyId
- [Creare un datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target=&quot;_blank&quot;} per abilitare l&#39;inoltro di dati da Edge Network
- [Configurare il datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target=&quot;_blank&quot;} per abilitare l&#39;inoltro dei dati ad Adobe Target

>[!CAUTION]
>
>Tieni presente che questi aspetti di progettazione dell’SDK web devono essere coordinati tra Target, Analytics e le migrazioni di Audience Manager.

Una volta completata la configurazione iniziale, la funzionalità di Target deve essere abilitata tramite Adobe Experience Platform Edge Network.

Quindi, scopri come [sostituisci la libreria at.js e configura un’implementazione SDK web di base per Platform](replace-library.md).

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
