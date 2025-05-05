---
title: Autenticazione e accesso alle API di Experience Platform
description: Scopri come accedere alle API di Adobe Experience Platform.
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 10%

---

# Autentica e accedi a [!DNL Experience Platform] API

Scopri come iniziare a utilizzare le API di Adobe Experience Platform. Questa esercitazione ti guida attraverso la procedura per creare le credenziali di autenticazione e iniziare ad effettuare richieste API Experience Platform.

## Creazione di un progetto in Adobe Developer Console ed esportazione di un ambiente Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) è un&#39;applicazione di terze parti che consente agli sviluppatori di interagire in modo rapido e semplice con le API di Adobe Experience Platform.

La funzionalità [Esporta dettagli per Postman **di Adobe Developer Console](https://developer.adobe.com/console/projects)** consente di esportare facilmente i dettagli dell&#39;account necessari per accedere e interagire con le API di Experience Platform in un unico file di ambiente Postman, eliminando la necessità di copiare e incollare i valori da Adobe Developer Console in Postman.

>[!IMPORTANT]
>
>Per accedere a [Adobe Developer Console](https://developer.adobe.com/console/projects), devi essere un [Amministratore di sistema](https://helpx.adobe.com/it/enterprise/using/admin-roles.html) o uno [Sviluppatore](https://helpx.adobe.com/it/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) in [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Dopo aver creato le credenziali API, un amministratore di sistema deve associarle a un ruolo in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&enablevpops)

## Generare un token di accesso con Postman{#generate-an-access-token-with-postman}

Utilizza le [API del servizio Adobe Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) per ottenere un token di accesso per accedere alle API di Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on&enablevpops)


## Interagire con le API di Experience Platform tramite Postman

Esplora l&#39;interazione con le API di Adobe Experience Platform utilizzando le [raccolte Postman API di Experience Platform fornite da Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), sulla base delle [variabili di ambiente Adobe Developer Console](#export-integration-details-to-postman) e del [token di accesso generato](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on&enablevpops)


## Risorse a cui si fa riferimento in questi video

* [Adobe Developer Console](https://developer.adobe.com/console/projects)
* [Esempi di Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Raccolta Postman di sistema di Identity Management per la generazione dei token di accesso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Raccolte Postman API Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Scarica Postman](https://www.postman.com/)
