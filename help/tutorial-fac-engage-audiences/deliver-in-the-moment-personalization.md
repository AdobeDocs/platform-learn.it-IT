---
title: Distribuisci personalizzazione immediata tramite Edge Network
seo-title: Deliver "in-the moment" personalization using Edge Network | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Distribuisci personalizzazione immediata tramite Edge Network
description: In questo esercizio, il pubblico federato viene valutato in Edge per il retargeting immediato e immediato.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
exl-id: 20bfafb1-1d1b-48d8-84eb-97d4c9e03b76
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Distribuisci personalizzazione immediata tramite Edge Network

La Composizione federata del pubblico consente di arricchire i tipi di pubblico esistenti in Adobe Experience Platform (AEP) utilizzando i dati del pubblico composto che sono stati federati dal data warehouse aziendale. Questi dati non verranno mantenuti in Adobe Experience Platform, ma puoi utilizzare le funzionalità di [inoltro eventi](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview){target="_blank"} per inviare questi dati direttamente al data warehouse.

In questo esercizio utilizziamo un pubblico federato interrogato con il punteggio di credito e l’attività di prestito per arricchire il pubblico comportamentale dei visitatori della pagina web della richiesta di prestito.

Valutando questo pubblico su Edge, effettuiamo immediatamente il retargeting dei visitatori della pagina di richiesta di prestito preapprovata con offerte personalizzate sul sito.

![edge-audience-enrich](assets/edge-audience-enrich.png)

## Passaggi

1. **Salva e avvia** la composizione del pubblico federato. Una volta eseguita la composizione, il pubblico federato verrà visualizzato nel portale del pubblico.
2. **Crea una regola di pubblico** utilizzando gli attributi del profilo e gli eventi di esperienza dal servizio Profilo, incorporando il pubblico federato.

Concludiamo questo con un [riepilogo degli insegnamenti e delle soluzioni finali](conclusion.md)!
