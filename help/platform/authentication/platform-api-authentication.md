---
title: Autenticazione e accesso alle API di Experience Platform
description: Scopri come accedere alle API di Adobe Experience Platform.
role: Developer
feature: API
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 13%

---

# Autenticazione e accesso [!DNL Experience Platform] API

Scopri come iniziare a utilizzare le API di Adobe Experience Platform. Questa esercitazione ti guida attraverso la procedura per creare le credenziali di autenticazione e iniziare ad effettuare richieste API Experience Platform.

## Creare un progetto nella console Adobe Developer ed esportare un ambiente Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) è un’applicazione di terze parti che consente agli sviluppatori di interagire in modo rapido e semplice con le API di Adobe Experience Platform.

[della console Adobe Developer](https://developer.adobe.com/console/home) **Esporta dettagli per Postman** Questa funzionalità consente di esportare facilmente i dettagli dell’account necessari per accedere e interagire con un’API di Experience Platform in un singolo file di ambiente Postman, eliminando la necessità di copiare e incollare valori dalla console Adobe Developer in Postman.

>[!IMPORTANT]
>
>Per accedere al [Console Adobe Developer](https://developer.adobe.com/console/home), devi essere un [Amministratore di sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html) o un [Sviluppatore](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) nel [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Dopo aver creato le credenziali API, un amministratore di sistema deve associarle a un ruolo nell’Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)




## Generare un token di accesso con Postman{#generate-an-access-token-with-postman}

Utilizza il [Adobe API del servizio Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) ottenere un token di accesso per accedere alle API di Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interagire con le API di Experience Platform tramite Postman

Esplora l’interazione con le API di Adobe Experience Platform utilizzando [Raccolte Postman Experience Platform API fornite dall’Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), basandosi sulla [Variabili di ambiente della console Adobe Developer](#export-integration-details-to-postman) e [token di accesso generato](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Risorse a cui si fa riferimento in questi video

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Esempi di Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Raccolta Postman di sistema di Identity Management per la generazione dei token di accesso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Raccolte Postman API di Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Scarica Postman](https://www.postman.com/)
