---
title: 'Pianificazione: migrazione da Adobe Target a Adobe Journey Optimizer, estensione Decisioning Mobile'
description: Scopri come pianificare l’implementazione di Adobe Target da at.js 2.x a Adobe Experience Platform Web SDK.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Pianificare la migrazione di Target all’estensione Decisioning

Prima di aggiornare Target dall’estensione Target all’estensione Decisioning nell’app mobile, è necessario valutare l’implementazione corrente.

## Valuta l’implementazione corrente dell’estensione Target

Il primo passaggio per una migrazione di successo consiste nell’acquisire una solida conoscenza dell’implementazione corrente dell’estensione Target. Potresti utilizzare funzioni, funzioni e codice personalizzato che richiedono aggiornamenti. Durante la valutazione, considera quanto segue:

### Quali funzioni sono supportate?

<!--Platform Web SDK is under continuous active development and features and enhancements are added regularly. As you evaluate your current at.js implementation, refer to the [supported use cases](https://github.com/orgs/adobe/projects/18/views/1) page for the latest information.-->

### Quali funzioni utilizza oggi?

<!--Platform Web SDK is a new library that consolidates all Adobe solutions for the websites into a single SDK. This enables tighter integration and enables new capabilities unique to Adobe Experience Platform. However, this also means at.js functions are not backwards compatible with Platform Web SDK. As you evaluate your current implementation, make note of the following:

- at.js functions such as `getOffer()` and `applyOffer()`
- Modifications to Target's global settings
- Integration with Adobe Analytics
- Use of a flicker mitigation script
- Use of response tokens
- Use of mbox, profile, and entity parameters
- Custom code unique to your implementation-->

### Quale approccio di migrazione adotterai?

<!--Once you have revisited your at.js implementation, you need to determine a migration approach. There are two options:

- Migrate all Adobe applications at once across the entire site
- Migrate on a page-by-page basis

Because Platform Web SDK combines and enables multiple Adobe applications, you must coordinate the Target migration of other Adobe applications like Analytics and Audience Manager. All Adobe libraries on a given page should be migrated at the same time. A mixed implementation of Platform Web SDK for Target and AppMeasurement for Analytics on a particular page is not supported. However, a mixed implementation across different pages is supported, for example Platform Web SDK on page A, and at.js with AppMeasurement on page B.

As you migrate, you should plan on following your company's process for testing and releasing new code and use things like development, qa, and staging environments before you release to production.-->

<!--
>[!CAUTION]
>
>Redirect offers are not supported in page-by-page migrations if redirecting from a page with one library to a page with a different library
-->


Rivedi quindi il confronto dettagliato [tra l&#39;estensione Target e l&#39;estensione Decisioning](detailed-comparison.md) per comprendere meglio le differenze tecniche e identificare le aree che richiedono un&#39;attenzione aggiuntiva.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
