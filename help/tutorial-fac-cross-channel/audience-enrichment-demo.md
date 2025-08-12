---
title: Arricchire il pubblico di Experience Platform con i dati federati
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Arricchire il pubblico di Experience Platform con i dati federati
description: In questa lezione, arricchiamo un pubblico di Experience Platform con dati federati.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 5%

---


# Composizione di pubblico federato

La Composizione federata del pubblico consente di arricchire i tipi di pubblico esistenti in Adobe Experience Platform (AEP) utilizzando i dati del pubblico composto che sono stati federati dal data warehouse aziendale. Questi dati non verranno mantenuti nei profili cliente di Adobe Experience Platform.

## Modi per arricchire una composizione di pubblico federato

Esistono due metodi principali per arricchire una Federated Audience Composition.

### &#x200B;1. Lettura di un pubblico di AEP all’interno di una composizione federata

In questo primo esempio utilizzeremo il pubblico **SecurFinancial Loan Application Page Visitor** memorizzato in AEP Profile Service per avviare la composizione federata. Arricchiremo il pubblico utilizzando i dati federati in Snowflake per determinare la pre-approvazione in base al punteggio di credito e all’attività di prestito.

![federated-composition-example](assets/snowflake-preapproval.png)

1. **Mappa il pubblico di AEP** alla destinazione Federated Audience Composition.
2. **Crea la tua composizione** con il pubblico mappato come Read audience.
3. **Riconcilia le identità** nel pubblico di lettura per unirti ai dati federati.

![metodo-federato-1-1](assets/federated-method-1-1.png)

![metodo-federato-1-2](assets/federated-method-1-2.png)

### &#x200B;2. Arricchimento della regola del pubblico di Experience Platform con un pubblico federato

Nel secondo esempio, utilizzeremo il pubblico federato interrogato con il punteggio di credito e l’attività di prestito per arricchire il pubblico comportamentale dei visitatori della pagina web della richiesta di prestito.

Valutando questo pubblico su Edge, possiamo eseguire immediatamente il retargeting dei visitatori della pagina di richiesta di prestito preapprovata con offerte personalizzate sul sito.

![edge-audience-enrich](assets/edge-audience-enrich.png)

1. **Salva e avvia** la composizione del pubblico federato. Una volta eseguita la composizione, il pubblico federato verrà visualizzato nel portale del pubblico.
2. **Crea una regola di pubblico** utilizzando gli attributi del profilo e gli eventi di esperienza dal servizio Profilo, incorporando il pubblico federato.

Concludiamo questo con un [riepilogo degli insegnamenti e delle soluzioni finali](conclusion.md)!
