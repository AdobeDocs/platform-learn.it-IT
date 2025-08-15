---
title: Arricchire i tipi di pubblico con i dati warehouse
seo-title: Enrich Audiences with warehouse data | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Arricchire i tipi di pubblico con i dati warehouse
description: In questo esercizio, un pubblico di Experience Platform viene arricchito con i dati di magazzino.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 7e2f7bbb392eba51c0d6b9ccc8224c2081a01c7c
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---

# Arricchire i tipi di pubblico con i dati warehouse

La Composizione federata del pubblico consente di arricchire i tipi di pubblico esistenti in Adobe Experience Platform (AEP) utilizzando i dati del pubblico composto che sono stati federati dal data warehouse aziendale. Questi dati non verranno mantenuti nei profili cliente di Adobe Experience Platform.

## Lettura di un pubblico in una composizione federata

In questo esercizio utilizzeremo il pubblico **SecurFinancial Loan Application Page Visitor** memorizzato in Experience Platform Profile Service per avviare la nostra composizione federata. Utilizza i dati federati in Snowflake per determinare la pre-approvazione in base al punteggio di credito e all’attività di prestito.

![federated-composition-example](assets/snowflake-preapproval.png)

### Passaggi

1. **Mappa il pubblico di AEP** alla destinazione Federated Audience Composition.
2. **Crea la tua composizione** con il pubblico mappato come Read audience.
3. **Riconcilia le identità** nel pubblico di lettura per unirti ai dati federati.

![metodo-federato-1-1](assets/federated-method-1-1.png)

![metodo-federato-1-2](assets/federated-method-1-2.png)

Esamineremo un altro esempio di utilizzo dei dati federati per [distribuire la personalizzazione &quot;nel momento&quot;](deliver-in-the-moment-personalization.md).
