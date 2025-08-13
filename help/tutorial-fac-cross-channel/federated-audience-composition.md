---
title: Arricchire il pubblico di Experience Platform con i dati federati
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Arricchire il pubblico di Experience Platform con i dati federati
description: In questo esercizio visivo, un pubblico di Experience Platform viene arricchito di dati federati.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 3de9721332379f9fd3dd45768ba2ca2308e09357
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 7%

---

# Arricchire il pubblico di Experience Platform con Federated Data

La Composizione federata del pubblico consente di arricchire i tipi di pubblico esistenti in Adobe Experience Platform (AEP) utilizzando i dati del pubblico composto che sono stati federati dal data warehouse aziendale. Questi dati non verranno mantenuti nei profili cliente di Adobe Experience Platform.

## Lettura di un pubblico di AEP in una composizione federata

In questo esercizio visivo utilizziamo il pubblico **SecurFinancial Loan Application Page Visitor** memorizzato in AEP Profile Service per avviare la composizione federata. Utilizza i dati federati in Snowflake per determinare la pre-approvazione in base al punteggio di credito e all’attività di prestito.

![federated-composition-example](assets/snowflake-preapproval.png)

### Passaggi

1. **Mappa il pubblico di AEP** alla destinazione Federated Audience Composition.
2. **Crea la tua composizione** con il pubblico mappato come Read audience.
3. **Riconcilia le identità** nel pubblico di lettura per unirti ai dati federati.

![metodo-federato-1-1](assets/federated-method-1-1.png)

![metodo-federato-1-2](assets/federated-method-1-2.png)

Esamineremo un altro esempio di utilizzo dei dati federati per [supportare la personalizzazione &quot;nel momento&quot;](drive-in-the-moment-personalization.md).
