---
title: Foundation - Configurazione di Adobe Experience Platform Data Collection e estensione Web SDK - Spiegazione della raccolta dati Adobe Experience Platform
description: Foundation - Configurazione di Adobe Experience Platform Data Collection e estensione Web SDK - Spiegazione della raccolta dati Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: f498bb8c-659c-44b4-bb2e-36ea14640773
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 5%

---

# 1.1 Informazioni sulla raccolta dati di Adobe Experience Platform

## Contesto

La raccolta dati di Adobe Experience Platform viene utilizzata dai marchi per diversi casi d’uso. Si tratta di un sistema Tag Management di nuova generazione (TMS) che offre ai clienti un modo semplice di implementare e gestire tutte le soluzioni di analisi, marketing e pubblicità necessarie per fornire ai clienti esperienze personalizzate. Non esiste alcun costo aggiuntivo per la raccolta dati di Adobe Experience Platform ed è disponibile per qualsiasi cliente Adobe Experience Cloud. Un marchio può utilizzare Adobe Experience Platform Data Collection per:

- Implementa le applicazioni Adobe Experience Cloud e Adobe Experience Platform.
- Gestire i diversi requisiti delle diverse parti dell&#39;organizzazione fornendo a ognuna di esse un proprio **Proprietà** da gestire.
- Consente il test e la gestione del ciclo di vita.
- Inserisci tag JavaScript personalizzati e di terze parti, tutti gestiti in un’unica posizione.

## Esplorare l’interfaccia utente

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/#/data-collection/).

Vai a **Tag**. Ora vedi il **[!UICONTROL Proprietà]** visualizza. Le proprietà elencate di seguito sono per la gestione delle esercitazioni. Queste proprietà rappresentano..

- Proprietà app e web
- Siti web diversi che servono i clienti in modi diversi. Ad esempio, se la vendita al dettaglio Luma ha una proprietà, la destinazione Luma Travel ne avrà un’altra
- Siti web legacy e attuali
- Una progettazione Adobe Analytics specifica comune a più siti web diversi
- Pagine Intranet interne e siti esterni

![Visualizzazione delle proprietà di Launch](./images/launch1.png)

Ora, guardate la barra a sinistra.

![Avvia barra a sinistra](./images/launch2.png)

- **[!UICONTROL Tag]** offre una panoramica di tutte le proprietà lato client
- **[!UICONTROL Superfici app]** fornisce una panoramica di tutte le configurazioni dell’app per abilitare le notifiche push (utilizzate/abilitate in combinazione con Project Sierra)
- **[!UICONTROL Datastreams]** sono esplorate nella [esercizio successivo](./ex2.md)
- **[!UICONTROL Inoltro eventi]** offre una panoramica di tutte le proprietà lato server esplorate in [Modulo 14 - Connessioni Real-Time CDP: Inoltro eventi](../module14/aep-data-collection-ssf.md)

## Ulteriori informazioni

Adobe Experience Platform Data Collection è uno strumento molto avanzato che ha un ambito superiore a un tutorial Adobe Experience Platform. Le organizzazioni potrebbero non utilizzare la raccolta dati di Adobe Experience Platform per le proprie funzionalità di gestione dei tag, ma utilizzare soluzioni di gestione dei tag non di Adobe per inserire codice e gestire tag. L’utilizzo di una soluzione di gestione tag non Adobe è supportato da Adobe e Adobe Professional Services.
Di seguito sono riportate ulteriori informazioni per chi è interessato a comprendere la raccolta dati di Adobe Experience Platform.

- [Guida utente alla raccolta dati di Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)
- [Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it)
- [Configurare le autorizzazioni utente](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [Documentazione API](https://developer.adobelaunch.com/api/)

Passaggio successivo: [1.2 Rete Edge, Datastreams e raccolta dati lato server](./ex2.md)

[Torna al modulo 1](./data-ingestion-launch-web-sdk.md)

[Torna a tutti i moduli](./../../overview.md)
