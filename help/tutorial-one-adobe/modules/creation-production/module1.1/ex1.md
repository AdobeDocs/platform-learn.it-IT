---
title: Guida introduttiva ai servizi Firefly
description: Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 1.1.1 Guida introduttiva ai servizi Firefly

Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly.

## 1.1.1.1 Prerequisiti

Prima di continuare con questo esercizio, devi aver completato la configurazione di [il tuo progetto Adobe I/O](./../../../modules/getting-started/gettingstarted/ex6.md) e devi anche aver configurato un&#39;applicazione per interagire con le API, ad esempio [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) o [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md).

## 1.1.1.2 Adobe I/O - access_token

Nella raccolta **Adobe IO - OAuth**, selezionare la richiesta denominata **POST - Ottieni token di accesso** e selezionare **Invia**. La risposta deve contenere un nuovo **accestoken**.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.3 API dei servizi Firefly, testo 2 immagine

Ora che disponi di un access_token valido e aggiornato, puoi inviare la prima richiesta alle API dei servizi Firefly.

Selezionare la richiesta denominata **POST - Firefly - T2I V3** dalla raccolta **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png){zoomable="yes"}

Copia l’URL dell’immagine dalla risposta e aprilo nel browser web per visualizzarla.

![Firefly](./images/ff2.png){zoomable="yes"}

Dovresti vedere una bella immagine che rappresenta `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

Puoi rispondere alla richiesta API prima di continuare con l’esercizio successivo.

## Passaggi successivi

Vai a [Ottimizza il processo Firefly utilizzando Microsoft Azure e gli URL prefirmati](./ex2.md){target="_blank"}

Torna a [Panoramica dei servizi Adobe Firefly](./firefly-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
