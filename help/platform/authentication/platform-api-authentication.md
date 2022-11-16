---
title: Autenticazione e accesso alle API di Experience Platform
description: Scopri come accedere alle API di Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 10%

---

# Autenticazione e accesso [!DNL Experience Platform] API

Per effettuare chiamate alle API Adobe Experience Platform, devi prima ottenere l’accesso a un account sviluppatore Experience Platform.

Per istruzioni dettagliate su come accedere a un account sviluppatore, visita il [Experience Platform di esercitazione sull’autenticazione API](https://www.adobe.com/go/platform-api-authentication-en).

## Creare ed esportare l’API Experience Platform in Postman

[Postman](https://www.getpostman.com/) è uno strumento che consente agli sviluppatori di interagire in modo rapido e semplice con le API Adobe Experience Platform.

Console di Adobe Developer **Dettagli esportazione per Postman** Questa funzionalità consente di esportare facilmente tutti i dettagli dell’account necessari per accedere e interagire con un’API di Experience Platform in un singolo file dell’ambiente Postman, eliminando la necessità di copiare e incollare i valori dalla console Adobe Developer in Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## Generare un token di accesso con Postman

Utilizza la [API del servizio Adobe Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) per ottenere un token di accesso per accedere alle API Adobe Experience Platform per uso non di produzione

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> Come indicato nell&#39;insieme Adobe I/O Access Token Generation Postman , i metodi di generazione indicati sono adatti per uso non di produzione. La firma locale carica una libreria JavaScript da un host di terze parti e la firma remota invia la chiave privata a un servizio Web di proprietà e gestito da Adobe. Sebbene Adobe non memorizzi questa chiave privata, le chiavi di produzione non devono mai essere condivise con nessuno.

## Interazione con le API di Adobe I/O tramite Postman

Scopri come interagire con le API di Adobe I/O utilizzando [Raccolte Postman API di Experience Platform fornite da Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), sulla base [Variabili dell’ambiente di Adobe I/O](#export-adobe-io-integration-details-to-postman) e [token di accesso generato](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

Tieni presente che le raccolte Postman fornite da Adobe potrebbero non esistere per ogni API di Adobe I/O, tuttavia la [Experience Platform raccolte Postman API](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) può essere utilizzato come guida su come definire le tue raccolte Postman per questi casi d’uso.

## Risorse aggiuntive

* [Console Adobe I/O](https://console.adobe.io)
* [Esempi Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Raccolta Postman di Adobe I/O Access Token Generation](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Raccolte Postman API di Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Scarica Postman](https://www.getpostman.com/)
