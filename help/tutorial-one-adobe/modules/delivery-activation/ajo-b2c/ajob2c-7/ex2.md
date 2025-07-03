---
title: 'Offer Decisioning: configurare le offerte e l’ID decisione'
description: 'Offer Decisioning: configurare le offerte e l’ID decisione'
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---

# 3.7.2 Configurare le offerte e la decisione

## 3.7.2.1 Crea le tue offerte personalizzate

In questo esercizio creerai quattro **offerte personalizzate**. Di seguito sono riportati i dettagli da tenere in considerazione per la creazione di tali offerte:

| Nome | Date Range | Collegamento immagine per e-mail | Collegamento immagine per il Web | Testo | Priorità | Idoneità | Lingua | Frequenza limite | Nome immagine |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | oggi - 1 mese dopo | https://bit.ly/4a9RJ5d | Scegli una delle librerie Assets | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | all - Clienti femminili | Inglese (Stati Uniti) | 3 | Apple AirPods Max- Femmina.jpg |
| `--aepUserLdap-- - Galaxy S24` | oggi - 1 mese dopo | https://bit.ly/3W8yuDv | Scegli una delle librerie Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | all - Clienti femminili | Inglese (Stati Uniti) | 3 | Galaxy S24 - Femmina.jpg |
| `--aepUserLdap-- - Apple Watch` | oggi - 1 mese dopo | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | all - Clienti maschi | Inglese (Stati Uniti) | 3 | Apple Watch - Maschio.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | oggi - 1 mese dopo | https://bit.ly/4gTrkeo | Scegli una delle librerie Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | all - Clienti maschi | Inglese (Stati Uniti) | 3 | Galaxy Watch7 - Maschio.jpg |

{style="table-layout:auto"}

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Passaggi successivi

Vai a [3.7.3 Installazione di Web SDK per Experience Decisioning](./ex3.md){target="_blank"}

Torna a [Experience Decisioning](ajo-decisioning.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
