---
title: Autenticazione e accesso alle API di Experience Platform
description: Scopri come accedere alle API di Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 15%

---

# Autenticazione e accesso [!DNL Experience Platform] API

Per effettuare richieste alle API di Adobe Experience Platform, devi disporre di un account sviluppatore Experience Platform.

## Creare un progetto nella console Adobe Developer ed esportare un ambiente Postman

[[!DNL Postman]](https://www.postman.com/) è uno strumento che consente agli sviluppatori di interagire in modo rapido e semplice con le API di Adobe Experience Platform.

della console Adobe Developer **Esporta dettagli per Postman** Questa funzionalità consente di esportare facilmente tutti i dettagli dell’account necessari per accedere e interagire con un’API Experience Platform in un singolo file di ambiente Postman, eliminando la necessità di copiare e incollare valori dalla console Adobe Developer in Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>Dopo aver creato le credenziali API, un amministratore di sistema della società deve associarle a un ruolo di Experience Platform.


## Generare un token di accesso con Postman

Utilizza il [Adobe API del servizio Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) ottenere un token di accesso per accedere alle API di Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interagire con le API di Experience Platform tramite Postman

Esplora l’interazione con le API di Adobe Experience Platform utilizzando [Raccolte Postman Experience Platform API fornite dall’Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), basandosi sulla [Variabili di ambiente della console Adobe Developer](#export-adobe-io-integration-details-to-postman) e [token di accesso generato](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Risorse aggiuntive

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Esempi di Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Raccolta Postman di sistema di Identity Management per la generazione dei token di accesso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Raccolte Postman API di Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Scarica Postman](https://www.postman.com/)
