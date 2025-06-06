---
title: Guida introduttiva ad Adobe I/O
description: Guida introduttiva ad Adobe I/O
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: a45283bf5263a6de5c2f83f5be35b7d03ce04d7d
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Configurare il progetto Adobe I/O

## Creare un progetto Adobe I/O

In questo esercizio, Adobe I/O viene utilizzato per eseguire query su vari endpoint di Adobe. Segui questi passaggi per configurare Adobe I/O.

Vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects){target="_blank"}.

![Nuova integrazione Adobe I/O](./images/iohome.png){zoomable="yes"}

Assicurati di selezionare l’istanza corretta nell’angolo in alto a destra dello schermo. L&#39;istanza è `--aepImsOrgName--`.

>[!NOTE]
>
> La schermata seguente mostra un’organizzazione specifica selezionata. Durante l’esercitazione, è molto probabile che il nome dell’organizzazione sia diverso. Quando ti sei iscritto a questo tutorial, ti sono stati forniti i dettagli dell’ambiente da utilizzare, segui queste istruzioni.

Selezionare **Crea nuovo progetto**.

![Nuova integrazione Adobe I/O](./images/iocomp.png){zoomable="yes"}

### API FIREFLY SERVICES

>[!IMPORTANT]
>
>A seconda del percorso di apprendimento selezionato, potresti non avere accesso all’API di Firefly Services. Potrai accedere all&#39;API di Firefly Services solo se ti trovi nel percorso di apprendimento **Firefly**, **Workfront Fusion**, **ALL** o se stai partecipando a un **workshop live di persona**. Puoi saltare questo passaggio se non sei su uno di questi percorsi di apprendimento.

Dovresti vedere questo. Selezionare **+ Aggiungi al progetto** e scegliere **API**.

![Nuova integrazione Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

Lo schermo dovrebbe essere simile al seguente.

![Nuova integrazione Adobe I/O](./images/api1.png){zoomable="yes"}

Seleziona **Creative Cloud** e scegli **Firefly - Firefly Services**, quindi seleziona **Next**.

![Nuova integrazione Adobe I/O](./images/api3.png){zoomable="yes"}

Specifica un nome per le credenziali: `--aepUserLdap-- - One Adobe OAuth credential` e seleziona **Avanti**.

![Nuova integrazione Adobe I/O](./images/api4.png){zoomable="yes"}

Selezionare il profilo predefinito **Configurazione Firefly Services predefinita** e selezionare **Salva API configurata**.

![Nuova integrazione Adobe I/O](./images/api9.png){zoomable="yes"}

Dovresti vedere questo.

![Nuova integrazione Adobe I/O](./images/api10.png){zoomable="yes"}

### API PHOTOSHOP SERVICES

>[!IMPORTANT]
>
>A seconda del percorso di apprendimento selezionato, potresti non avere accesso all’API di Photoshop Services. Potrai accedere all&#39;API di Photoshop Services solo se ti trovi nel percorso di apprendimento **Firefly**, **Workfront Fusion**, **ALL** o se stai partecipando a un **workshop live di persona**. Puoi saltare questo passaggio se non sei su uno di questi percorsi di apprendimento.

Selezionare **+ Aggiungi al progetto**, quindi selezionare **API**.

![Archiviazione Azure](./images/ps2.png){zoomable="yes"}

Seleziona **Creative Cloud** e scegli **Photoshop - Firefly Services**. Seleziona **Avanti**.

![Archiviazione Azure](./images/ps3.png){zoomable="yes"}

Seleziona **Avanti**.

![Archiviazione Azure](./images/ps4.png){zoomable="yes"}

Successivamente, devi selezionare un profilo di prodotto che definisca quali autorizzazioni sono disponibili per questa integrazione.

Selezionare **Configurazione predefinita Firefly Services** e **Configurazione predefinita Creative Cloud Automation Services**.

Seleziona **Salva API configurata**.

![Archiviazione Azure](./images/ps5.png){zoomable="yes"}

Dovresti vedere questo.

![Nuova integrazione Adobe I/O](./images/ps7.png){zoomable="yes"}

### API ADOBE EXPERIENCE PLATFORM

>[!IMPORTANT]
>
>A seconda del percorso di apprendimento selezionato, potresti non avere accesso all’API di Adobe Experience Platform. Potrai accedere all&#39;API di Adobe Experience Platform solo se ti trovi nel percorso di apprendimento **AEP + App**, **ALL** o se stai partecipando a un **workshop live di persona**. Puoi saltare questo passaggio se non sei su uno di questi percorsi di apprendimento.

Selezionare **+ Aggiungi al progetto**, quindi selezionare **API**.

![Archiviazione Azure](./images/aep1.png){zoomable="yes"}

Seleziona **Adobe Experience Platform** e scegli **Experience Platform API**. Seleziona **Avanti**.

![Archiviazione Azure](./images/aep2.png){zoomable="yes"}

Seleziona **Avanti**.

![Archiviazione Azure](./images/aep3.png){zoomable="yes"}

Successivamente, devi selezionare un profilo di prodotto che definisca quali autorizzazioni sono disponibili per questa integrazione.

Selezionare **Adobe Experience Platform - Tutti gli utenti - PROD**.

>[!NOTE]
>
>Il nome del profilo di prodotto per AEP dipende da come è stato configurato l’ambiente. Se il profilo di prodotto sopra indicato non viene visualizzato, è possibile che sia presente un profilo di prodotto denominato **Default Production All Access**. Se non sai quale scegliere, rivolgiti all’amministratore di sistema di AEP.

Seleziona **Salva API configurata**.

![Archiviazione Azure](./images/aep4.png){zoomable="yes"}

Dovresti vedere questo.

![Nuova integrazione Adobe I/O](./images/aep5.png){zoomable="yes"}

### Nome progetto

Fai clic sul nome del progetto.

![Nuova integrazione Adobe I/O](./images/api13.png){zoomable="yes"}

Seleziona **Modifica progetto**.

![Nuova integrazione Adobe I/O](./images/api14.png){zoomable="yes"}

Immetti un nome descrittivo per l&#39;integrazione: `--aepUserLdap-- One Adobe tutorial` e seleziona **Salva**.

![Nuova integrazione Adobe I/O](./images/api15.png){zoomable="yes"}

La configurazione del progetto Adobe I/O è terminata.

![Nuova integrazione Adobe I/O](./images/api16.png){zoomable="yes"}

## Passaggi successivi

Vai a [Opzione 1: installazione di Postman](./ex7.md){target="_blank"}

Vai a [Opzione 2: installazione di PostBuster](./ex8.md){target="_blank"}

Torna a [Guida introduttiva](./getting-started.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
