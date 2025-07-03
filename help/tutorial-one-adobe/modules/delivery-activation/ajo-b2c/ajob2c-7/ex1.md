---
title: 'Experience Decisioning: Experience Decisioning 101'
description: 'Experience Decisioning: Experience Decisioning 101'
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 3.7.1 Experience Decisioning 101

## Terminologia 3.7.1.1

Per comprendere meglio Experience Decisioning, ti consigliamo di leggere la [panoramica](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) sul funzionamento del servizio applicativo Offer Decisioning con Adobe Experience Platform.

Quando si lavora con Offer Decisioning, è necessario comprendere i seguenti concetti:

| Termine | Spiegazione |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Offerta** | Un’offerta è un messaggio di marketing a cui possono essere associate delle regole che determinano gli utenti idonei per visualizzare l’offerta. Un’offerta ha uno stato: bozza, approvata o archiviata. |
| **Posizionamento** | La combinazione di posizione (o tipo di canale) e contesto (o tipo di contenuto) in cui un’offerta viene visualizzata per un utente finale. In effetti, si tratta della combinazione di testo, HTML, immagine, JSON in canali mobili, web, social, messaggistica istantanea e non digitali. |
| **Regola** | La logica che definisce e controlla l’idoneità degli utenti finali a un’offerta. |
| **Offerta Personalizzata** | Un messaggio di marketing personalizzabile basato su regole e vincoli di idoneità. |
| **Offerta di fallback** | L’offerta predefinita viene visualizzata quando un utente finale non è idoneo per nessuna delle offerte nella raccolta utilizzata. |
| **Limitazione** | Utilizzato in una definizione di offerta per definire quante volte un’offerta può essere presentata in totale e a un utente specifico. |
| **Priorità** | Livello per determinare la classificazione di priorità da un set di risultati di offerte. |
| **Raccolta** | Utilizzato per filtrare un sottoinsieme di offerte dall’elenco delle offerte personalizzate per velocizzare il processo di Offer Decisioning. |
| **Decisione** | Combinazione di un set di offerte, posizionamento e profilo per cui l’addetto marketing desidera che il motore decisionale fornisca l’offerta migliore. |
| **AEM Assets Essentials** | Un&#39;esperienza universale e centralizzata per l&#39;archiviazione, la ricerca e la selezione delle risorse nelle soluzioni Adobe Experience Cloud e Adobe Experience Platform. |

{style="table-layout:auto"}

## 3.7.1.2 Experience Decisioning

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Nel prossimo esercizio, configurerai le tue offerte e la tua decisione.

## Passaggi successivi

Vai a [3.7.2 Configurare le offerte e la decisione](./ex2.md){target="_blank"}

Torna a [Experience Decisioning](ajo-decisioning.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
