---
title: Incentivare la personalizzazione "nel momento" su Edge
seo-title: Drive "in-the moment" personalization on the Edge | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Incentivare la personalizzazione "nel momento" su Edge
description: In questo esercizio visivo, il pubblico federato viene valutato in Edge per il retargeting immediato e immediato.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
hide: true
source-git-commit: 0bbdc93969b4716407ecf51499d572cb50f5a0d3
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# Incentivare la personalizzazione &quot;nel momento&quot; su Edge

La Composizione federata del pubblico consente di arricchire i tipi di pubblico esistenti in Adobe Experience Platform (AEP) utilizzando i dati del pubblico composto che sono stati federati dal data warehouse aziendale. Questi dati non verranno mantenuti nei profili cliente di Adobe Experience Platform.

In questo esercizio visivo utilizziamo un pubblico federato interrogato con il punteggio di credito e l’attività di prestito per arricchire il pubblico comportamentale dei visitatori della pagina web della richiesta di prestito.

Valutando questo pubblico su Edge, effettuiamo immediatamente il retargeting dei visitatori della pagina di richiesta di prestito preapprovata con offerte personalizzate sul sito.

![edge-audience-enrich](assets/edge-audience-enrich.png)

## Passaggi

1. **Salva e avvia** la composizione del pubblico federato. Una volta eseguita la composizione, il pubblico federato verrà visualizzato nel portale del pubblico.
2. **Crea una regola di pubblico** utilizzando gli attributi del profilo e gli eventi di esperienza dal servizio Profilo, incorporando il pubblico federato.

Concludiamo questo con un [riepilogo degli insegnamenti e delle soluzioni finali](conclusion.md)!
